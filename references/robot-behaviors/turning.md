# Turning

These custom functions for pivoting or turning the robot use the [wheel encoders](../physical-inputs/wheel-encoders.md):

* `pivotAngle()` — pivot on both wheels by specific angle
* `turnAngle()` — turn on one wheel by specific angle

## pivotAngle\(\)

A custom function named `pivotAngle()` uses the wheel encoders to make your robot pivot by a specified angle.

When pivoting, the robot turns in a circle centered between the robot's wheels. The distance between the centers of the RedBot wheel treads is 6.125 inches, which represents the diameter of the robot's pivot circle. If the robot pivoted 360°, the distance traveled by each wheel would be equal to the circumference of this pivot circle:

**C = 𝛑 × d = 3.14 × 6.125 = 19.23 inches**

Usually you will want your RedBot to pivot by a specific angle that is less than 360° — such as 45°, 90°, 180°, etc. For any specific angle, you can calculate its **arc length** \(i.e., a "partial circumference"\):

**L = 𝛂 / 360° × 𝛑 × d**

The arc length \(**L**\) represents the distance each wheel will travel while pivoting by a specific angle \(𝛂\).

For example, when pivoting by 90°, the arc length is:

L = 90° / 360° × 𝛑 × d = 0.25 × 3.14 × 6.125 = 4.81 inches

Once this arc length is calculated for a specific angle, the wheel encoders can be used to control how long the wheels are pivoted. This is what the `pivotAngle()` function does.

When calling the `pivotAngle()` function, you must pass in a value for the **angle** \(degrees\) by listing the value inside the parentheses after the function's name.:

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

The `pivotAngle()` function requires these objects as part of your global variables before the `setup()` function:

```cpp
RedBotMotors motors;
RedBotEncoder encoder(A2, 10);
```

Add the `pivotAngle()` custom function **after** the `loop()` function:

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
}
```

## turnAngle\(\)

A custom function named `turnAngle()` uses the wheel encoders to make your robot turn on one wheel by a specified angle.

When turning on one wheel, the robot turns in a circle centered on the stopped wheel. The distance between the centers of the RedBot wheel treads is 6.125 inches, which represents the radius of the robot's turn circle, so the diameter of the turn circle is twice its radius - i.e., 12.25 inches. If the robot turned 360° on one wheel, the distance traveled by the driving wheel would be equal to the circumference of this turn circle:

**C = 𝛑 × d = 3.14 × 12.25 = 38.47 inches**

Usually you will want your RedBot to turn by a specific angle that is less than 360° — such as 45°, 90°, 180°, etc. For any specific angle, you can calculate its **arc length** \(i.e., a "partial circumference"\):

**L = 𝛂 / 360° × 𝛑 × d**

The arc length \(**L**\) represents the distance that the driving wheel will travel while turning by that specific angle \(𝛂\).

For example, when turning on one wheel by 90°, the arc length is:

L = 90° / 360° × 𝛑 × d = 0.25 × 3.14 × 12.25 = 9.62 inches

Once this arc length is calculated for a specific angle, the wheel encoders can be used to control how long the driving wheel travels. This is what the `turnAngle()` function does.

When calling the `turnAngle()` function, you must pass in a value for the **angle** \(degrees\) by listing the value inside the parentheses after the function's name.:

* A **positive** angle will turn the robot **clockwise** to the right.
* A **negative** angle will turn the robot **counter-clockwise** to the left.

For example, to make your robot turn on one wheel 90 degrees right:

```cpp
turnAngle(90);
```

To make your robot turn on one wheel 90 degrees left:

```cpp
turnAngle(-90);
```

The `turnAngle()` function requires these objects as part of your global variables before the `setup()` function:

```cpp
RedBotMotors motors;
RedBotEncoder encoder(A2, 10);
```

Add the `turnAngle()` custom function **after** the `loop()` function:

```cpp
void turnAngle(float angle) {

    // use wheel encoders to turn on one wheel by specified angle

    // set motor power for pivoting
    int power = 100;

    // use correction to improve angle accuracy
    // adjust correction value based on test results
    float correction = 5.0; // need decimal point for float value
    if (angle > 0) angle += correction;
    else if (angle < 0) angle -= correction;

    // variables for tracking wheel encoder counts
    long leftCount = 0;
    long rightCount = 0;

    // values based on RedBot's encoders, motors & wheels
    float countsPerRev = 192.0; // 192 encoder ticks per wheel revolution
    float wheelDiam = 2.56; // wheel diameter = 65 mm = 2.56 in
    float wheelCirc = PI * wheelDiam; // wheel circumference = 3.14 x 2.56 in = 8.04 in
    float turnDiam = 12.25; // turn diameter = 2 x distance between centers of wheel treads = 2 x 6.125 in
    float turnCirc = PI * turnDiam; // turn circumference = 3.14 x 12.25 in = 38.47 in

    // based on angle, calculate distance (arc length) for turn
    float distance = abs(angle) / 360.0 * turnCirc;

    // based on distance, calculate number of wheel revolutions
    float numRev = distance / wheelCirc;

    // based on number of revolutions, calculate target encoder count
    float targetCount = numRev * countsPerRev;

    // reset encoder counters
    encoder.clearEnc(BOTH);
    delay(100);

    // based on turn angle, turn using either left wheel or right wheel
    if (angle > 0) {
        // turn clockwise using left wheel only
        motors.rightStop();
        motors.leftDrive(power);

        // keeps looping while left encoder count less than target count
        while (leftCount < targetCount) {
            // get current wheel encoder count
            leftCount = encoder.getTicks(LEFT);
            delay(10);  // short delay before next reading
        }
    }
    else {
        // turn counter-clockwise using right wheel only
        motors.leftStop();
        motors.rightDrive(power);

        // keeps looping while right encoder count less than target count
        while (rightCount < targetCount) {
            // get current wheel encoder count
            rightCount = encoder.getTicks(RIGHT);
            delay(10); // short delay before next reading
        } 
    }

    // target count reached
    motors.stop();
    delay(250);

    // uncomment following statements only if using driveStraight() elsewhere in program
    // encoder.clearEnc(BOTH);
    // prevLeftCount = 0;
    // prevRightCount = 0;
}
```

