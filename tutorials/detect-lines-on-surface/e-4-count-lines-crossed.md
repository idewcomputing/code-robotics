# E-4 Count Lines Crossed

**STILL IN PROGRESS**

Next, you'll code an app that uses the IR line sensors to make your robot count line markers it crosses as it drives straight. The robot will stop driving when it reaches a specific line number. You can then make the robot turn and start driving in a new direction.

## Create Line Markers on Surface

get large sheet of paper \(such as: butcher paper, flip chart paper, etc.\), use black permanent marker \(not dry erase marker\) to draw 0.5 inch wide lines that form pattern shown in diagram \(main path with two side paths\)

![](../../.gitbook/assets/count-line-diagram1.png)

## Save Copy of App With New Name <a id="save-copy-of-app-with-new-name"></a>

In your Arduino code editor, use the "Save As" command to save a copy of the `drive_straight_test` app as a different app named: `count_lines_test`

Once you saved the new app name, modify the block comment near the beginning of the app code to change `Drive Straight Test` to `Count Lines Test`.

## Create Objects for Line Sensors

Your app will need to create new objects \(as global variables\) to represent the robot's IR line sensors. Add this code **before** the `setup()` function:

```cpp
RedBotSensor leftLine(A3);
RedBotSensor centerLine(A6);
RedBotSensor rightLine(A7);
```

## Add Custom Function to Count Lines

You'll add a custom function named `countLine()` which will contain code to make your robot drive straight continuously while using readings from the IR line sensors to count each line marker that it crosses. The robot will stop when it reaches a specified line number.

Add this custom function **after** the `loop()` function:

```cpp
void countLine(int target) {
  /* COUNT LINES
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

use countLine\(\) custom function - explain conceptually how it works

also need driveStraight\(\) - plus global variables for left and right motor powers and previous left and right wheel encoder counts - used to make robot drive straight continuously while it counts lines crossed

also need driveDistance\(\) function - used to align center of robot with target line number

upload app to robot, and confirm it works - may need to adjust values in function \(such as: line threshold, etc.\) - test, adjust value, upload revised app, test again

modify pattern & app

![](../../.gitbook/assets/count-line-diagram2.png)

