# C-2 Turns \(Pivoting\)

Next, you'll code an app to make your robot turn 90° right. Then you'll modify the app so the robot turns 90° left and turns 180° around.

## Save Copy of App With New Name

In your Arduino code editor, use the "Save As" command to save a copy of your existing `driving_test` app as a different app named:  `pivot_test`

If necessary, here are [instructions for how to save a copy of an app with a new name](../../references/arduino-code-editor/save-and-rename-app.md).

Once you saved the new app name, modify the block comment near the beginning of the app code to change `Driving Test` to `Pivot Test`.

## Turn Right

The most common types of turns needed for robot navigation are:  turn 90° right, turn 90° left, and turn 180° around.

The `RedBotMotors` class defines a method named `pivot()` that can be used to turn the robot either clockwise or counter-counterclockwise. The `pivot()` method turns the robot by driving both motors in opposite directions.

There are other ways to turn your robot, but the `pivot()` method results in a perfectly tight turn because the robot's axis of rotation is centered between its wheels. Pivoting is the best way to turn the robot when space is limited \(as it will be in your robot demonstration environment\).

When the `motors.pivot()` method is used in your code, the motors will start and will keep pivoting continuously. You'll use a `delay()` statement to allow the motors to pivot for a certain amount of time before turning the motors off with the `motors.brake()` method.

First, modify the "Push to Start" code **within** the `if` statement in the `loop()` function to **remove** the existing code statements that make the robot drive forward and then backward.

Next, you'll add new code so that when the robot's button is pressed, the robot will drive forward for 1.5 seconds \(about 2 feet\), turn 90° right, and then drive forward for another 1.5 seconds. Add this new code **within** the `if` statement in the `loop()` function \(**after** the `noTone()` statement\):

```cpp
    motors.drive(200);
    delay(1500);
    motors.brake();

    motors.pivot(100);
    delay(650);
    motors.brake();

    motors.drive(200);
    delay(1500);
    motors.brake();
```

The `motors.pivot()` method requires one parameter inside its parentheses:

* **The motor power**, which can be any integer \(whole number\) between `-255` and `255`. A positive power pivots the robot clockwise \(to the right\), and a negative power pivots the robot counter-clockwise \(to the left\). A larger absolute power produces a faster pivot speed \(`-255` and `255` are the fastest speeds, while `-1` and `1` are the slowest speeds\). In this case, the power will be `100`.

{% hint style="success" %}
**PIVOT SLOWLY:**  You should pivot the robot at a lower power to avoid wheel slippage. In general, try using a power of 100 for pivoting \(though you may need to adjust this value depending on whether the floor surface is hard or soft, such as tile vs. carpet\).
{% endhint %}

The second `delay()` of `650` milliseconds \(0.65 seconds\) is an estimate of how much time it will take your robot to pivot 90 degrees. You may have to change this value after testing your robot.

## Upload App to Robot

[Follow the steps to upload the app to your robot](../../references/arduino-code-editor/upload-app-to-robot.md):

1. Connect Robot to Computer
2. Turn on Robot Power
3. Select Correct Board and Port
4. Upload App to Robot

Unplug the USB cable from the robot, and place the robot on the floor. Be sure an area of about 3 feet square in front and to the right of the robot is clear of any obstacles.

* Press the D12 button on your robot's circuit board. Your robot should beep and then drive forward for 1.5 seconds \(about 22 inches\). Then the robot should pivot 90° right, and then drive forward for another 1.5 seconds \(about 22 inches\).

Test out your robot's app several times to see how close the pivot is to a 90° right turn.

In the app code, the second `delay()` of `650` milliseconds \(0.65 seconds\) is an estimate of how much time it will take your robot to pivot 90 degrees. You may have to change this value based on your testing:

* If your robot is pivoting **less** than 90°, **increase** the pivot `delay()` time slightly \(such as: `700` ms\).
* If your robot is pivoting **more** than 90°, **decrease** the pivot `delay()` time slightly \(such as: `600` ms\).

If you do change the pivot `delay()` time, upload the modified app to your robot, and test it again with the new value. You may need to change the value several times to fine-tune your results.

Later in this tutorial, you'll learn how to use the wheel encoders to measure how far the wheels have turned, in order to make the robot pivot by a specific angle.

## Turn Left

Next, you'll modify the app code so your robot will pivot 90° left.  To do this, you simply need to make the robot pivot **counter-clockwise** by using a **negative** motor power.

Modify the `motors.pivot()` statement so the motor power is `-100` \(instead of positive\).

You don't need to change the pivot `delay()` time because the amount of time to pivot 90 degrees should be the same whether the robot is pivoting clockwise \(to the right\) or counter-clockwise \(to the left\).

Upload the modified app to your robot.

Unplug the USB cable from the robot, and place the robot on the floor. Be sure an area of about 3 feet square in front and to the left of the robot is clear of any obstacles.

* Press the D12 button on your robot's circuit board. Your robot should beep and then drive forward for 1.5 seconds \(about 22 inches\). Then the robot should pivot 90° left, and then drive forward for another 1.5 seconds \(about 22 inches\).

Test out your robot's app several times to see how close the pivot is to a 90° left turn.

## Turn Around

Next, you'll modify the app code so your robot will pivot 180° to turn around. To do this, you simply need to allow the robot to pivot for twice the amount of time as a 90° pivot.

For a 180° turn, it doesn't matter if the robot pivots clockwise or counter-clockwise. So you can either leave the motor power in the `motors.pivot()` statement as `-100` \(counter-clockwise\) — or you can change the power back to `100` \(clockwise\).

Modify the pivot `delay()` time so its value is **twice** the amount that was needed for a 90° turn. For example, if the time required for a 90° turn was `650` milliseconds, try `1300` ms for a 180° turn.

Upload the modified app to your robot.

Unplug the USB cable from the robot, and place the robot on the floor. Be sure a path of about 3 feet in front of the robot is clear of any obstacles.

* Press the D12 button on your robot's circuit board. Your robot should beep and then drive forward for 1.5 seconds \(about 22 inches\). Then the robot should pivot 180° around, and then drive forward for another 1.5 seconds \(about 22 inches\), returning approximately to its starting point.

Test out your robot's app several times to see how close the pivot is to a 180° turn. You may have to adjust the pivot `delay()` time in the app code, and re-upload the app to test again.

