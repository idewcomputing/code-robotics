# E-5 Follow and Count Lines

**STILL IN PROGRESS**

Finally, you'll code an app that uses the IR line sensors to make your robot count line markers it crosses as it follows a line. The robot will stop driving when it reaches a specific line number. You can then make the robot turn and start following a new line.

The **advantage** of counting line markers while following a line is that the robot will follow the path more reliably \(even if the robot's turns aren't perfect\), and the path doesn't necessarily have to form a closed loop. You can also create complex patterns with curved paths and intersecting paths.

The **limitation** of counting line markers while following a line is that you have to create a continuous line for each path, and different paths must intersect each other at 90° angles.

## Create Line Pattern on Surface

Your teacher might have set up one or more sets of line paths for the class to use for this tutorial.

If not, then create a set of lines and line markers on your floor or surface \(e.g., large sheet of paper, etc.\) similar to the diagram below:

INSERT DIAGRAM

* Each line or line marker should be about 0.5 inch wide.
* Any line markers along another line should be about 3-6 inches long.
* Any lines or line markers that intersect should cross at a 90° angle.

## Save Copy of App With New Name <a id="save-copy-of-app-with-new-name"></a>

In your Arduino code editor, use the "Save As" command to save a copy of the `count_lines_test` app as a different app named: `follow_count_lines_test`

Once you saved the new app name, modify the block comment near the beginning of the app code to change `Count Lines Test` to `Follow and Count Lines Test`.

## Add Custom Function to Count Lines While Following Line

You'll add a custom function named `followCountLine()` which will contain code to make your robot follow a line while using readings from the IR line sensors to count line markers that it crosses. The robot will stop when it reaches a specified line number. You can then make the robot turn and start following a new line.

Add this custom function **after** the `loop()` function:

```cpp
void followCountLine(int target) {
  /* FOLLOW LINE WHILE COUNTING LINES CROSSED
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

**IMPORTANT:**  The `followCountLine()` function requires two other custom functions, in order to work:

* `followLine()` function — used to make the robot follow the current line
* `driveDistance()` function — used to center the robot on the target line marker

So your app will also need to have both of these custom functions. Luckily, the saved app that you re-used for this current app already has the `driveDistance()` function.

Furthermore, once your robot reaches a specific line marker using the `followCountLine()` function, you'll usually turn the robot to start following a new line. Typically, you'll pivot the robot 90° right, 90° left, or 180° around.

So you'll also want to have the `pivotAngle()` custom function, which contains code to make your robot pivot by a specified angle by using the wheel encoders. Luckily, the saved app that you re-used for this current app already has the `pivotAngle()` function.

## Add Custom Function to Follow Line

Copy the `followLine()` function from [tutorial E-2](e-2-follow-line.md#add-custom-function-to-follow-line), and add this function **after** the `loop()` function.

## Modify Code to Perform When Robot is Started

When the D12 button is pressed to "start" the robot, we want to make the robot follow the current line until it has counted X line markers. Then we'll make the robot ... ADD DESCRIPTION

First, **delete** the existing code statement **within** the `if` statement in the `loop()` function that are performed when `started` is `true`.

Then add these code statements **within** the `if` statement in the `loop()` function, so they will be performed when `started` is `true`:

```cpp
// code to be added
```

## Upload App to Robot

Follow the steps to connect your robot to your computer, and upload the app.

Unplug the USB cable from the robot, and place the robot on the main line with the robot's IR line sensors in **front** of the "start" line marker \(so it will **not** be counted as the first line marker\).

INSERT DIAGRAM

Press the D12 button to "start" the robot. The robot should start following the line. After the robot has counted X line markers \(meaning it has reached the X line after the start line\), the robot should...ADD DESCRIPTION

If you want to test the robot again, press the D12 button to "start" the robot again.

As further practice, you could modify the app to make the robot drive in different patterns using this same set of lines and line markers.

