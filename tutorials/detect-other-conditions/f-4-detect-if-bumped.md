# F-4 Detect If Bumped

Finally, you'll code an app that uses the accelerometer to detect when the robot has been bumped \(e.g., by colliding with another object, etc.\). If the robot is bumped, it will stop its motors and make an alert sound.

## Save Copy of App With New Name <a id="save-copy-of-app-with-new-name"></a>

In your Arduino code editor, use the "Save As" command to save a copy of the `upside_down_test` app as a different app named:  `detect_bump_test`

Once you saved the new app name, modify the block comment near the beginning of the app code to change `Detect Upside-Down Test` to `Detect Bump Test`.

## Start Bump Detection

The `RedBotAccel` class defines a method named `checkBump()` that can detect whether the robot has been physically bumped as the result of a collision or other force.

However, your app must first enable bump detection by using another method named `enableBump()` which is also defined in the `RedBotAccel` class. This is only required one-time.

To enable bump detection, add this code statement **within** the `setup()` function:

```cpp
accel.enableBump();
```

## Modify Code to Perform When Robot is Started

Your app can check for a "bump" using the `RedBotAccel` object's `checkBump()` method, which will return a value of `true` or `false` based on whether or not a physical bump was detected.

The `checkBump()` method can detect a bump from any direction on the robot's body \(front, back, left, right, top, or bottom\) — but it **won't** tell you which specific direction the bump came from.

When the D12 button is pressed to "start" the robot, we want the robot to check whether it has been bumped by using the `checkBump()` method and then performing appropriate actions based on the result:

* If the robot has been bumped, it should brake its motors, make an alert sound, and "pause" itself.
* Otherwise, the robot should drive forward.

The boolean value returned by the `checkBump()` method will be stored in a local variable named `bump`.

First, **delete** the existing code statements **within** the `if` statement in the `loop()` function that are performed when `started` is `true`

Next, add this code **within** the `if` statement in the `loop()` function, so it will be performed when `started` is `true`:

```cpp
    bool bump = accel.checkBump();
    if (bump == true) {
      // add code to perform special actions: brake, distress signal, etc.
        motors.brake();
        // triple beep
        for (int i=0; i < 3; i++) {
          tone(speaker, 4000, 100);
          delay(200);
        }
        started = false; // pause until button pressed again
    }
    else {
        // add code to perform normal actions: drive, turn, etc.
        motors.drive(100);
    }
```

## Upload App to Robot

Follow the steps to connect your robot to your computer, and upload the app.

Unplug the USB cable from the robot, and place the robot on the floor.

Press the D12 button to "start" the robot driving forward. You can use your hand to tap the front of the robot. When a bump is detected, the robot should stop, make an alert sound, and then pause itself.

Press the button again, and then tap on another part of the robot's chassis \(side, back, etc.\). You can repeat to test other bumps to the robot.

When you're done testing the robot, you can turn off its power.





