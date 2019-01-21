# D-4 Avoid Collisions

**STILL IN PROGRESS**

As your last step of this tutorial, you'll code an app to make your robot drive and avoid collisions using its ultrasonic sensor.

## Save Copy of App With New Name <a id="save-copy-of-app-with-new-name"></a>

In your Arduino code editor, use the "Save As" command to save a copy of the `ultrasonic_sensor_test` app as a different app named: `avoid_collisions_test`

Once you saved the new app name, modify the block comment near the beginning of the app code to change `Ultrasonic Sensor Test` to `Avoid Collisions Test`.

## Add Custom Function to Avoid Collisions

use avoidCollisions\(\) custom function - need to add code

can modify code to perform other actions, such as trying to navigate around the object \(include diagram showing possible path\) - or checking both left and right for possible open path

## Upload App to Robot

Follow the steps to connect your robot to your computer, and upload the app.

Unplug the USB cable from the robot, and place the robot on the floor.

Press the D12 button to "start" the robot driving forward. You can use your leg as an obstacle in the robot's path. When the robot detects that it is too close to an obstacle, the robot should stop, back up, and then turn 90° right or left.

When you're done testing the robot, you can pick it up, and press the D12 button to "pause" the robot.

If you want to test further, place the robot on the floor, and press the button to "start" the robot again.

