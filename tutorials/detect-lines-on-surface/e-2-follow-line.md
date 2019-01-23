# E-2 Follow Line

**STILL IN PROGRESS**

Next, you'll code an app that uses the IR line sensors to make your robot follow a line. The line determines the robot's path.

## Create Line on Surface

![](../../.gitbook/assets/follow-line-diagram.png)

conditions required for accurate line following:

* line should form a closed loop \(otherwise, robot will drive off end of line and get lost\)
* line should turn using gentle curves \(no sharp turns\)
* line color should have high contrast compared to surface color:  typically you'll use a dark line \(black\) on a light surface \(white\), but you could use a light line on a dark surface
* line should be as uniform in color as possible and should be 0.25 to 0.75 inches wide
* surface must be relatively smooth \(may not work on uneven surface\)

get large sheet of paper \(such as: butcher paper, flip chart paper, etc.\), use black permanent marker \(not dry erase marker\) to draw 0.5 inch wide line that forms an oval about 3 feet in diameter

## How Line Following Works

The goal during line following is to try to keep the robot centered on the line as it drives. For this explanation, let's assume that the robot is trying to follow a dark line on a light-colored surface.

If the robot is centered on the line, the line will be under the center IR line sensor. The robot can detect this situation because the center IR line sensor will have a high reading \(dark line\) while the left and right sensors will have a low readings \(light surface\).  In order to keep following the line, the robot should drive straight to stay centered on the line.

The IR sensors can be used to make the RedBot follow a line on the surface:

* If the RedBot is **aligned with the line**, the line will be under the **center** IR sensor. The RedBot should **drive straight** to stay on the line.
* If the RedBot has started to **move off the line towards the right**, the line will under the **left** IR sensor. The RedBot should **curve slightly to the left** to get back on the line.
* If the RedBot has started to **move off the line towards the left**, the line will under the **right** IR sensor. The RedBot should **curve slightly to the right** to get back on the line.

## Save Copy of App With New Name <a id="save-copy-of-app-with-new-name"></a>

In your Arduino code editor, use the "Save As" command to save a copy of the `line_sensors_test` app as a different app named: `follow_line_test`

Once you saved the new app name, modify the block comment near the beginning of the app code to change `Line Sensors Test` to `Follow Line Test`.

## Global Variables for Motor Powers

global variables for left and right motor powers



In order to make the RedBot curve to the left or to the right, you can use different motor powers for the left and right motors. We'll use variables to keep track of each motor's power.

Add this code statement **before** your `setup()` function:

```cpp
int leftPower, rightPower;
```

This code statement actually creates two variables at the same time. You can create multiple variables of the same data type with one code statement by using a comma to separate the variable names.

## Add Custom Function to Follow Line

```cpp
void followLine() {
    /* FOLLOW LINE
    To follow dark line on light surface:
    Use high threshold & see if sensors greater than threshold

    To follow light line on dark surface:
    Use low threshold & see if sensors less than threshold
    */

    // change values if necessary
    int lineThreshold = 800;
    int power = 100;
    int powerShift = 50;

    // get IR sensor readings
    int leftSensor = leftLine.read();
    int centerSensor = centerLine.read();
    int rightSensor = rightLine.read();

    // when line under center sensor, drive straight to stay aligned
    if (centerSensor > lineThreshold) {
        // set both motors to same power
        leftPower = power;
        rightPower = power;
    }
    // when line under left sensor, turn slightly left to realign
    else if (leftSensor > lineThreshold) {
        // decrease left motor, increase right motor
        leftPower = power - powerShift;
        rightPower = power + powerShift;
    } 
    // when line under right sensor, turn slightly right to realign
    else if (rightSensor > lineThreshold) {
        // increase left motor, decrease right motor
        leftPower = power + powerShift;
        rightPower = power - powerShift;
    }

    // drive motors using power values from above
    motors.leftDrive(leftPower);
    motors.rightDrive(rightPower);

    delay(25);  // change delay to adjust line following sensitivity    
}
```

use followLine\(\) custom function - explain conceptually how it works

## Upload App to Robot

upload app to robot, and confirm it works - may need to adjust values in function \(such as: line threshold, etc.\) - test, adjust value, upload revised app, test again

