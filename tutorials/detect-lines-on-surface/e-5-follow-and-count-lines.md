# E-5 Follow and Count Lines

Finally, you'll code an app that uses the IR line sensors to make your robot count line markers it crosses as it follows a line. The robot will stop driving when it reaches a specific line number. You can then make the robot turn and start following a new line.

The **advantage** of counting line markers while following a line is that the robot will follow the path more reliably \(even if the robot's turns aren't perfect\), and the path doesn't necessarily have to form a closed loop. You can also create complex patterns with straight paths, curved paths, and loops.

The **limitation** of counting line markers while following a line is that you have to create a continuous line for each path, and different paths must intersect each other at 90° angles.

## Create Line Pattern on Surface

Your teacher might have set up one or more sets of line paths for the class to use for this tutorial.

If not, then create a set of lines and line markers on your floor or surface \(e.g., large sheet of paper, etc.\) similar to the diagram below, which represents an area about 3 feet by 4 feet in size.

{% hint style="success" %}
**REUSE LINE PATH:**  If you still have the line path that was created in [tutorial E-2](e-2-follow-line.md#create-line-on-surface), you could modify it by adding lines to match the diagram below.
{% endhint %}

![](../../.gitbook/assets/follow-count-line-diagram1.png)

* Each line or line marker should be about 0.5—0.75 inch wide.
* Any line markers that intersect another line should be about 4—6 inches long.
* Any lines or line markers that intersect should cross at a 90° angle.

## Save Copy of App With New Name <a id="save-copy-of-app-with-new-name"></a>

In your Arduino code editor, use the "Save As" command to save a copy of the `follow_line_test` app as a different app named: `follow_count_lines_test`

Once you saved the new app name, modify the block comment near the beginning of the app code to change `Follow Line Test` to `Follow and Count Lines Test`.

## Add Custom Function to Count Lines While Following Line

You'll add a custom function named `followCountLine()` which will contain code to make your robot follow a line while using readings from the IR line sensors to count line markers that it crosses. The robot will stop when it reaches a specified line number. You can then make the robot turn and start following a new line.

Add this custom function **after** the `loop()` function:

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

**IMPORTANT:**  The `followCountLine()` function requires two other custom functions, in order to work:

* `followLine()` function — used to make the robot follow the current line
* `driveDistance()` function — used to center the robot on the target line marker

So your app will also need to have both of these custom functions. Luckily, the saved app that you re-used for this current app already has the `followLine()` function.

## Add Custom Function to Drive Specific Distance

The `followCountLine()` function calls the `driveDistance()` function once the target line count is reached. The robot drives forward 3.5 inches, in order to center the robot's wheels on the target line marker.

So you'll need to add the `driveDistance()` custom function, which contains code to make your robot drive in a straight line for a specified distance by using the wheel encoders.

Copy the `driveDistance()` function from [tutorial C-4](../driving-and-turning/c-4-drive-for-specific-distance.md#add-custom-function-to-drive-specific-distance) \(use your browser's back button to return this page after copying\), and add the function **after** the `loop()` function.

## Add Custom Function to Pivot Specific Angle

Once your robot reaches a specific line marker using the `followCountLine()` function, you'll usually turn the robot to start following a new line. Typically, you'll pivot the robot 90° right, 90° left, or 180° around.

So you'll also need to add the `pivotAngle()` custom function, which contains code to make your robot pivot by a specified angle by using the wheel encoders.

Copy the `pivotAngle()` function from [tutorial C-5](../driving-and-turning/c-5-pivot-by-specific-angle.md#add-custom-function-to-pivot-specific-angle) \(use your browser's back button to return to this page after copying\), and add the function **after** the `loop()` function.

## Create Object for Encoders

Your app will need to create a new object \(as a global variable\) to represent the robot's wheel encoders, which are used by the `driveDistance()` and `pivotAngle()` functions.

Add this code statement **before** the `setup()` function:

```cpp
RedBotEncoder encoder(A2, 10);
```

## Modify Code to Perform When Robot is Started

The robot will start on the inner line inside the loop. When the D12 button is pressed to "start" the robot, we want to make the robot follow the current line until it has counted 1 line marker \(i.e., reached marker A in the diagram\). Then we'll make the robot turn 90° right and follow the outer loop line until it has counted 4 line markers \(which will bring it back to marker A\). Then the robot will turn 90° right again, and follow the inner line until it has counted 1 line marker \(i.e., returned to the start\). Finally, the robot will turn around \(180°\) and "pause" itself, so it's back in its starting position.

![](../../.gitbook/assets/follow-count-line-diagram2.png)

First, **delete** the existing code statement **within** the `if` statement in the `loop()` function that calls the `followLine()` function  when `started` is `true`.

Then add these code statements **within** the `if` statement in the `loop()` function, so they will be performed when `started` is `true`:

```cpp
    followCountLine(1); // follow line until 1 line marker counted
    pivotAngle(90); // turn right
    followCountLine(4); // follow line until 4 line markers counted
    pivotAngle(90); // turn right
    followCountLine(1); // follow line until 1 line marker counted
    pivotAngle(180); // turn around
    started = false; // pause robot
```

## Upload App to Robot

Follow the steps to connect your robot to your computer, and upload the app.

Unplug the USB cable from the robot, and place the robot on the inner line with the robot's IR line sensors in **front** of the "start" line marker \(so it will **not** be counted as the first line marker\).

Press the D12 button to "start" the robot. The robot should follow the inner line. After the robot has reached the outer line, the robot should turn right and follow the outer line clockwise around one complete loop before turning right and returning to its starting position.

If you want to test the robot again, press the D12 button to "start" the robot again.

As further practice, you could modify the app to make the robot drive in different patterns using this same set of lines and line markers. For example, you could try to make the robot drive from the "start" line to line marker A, then turn left and drive to line marker D, then turn around \(180°\) and return to the start.

