# Driving

These custom functions use the [wheel encoders](../physical-inputs/wheel-encoders.md):

* [`driveStraight()`](https://github.com/idewcomputing/code-robotics/tree/a64094b0d9c5c1da17c73efd3f8730c1ce974c2a/references/wheel-encoders.md#drive-straight-continuously) — drive straight continuously
* [`driveDistance()`](https://github.com/idewcomputing/code-robotics/tree/a64094b0d9c5c1da17c73efd3f8730c1ce974c2a/references/wheel-encoders.md#drive-straight-for-specific-distance) — drive straight for specific distance at specific motor power

## driveDistance\(\)

A custom function named `driveDistance()` can be used to make your robot drive straight for a specified distance by using the wheel encoders.

When calling this custom function, you must pass in a value for the **distance** \(inches\) by listing the value inside the parentheses after the function's name.

For example, to make your robot drive 24 inches:

```cpp
driveDistance(24);
```

You can even drive backward by passing in a **negative** value for the distance:

```cpp
driveDistance(-12);
```

Add this `driveDistance()` custom function **after** the `loop()` function:

```cpp
void driveDistance(float distance) {

    // use wheel encoders to drive straight for specified distance at specified power

    // set initial power for left and right motors
    int leftPower = 175;
    int rightPower = leftPower;

    // amount to offset motor powers to drive straight
    int offset = 5;

    // if negative distance, make motor powers & offset also negative
    if (distance < 0) {
        leftPower *= -1;
        rightPower *= -1;
        offset *= -1;
    }

    // use correction to improve distance accuracy
    // adjust correction value based on test results
    float correction = -1.5; // need decimal point for float value
    if (distance > 0) distance += correction;
    else if (distance < 0) distance -= correction;

    // variables for tracking wheel encoder counts
    long leftCount = 0;
    long rightCount = 0;
    long prevLeftCount = 0;
    long prevRightCount = 0;
    long leftDiff, rightDiff;

    // RedBot values based on encoders, motors & wheels
    float countsPerRev = 192.0; // 192 encoder ticks per wheel revolution
    float wheelDiam = 2.56;  // wheel diameter = 65 mm = 2.56 in
    float wheelCirc = PI * wheelDiam; // wheel circumference = 3.14 x 2.56 in = 8.04 in

    // based on distance, calculate number of wheel revolutions
    float numRev = distance / wheelCirc;

    // calculate target encoder count
    float targetCount = numRev * countsPerRev;

    // reset encoder counters and start driving
    encoder.clearEnc(BOTH);
    delay(100);
    motors.leftDrive(leftPower);
    motors.rightDrive(rightPower);

    // keeps looping while right encoder count less than target count
    while (abs(rightCount) < abs(targetCount)) {

        // get current wheel encoder counts
        leftCount = encoder.getTicks(LEFT);
        rightCount = encoder.getTicks(RIGHT);

        // calculate increase in count from previous reading
        leftDiff = abs(leftCount - prevLeftCount);
        rightDiff = abs(rightCount - prevRightCount);

        // store current counts as "previous" counts for next reading
        prevLeftCount = leftCount;
        prevRightCount = rightCount;

        // adjust left & right motor powers to keep counts similar (drive straight)

        // if left rotated more than right, slow down left & speed up right
        if (leftDiff > rightDiff) {
            leftPower = leftPower - offset;
            rightPower = rightPower + offset;
        }
        // else if right rotated more than left, speed up left & slow down right
        else if (leftDiff < rightDiff) {
            leftPower = leftPower + offset;
            rightPower = rightPower - offset;
        }

        // apply adjusted motor powers
        motors.leftDrive(leftPower);
        motors.rightDrive(rightPower);
        delay(10);  // short delay before next reading
    }

    // target count reached
    motors.brake(); // or use: motors.stop()
    delay(500); // brief delay to wait for complete stop
}
```

