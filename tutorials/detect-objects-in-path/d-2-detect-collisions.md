# D-2 Detect Collisions

Next, you'll code an app to make your robot drive around and detect collisions using its mechanical bumpers.

## Save Copy of App With New Name <a id="save-copy-of-app-with-new-name"></a>

In your Arduino code editor, use the "Save As" command to save a copy of the `mechanical_bumper_test` app as a different app named: `detect_collisions_test`

Once you saved the new app name, modify the block comment near the beginning of the app code to change `Mechanical Bumper Test` to `Detect Collisions Test`.

## Add Code for "Press to Start"

This app will use a **different** version of the "Press to Start" code.

You'll press the D12 button to "start" the robot. Once the robot is "started," you can press the button again to "pause" the robot. \(Pressing the button yet again will "start" the robot again.\)

You'll use a global variable to keep track of whether or not the robot has been "started." Add this code statement **before** the `setup()` function:

```cpp
bool started = false;
```

This code statement does three things \(in order\):

1. **It declares a data type for the variable's value.**  In this case, `bool` stands for boolean. A boolean value can either be `true` or `false`.  In this case, `true` will mean the robot is "started," and `false` will mean the robot is "paused."
2. **It declares the variable's name.** In this case, the variable will be called `started`. You get to decide what to name your variables. Choose names that will make sense to anyone reviewing your code.
3. **It assigns a value to the variable.**  In this case, the variable's initial value will be equal to `false` because we don't want to "start" the robot until the D12 button is pressed.

Next, you'll add a custom function named `checkButton()` that will check whether the D12 button is pressed. If the button is pressed, the function will reverse the current value of `started` from `true` to `false` \(or from `false` to `true`\).

Add this custom function **after** the `loop()` function \(i.e., after its closing curly brace\):

```cpp
void checkButton() {
  if (button.read() == true) {
    // reverse value of started
    started = !started;
    
    // beep and blink as feedback
    digitalWrite(LED, HIGH);
    tone(speaker, 2000);
    delay(200);
    digitalWrite(LED, LOW);
    noTone(speaker);
    delay(200);
  }
}
```

The code statement that reverses the value of `started` is:  `started = !started;`

This code statement works by assigning a new value to `started` that is equal to its opposite value. For a boolean variable, listing an **exclamation point** in front of the variable name represents its opposite value. So if `started` currently has a value of `true`, it will be assigned a new value of `false` \(or vice versa\).

Next, **delete** the code statement that calls the `checkBumpers()` function **within** the `loop()` function. This will give you an "empty" `loop()` function.

Now add this new code **within** the `loop()` function:

```cpp
  checkButton();
  if (started == true) {
    // add code to perform when "started"
    
  }
  else {
    // add code to perform when "paused"
    
  }
```

As you can see, this code will call the `checkButton()` function. Then it uses an if-else statement to perform different code \(not added yet\) depending on whether `started` is `true` or `false`.

## Add Code to Perform When Robot is Started

When the D12 button is pressed to "start" the robot, we want to make the robot drive forward continuously and also check for any bumper collisions.

Add this code **within** the `if` statement in the `loop()` function, so it will be performed when `started` is `true`:

```cpp
    motors.drive(150);
    checkBumpers();
```

## Add Code to Perform When Robot is Paused

Once the robot has been "started," the D12 button can be pressed again to "pause" the robot.

When the robot is "paused," we want to make sure the robot stops driving.

Add this code **within** the `else` statement in the `loop()` function, so it will be performed when `started` is `false`:

```cpp
    motors.brake();
```

## Modify Custom Function to Check Bumpers

You'll modify the `checkBumpers()` custom function by adding code statements to perform further actions when a bumper collision occurs.

Right now, when a bumper collision is detected, the `checkBumpers()` function will brake the motors and make a sound.

You'll add code to also make the robot back up \(drive in reverse for 12 inches\) and then turn right or left \(pivot 90°\) depending on whether the left or right bumper detected a collision.

Add this code **within** the `if` statement in the `checkBumpers()` function, so it will be performed when the **left bumper** detects a collision \(add this code **after** the `tone()` statement\):

```cpp
    delay(1000);
    driveDistance(-12); // back up
    pivotAngle(90); // turn right
```

Add this code **within** the `else if` statement in the `checkBumpers()` function, so it will be performed when the **right bumper** detects a collision \(add this code **after** the `tone()` statement\):

```cpp
    delay(1000);
    driveDistance(-12); // back up
    pivotAngle(-90); // turn left
```

## Upload App to Robot

Follow the steps to connect your robot to your computer, and upload the app.

Unplug the USB cable from the robot, and place the robot on the floor.

Press the D12 button to "start" the robot driving forward. You can use your hand as an obstacle to create collisions with the wire whiskers. When a collision is detected, the robot should stop, back up, and then turn 90° right or left \(depending on which bumper detected the collision\).

When you're done testing the robot, you can pick it up, and press the D12 button to "pause" the robot.

If you want to test further, place the robot on the floor, and press the button to "start" the robot again.

