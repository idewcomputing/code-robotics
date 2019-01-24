# Detecting Lines

These custom functions use the [IR line sensors](../physical-inputs/ir-line-sensors.md):

* `followLine()` — follow a line automatically
* `avoidLine()` — avoid a line automatically \(acts like border to contain robot\)
* `countLine()` — drive straight while counting lines crossed and stop at specific line number
* `followCountLine()` — follow a line while counting lines crossed and stop at specific line number

## followLine\(\)

A custom function named `followLine()` uses the IR line sensors to make your robot follow a line. The line determines the robot's path.

```cpp
void followLine() {
  /* FOLLOW LINE
  To follow dark line on light surface:
  Use high threshold & see if sensors greater than threshold
  
  To follow light line on dark surface:
  Use low threshold & see if sensors less than threshold
  */

  int leftPower, rightPower;
  int power = 100;
  int powerShift = 50;
  int lineThreshold = 800; // change value if necessary

  // get IR sensor readings
  int leftSensor = leftLine.read();
  int centerSensor = centerLine.read();
  int rightSensor = rightLine.read();

  // if line under center sensor, drive straight to stay aligned
  if (centerSensor > lineThreshold) {
    // set both motors to same power
    leftPower = power;
    rightPower = power;
  }
  // if line under left sensor, curve left to realign
  else if (leftSensor > lineThreshold) {
    // decrease left motor, increase right motor
    leftPower = power - powerShift;
    rightPower = power + powerShift;
  }
  // if line under right sensor, curve right to realign
  else if (rightSensor > lineThreshold) {
    // increase left motor, decrease right motor
    leftPower = power + powerShift;
    rightPower = power - powerShift;
  }

  // drive motors using power values from above
  motors.leftDrive(leftPower);
  motors.rightDrive(rightPower);

  delay(25);  // can change delay to adjust line following sensitivity    
}
```

## avoidLine\(\)

A custom function named `followLine()` uses the IR line sensors to make your robot avoid a line. The line acts as a border to keep the robot inside \(or outside\) a certain area or path.

```cpp
void avoidLine() {
  /* AVOID LINE
  To avoid dark line on light surface:
  Use high threshold & see if sensors greater than threshold

  To avoid light line on dark surface:
  Use low threshold & see if sensors less than threshold
  */

  // adjust value if necessary
  int lineThreshold = 800;

  // get IR sensor readings (only need left and right)
  int leftSensor = leftLine.read();
  int rightSensor = rightLine.read();

  // if either sensor detects line, first brake motors
  if (leftSensor > lineThreshold || rightSensor > lineThreshold) {
    motors.brake();
    delay(250);
  }

  // if both sensors on line, turn around (about 180 degrees)
  if (leftSensor > lineThreshold && rightSensor > lineThreshold) {
    long randomNum = random(975, 1625); // approx 135-225 degree pivot
    motors.pivot(100);
    delay(randomNum);
    motors.stop();
  }
  // if line under left sensor only, turn right (min 90 degrees)
  else if (leftSensor > lineThreshold) {
    long randomNum = random(650, 975); // approx 90-135 degree pivot
    motors.pivot(100); // pivot clockwise to right
    delay(randomNum);
    motors.stop();
  }
  // if line under right sensor only, turn left (min 90 degrees)
  else if (rightSensor > lineThreshold) {
    long randomNum = random(650, 975); // approx 90-135 degree pivot
    motors.pivot(-100); // pivot counter-clockwise to left
    delay(randomNum);
    motors.stop();
  }
  // otherwise, keep driving straight
  else motors.drive(100);

  delay(25);  // can change delay to adjust line following sensitivity    
}
```

