# C-6 Drive Straight Continuously

As your last step of this tutorial, you'll code an app that uses the wheel encoders to make your robot drive straight continuously \(rather than for a specific distance\).

Driving straight continuously is usually combined with other robot behaviors that you'll learn about in the upcoming tutorials:  detecting collisions, avoiding collisions, avoiding a line, counting lines crossed, etc.

## Create New App

Open your Arduino code editor, and create a new app template.

Add a block comment at the beginning of the app code to identify your new app:

```cpp
/*
Drive Straight Test
Team Info
Teacher - Class Period
*/
```

## Rename App

Rename the the new app as:  `drive_straight_test`

If you need a reminder, here are [instructions for how to rename an app](../../references/arduino-code-editor/save-and-rename-app.md).

## Include RedBot Library

[Follow the steps to include the SparkFun RedBot Library in your app](../../references/arduino-code-editor/include-redbot-library.md#include-redbot-library-in-app). \(You **don't** need to add the library to your code editor again — just include the library in this new app.\)

## Create Objects for Motors, Button, and Encoders

Your app will need to create new objects \(as global variables\) to represent the robot's motors, button, and wheel encoders. Add this code **before** the `setup()` function:

```cpp
RedBotMotors motors;
RedBotButton button;
RedBotEncoder encoder(A2, 10);
```

## Add Code for "Press to Start"

This app will use a **different** version of the "Press to Start" code.

Create global variables for the LED pin and speaker pin by adding this code **before** the `setup()` function:

```cpp
int LED = 13;
int speaker = 9;
```

Set the pin modes for the LED and speaker by adding this code **within** the `setup()` function:

```cpp
    pinMode(LED, OUTPUT);
    pinMode(speaker, OUTPUT);
```

In this version of the "Press to Start" code, you'll still press the D12 button to "start" the robot. However, once the robot is "started," you can press the D12 button again to "pause" the robot. \(Pressing the button yet again will "start" the robot again.\)

To do this, you'll use a global variable to keep track of whether or not the robot has been "started." Add this code statement **before** the `setup()` function:

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

## Add Custom Function to Drive Straight

You'll add another custom function named `driveStraight()` which will contain code to use the wheel encoders to make your robot drive in a continuous straight line \(as long as this function is called continuously by the `loop()` function\).

The `driveStraight()` function works similar to the `driveDistance()` function, except it **doesn't** stop the robot after a specific distance.

Add this custom function **after** the `loop()` function:

```cpp
void driveStraight() {

  // use wheel encoders to drive straight continuously

  // amount to offset motor powers to drive straight
  int offset = 5;

  // get current wheel encoder counts
  leftCount = encoder.getTicks(LEFT);
  rightCount = encoder.getTicks(RIGHT);
  
  // calculate increase in count from previous reading
  long leftDiff = leftCount - prevLeftCount;
  long rightDiff = rightCount - prevRightCount;

  // store current counts as "previous" counts for next reading
  prevLeftCount = leftCount;
  prevRightCount = rightCount;

  // adjust left & right motor powers to keep counts similar (drive straight)
  // if left rotated more than right, slow down left & speed up right
  if (leftDiff > rightDiff) {
    leftPower = leftPower - offset;
    rightPower = rightPower + offset;
  }
  // if right rotated more than left, speed up left & slow down right
  else if (leftDiff < rightDiff) {
    leftPower = leftPower + offset;
    rightPower = rightPower - offset;
  }

  // apply adjusted motor powers
  motors.leftDrive(leftPower);
  motors.rightDrive(rightPower);
  delay(10);  // short delay before next reading
}
```

## Add Global Variables for Motor Powers and Encoder Counts

The `driveStraight()` function checks to see whether the wheel encoder counts are increasing at the same rate \(by comparing how much their current counts increased from their previous counts\). If one of the wheel encoder counts is increasing at a faster rate, the function adjusts the individual motor powers to try to keep them rotating at the same rate \(which makes the robot drive straight\).

In order to do this, the `driveStraight()` function relies on global variables to track the left and right motor powers, as well as the left and right encoder counts. Add this code **before** the `setup()` function:

```cpp
// global variables needed for driveStraight() function
int leftPower = 175, rightPower = leftPower;
long prevLeftCount = 0, prevRightCount = 0;
```

## Reset Encoder Counters

You'll also want to reset both wheel encoder counters to zero when the app first starts. Add this code statement **within** the `setup()` function:

```cpp
  encoder.clearEnc(BOTH);
```

## Add Code to Perform When Robot is Started

When the D12 button is pressed to "start" the robot, we want to make the robot drive straight continuously.

Add this code **within** the `if` statement in the `loop()` function, so it will be performed when `started` is `true`:

```cpp
    driveStraight();
```

## Add Code to Perform When Robot is Paused

Once the robot has been "started," the D12 button can be pressed again to "pause" the robot.

When the robot is "paused," we want to make sure the robot stops driving.

Add this code **within** the `else` statement in the `loop()` function, so it will be performed when `started` is `false`:

```cpp
    motors.brake();
```

## Upload App to Robot

Follow the steps to connect your robot to your computer, and upload the app.

Unplug the USB cable from the robot, and place the robot on the floor. Be sure the robot has a clear path to drive forward for at least 6 feet.

Press the D12 button to "start" the robot driving in a straight line. It should keep driving in a straight line continuously, so you'll have to pick up the robot at some point and "pause" it by pressing the D12 button \(or you can press the Reset button\).

If you want to test further, place the robot on the floor, and press the button to "start" the robot again.

