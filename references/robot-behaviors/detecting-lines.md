# Detecting Lines

These custom functions use the [IR line sensors](../physical-inputs/ir-line-sensors.md):

* `followLine()` — follow a line automatically
* `avoidLine()` — avoid a line automatically \(acts like border to contain robot\)
* `countLine()` — drive straight while counting lines crossed and stop at specific line number
* `followCountLine()` — follow a line while counting lines crossed and stop at specific line number

## followLine\(\)

A custom function named `followLine()` uses the IR line sensors to make your robot follow a line. The line determines the robot's path.

In order to work, the `followLine()` function must be continuously called by the `loop()` function \(or continuously called by a loop within another function\).

The `followLine()` function requires these objects as part of your global variables before the `setup()` function:

```cpp
RedBotMotors motors;
RedBotSensor leftLine(A3);
RedBotSensor centerLine(A6);
RedBotSensor rightLine(A7);
```

Add the `followLine()` custom function **after** the `loop()` function:

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

A custom function named `avoidLine()` uses the IR line sensors to make your robot avoid a line. The line acts as a border to keep the robot inside \(or outside\) an area or path.

In order to work, the `avoidLine()` function must be continuously called by the `loop()` function \(or continuously called by a loop within another function\).

The `avoidLine()` function requires these objects as part of your global variables before the `setup()` function:

```cpp
RedBotMotors motors;
RedBotSensor leftLine(A3);
RedBotSensor centerLine(A6);
RedBotSensor rightLine(A7);
```

Add the `avoidLine()` custom function **after** the `loop()` function:

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

## countLine\(\)

A custom function named `countLine()` uses the wheel encoders to make the robot drive straight while also using the IR line sensors to count line markers the robot crosses. The robot will stop driving when it reaches a specific line number. You can then make the robot turn and start driving in a new direction.

The `countLine()` function requires two other custom functions, in order to work. Be sure to add these two functions **after** the `loop()` function:

* `driveStraight()` function — used to make the robot drive straight
* `driveDistance()` function — used to center the robot on the target line marker

Once your robot reaches a specific line marker using the `countLine()` function, you'll usually turn the robot to start driving in a new direction. Typically, you'll pivot the robot 90° right, 90° left, or 180° around. So you'll also want to add the `pivotAngle()` custom function after the `loop()` function.

The `countLine()` function requires these objects as part of your global variables before the `setup()` function:

```cpp
RedBotMotors motors;
RedBotEncoder encoder(A2, 10);
RedBotSensor leftLine(A3);
RedBotSensor centerLine(A6);
RedBotSensor rightLine(A7);
```

Add the `countLine()` custom function **after** the `loop()` function:

```cpp
void countLine(int target) {
  /* DRIVE STRAIGHT WHILE COUNTING LINES CROSSED
  Requires driveStraight() and driveDistance() functions
  
  To count dark lines on light surface:
  Use high threshold & see if sensors greater than threshold

  To count light lines on dark surface:
  Use low threshold & see if sensors less than threshold
  */

  int lineThreshold = 800; // change value if necessary

  // variables for counting lines
  int lineCount = 0;
  boolean lineDetected = false;

  // keeps looping while line count is less than target
  while (lineCount < target) {

    driveStraight();

    // get IR sensor readings
    int leftSensor = leftLine.read();
    int centerSensor = centerLine.read();
    int rightSensor = rightLine.read();

    // toggle between checking for line vs. checking for no line
    if (lineDetected == false) {
      // if all 3 sensors detect line, increase line count and toggle to checking for no line
      if (leftSensor > lineThreshold && centerSensor > lineThreshold && rightSensor > lineThreshold) {
        lineCount++;
        lineDetected = true;
      }
    }
    else if (lineDetected == true) {
      // if all 3 sensors detect no line, toggle back to checking for line
      if (leftSensor < lineThreshold && centerSensor < lineThreshold && rightSensor < lineThreshold) {
        lineDetected = false;
      }
    }
  }
  // target line count reached
  motors.brake();
  delay(250);
  driveDistance(3.5); // drive forward to center robot on target line
}
```

## followCountLine\(\)

A custom function named `followCountLine()` uses IR line sensors to make the robot follow a line while also counting line markers the robot crosses. The robot will stop driving when it reaches a specific line number. You can then make the robot turn and start following a new line.

The `followCountLine()` function requires two other custom functions, in order to work. Be sure to add these two functions **after** the `loop()` function:

* `followLine()` function — used to make the robot follow the current line
* `driveDistance()` function — used to center the robot on the target line marker

Once your robot reaches a specific line marker using the `followCountLine()` function, you'll usually turn the robot to start following a new line. Typically, you'll pivot the robot 90° right, 90° left, or 180° around. So you'll also want to add the `pivotAngle()` custom function after the `loop()` function.

The `followCountLine()` function requires these objects as part of your global variables before the `setup()` function:

```cpp
RedBotMotors motors;
RedBotEncoder encoder(A2, 10);
RedBotSensor leftLine(A3);
RedBotSensor centerLine(A6);
RedBotSensor rightLine(A7);
```

Add the `followCountLine()` custom function **after** the `loop()` function:

```cpp
void followCountLine(int target) {
  /* FOLLOW LINE WHILE COUNTING LINES CROSSED
  Requires followLine() and driveDistance() functions
  
  To follow and count dark lines on light surface:
  Use high threshold & see if sensors greater than threshold
  
  To follow and count light lines on dark surface:
  Use low threshold & see if sensors less than threshold
  */

  int lineThreshold = 800;  // change value if necessary

  // variables for counting lines
  int lineCount = 0;
  boolean lineDetected = false;

  // while line count is less than target, follow current line and count lines crossed
  while (lineCount < target) {
    followLine();
    
    // get IR sensor readings
    int leftSensor = leftLine.read();
    int centerSensor = centerLine.read();
    int rightSensor = rightLine.read();
    
    // toggle between checking for line versus checking for no line
    if (lineDetected == false) {
      // when all 3 sensors detect line, increase line count and toggle to checking for no line
      if (leftSensor > lineThreshold && centerSensor > lineThreshold && rightSensor > lineThreshold) {
        lineCount++;
        lineDetected = true;
      }
    }
    else if (lineDetected) {
      // when all 3 sensors detect no line, toggle back to checking for line
      if (leftSensor < lineThreshold && centerSensor < lineThreshold && rightSensor < lineThreshold) {
        lineDetected = false;
      }
    }
  }
  // target line count reached
  motors.brake();
  delay(250);
  driveDistance(3.5); // drive forward to center robot on target line
}
```

