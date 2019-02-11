# Turning

These custom functions for pivoting or turning the robot use the [wheel encoders](../physical-inputs/wheel-encoders.md):

* `pivotAngle()` — pivot on both wheels by specific angle
* `turnAngle()` — turn on one wheel by specific angle

## pivotAngle\(\)

A custom function named `pivotAngle()` uses the wheel encoders to make your robot pivot by a specified angle.

When calling this custom function, you must pass in a value for the **angle** \(degrees\) by listing the value inside the parentheses after the function's name.:

* A **positive** angle will pivot the robot **clockwise** to the right.
* A **negative** angle will pivot the robot **counter-clockwise** to the left.

For example, to make your robot pivot 90 degrees right:

```cpp
pivotAngle(90);
```

To make your robot pivot 90 degrees left:

```cpp
pivotAngle(-90);
```

Add this `pivotAngle()` custom function **after** the `loop()` function:

```cpp
void pivotAngle(float angle) {

    // use wheel encoders to pivot (turn) by specified angle

    // set motor power for pivoting
    int power = 100; // clockwise
    if (angle < 0) power *= -1; // negative power for counter-clockwise

    // use correction to improve angle accuracy
    // adjust correction value based on test results
    float correction = -5.0; // need decimal point for float value
    if (angle > 0) angle += correction;
    else if (angle < 0) angle -= correction;

    // variable for tracking wheel encoder counts
    long rightCount = 0;

    // values based on RedBot's encoders, motors & wheels
    float countsPerRev = 192.0; // 192 encoder ticks per wheel revolution
    float wheelDiam = 2.56; // wheel diameter = 65 mm = 2.56 in
    float wheelCirc = PI * wheelDiam; // wheel circumference = 3.14 x 2.56 in = 8.04 in
    float pivotDiam = 6.125; // pivot diameter = distance between centers of wheel treads = 6.125 in
    float pivotCirc = PI * pivotDiam; // pivot circumference = 3.14 x 6.125 in = 19.23 in

    // based on angle, calculate distance (arc length) for pivot
    float distance = abs(angle) / 360.0 * pivotCirc;

    // based on distance, calculate number of wheel revolutions
    float numRev = distance / wheelCirc;

    // based on number of revolutions, calculate target encoder count
    float targetCount = numRev * countsPerRev;

    // reset encoder counters and start pivoting
    encoder.clearEnc(BOTH);
    delay(100);
    motors.pivot(power);

    // keeps looping while right encoder count less than target count
    while (abs(rightCount) < abs(targetCount)) {
        // get current wheel encoder count
        rightCount = encoder.getTicks(RIGHT);
        delay(10);  // short delay before next reading
    }

    // target count reached
    motors.brake();
    delay(250);
    
    // uncomment next statement only if using driveStraight() or countLine() elsewhere in program
    // clearEncoders();
}
```

