# Driving

These custom functions for driving the robot use the [wheel encoders](../physical-inputs/wheel-encoders.md):

* `driveStraight()` — drive straight continuously
* `driveDistance()` — drive straight for specific distance

## driveStraight\(\)

A custom function named `driveStraight()` uses the wheel encoders to make your robot drive in a straight line.

Driving perfectly straight requires the left and right motors to rotate at the same rate. It is common for a robot to drift slightly \(to the left or right\) when driving. This indicates the motors aren't rotating at the same rate, even though they're using the same motor power.

You can compare the left and right wheel encoder counts as your robot drives to see whether they are the same or not. If they aren't the same, the left and right motor powers can be individually adjusted, so they rotate at similar rates, making the robot drive in a straight line.

In order to work, the `driveStraight()` function must be continuously called by the `loop()` function \(or continuously called by a loop within another function\).

Driving straight continuously is usually combined with other robot behaviors, such as:  detecting collisions, avoiding collisions, avoiding a line, counting lines crossed, etc.

The `driveStraight()` function requires these objects as part of your global variables before the `setup()` function:

```cpp
RedBotMotors motors;
RedBotEncoder encoder(A2, 10);
```

The `driveStraight()` function uses global variables to track the left and right motor powers, as well as the left and right encoder counts. Add this code **before** the `setup()` function:

```cpp
// global variables needed for driveStraight() function
int leftPower = 150, rightPower = leftPower;
long prevLeftCount = 0, prevRightCount = 0;
```

The wheel encoder counters should be reset to zero when your app first starts. Add this code statement **within** the `setup()` function:

```cpp
  encoder.clearEnc(BOTH);
```

Add the `driveStraight()` custom function **after** the `loop()` function:

```cpp
void driveStraight() {

  // use wheel encoders to drive straight continuously

  // amount to offset motor powers to drive straight
  int offset = 5;

  // get current wheel encoder counts
  leftCount = encoder.getTicks(LEFT);
  rightCount = encoder.getTicks(RIGHT);
  
  // calculate increase in count from previous reading
  long leftDiff = leftCount - prevLeftCount;
  long rightDiff = rightCount - prevRightCount;

  // store current counts as "previous" counts for next reading
  prevLeftCount = leftCount;
  prevRightCount = rightCount;

  // adjust left & right motor powers to keep counts similar (drive straight)
  // if left rotated more than right, slow down left & speed up right
  if (leftDiff > rightDiff) {
    leftPower = leftPower - offset;
    rightPower = rightPower + offset;
  }
  // if right rotated more than left, speed up left & slow down right
  else if (leftDiff < rightDiff) {
    leftPower = leftPower + offset;
    rightPower = rightPower - offset;
  }

  // apply adjusted motor powers
  motors.leftDrive(leftPower);
  motors.rightDrive(rightPower);
  delay(10);  // short delay before next reading
}
```

## driveDistance\(\)

A custom function named `driveDistance()` uses the wheel encoders to make your robot drive straight for a specified distance.

[Remember that for the RedBot](../physical-inputs/wheel-encoders.md#calculate-distance-with-encoders), the following is true:

**192 ticks of wheel encoder = 1 wheel revolution = 8.04 inches traveled**

This information can be used to convert any encoder count into distance traveled — or to convert a desired distance into a target encoder count. The `driveDistance()` function uses the encoder counters to control how long the motors are allow to drive.

When calling the `driveDistance()` function, you must pass in a value for the desired **distance** \(inches\) by listing the value inside the parentheses after the function's name.

For example, to make your robot drive 24 inches:

```cpp
driveDistance(24);
```

You can even drive backward by passing in a **negative** value for the distance:

```cpp
driveDistance(-12);
```

The `driveDistance()` function requires these objects as part of your global variables before the `setup()` function:

```cpp
RedBotMotors motors;
RedBotEncoder encoder(A2, 10);
```

Add the `driveDistance()` custom function **after** the `loop()` function:

```cpp
void driveDistance(float distance) {

    // use wheel encoders to drive straight for specified distance at specified power

    // set initial power for left and right motors
    int leftPower = 150;
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
    float correction = -1.0; // need decimal point for float value
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



