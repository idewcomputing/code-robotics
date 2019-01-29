# F-3 Detect If Upside-Down

Next, you'll code an app that uses the accelerometer to detect if the robot is upside-down by measuring its pitch and roll. If the robot is upside-down, it will stop its motors and make a distress sound.

## Create New App

Open your Arduino code editor, and create a new app template.

Add a block comment at the beginning of the app code to identify your new app:

```cpp
/*
Detect Upside-Down Test
Team Info
Teacher - Class Period
*/
```

## Rename App

Rename the the new app as:  `upside_down_test`

If you need a reminder, here are [instructions for how to rename an app](../../references/arduino-code-editor/save-and-rename-app.md).

## Include RedBot Library

[Follow the steps to include the SparkFun RedBot Library in your app](../../references/arduino-code-editor/include-redbot-library.md#include-redbot-library-in-app). \(You **don't** need to add the library to your code editor again — just include the library in this new app.\)

## Create Objects for Motors, Button, and Accelerometer

Your app will need to create new objects \(as global variables\) to represent the robot's motors, button, and accelerometer. Add this code **before** the `setup()` function:

```cpp
RedBotMotors motors;
RedBotButton button;
RedBotAccel accel;
```

## Add Code for "Press to Start"

This app will use the "Press to Start" code. You'll press the D12 button to "start" the robot. Once the robot is "started," you can press the button again to "pause" the robot. \(Pressing the button yet again will "start" the robot again.\)

You need to declare global variables for the LED  pin and speaker pin. You also need a global variable to keep track of whether or not the robot has been "started."  Add this code **before** the `setup()` function:

```cpp
int LED = 13;
int speaker = 9;
bool started = false;
```

Set the pin modes for the LED and speaker by adding this code **within** the `setup()` function:

```cpp
    pinMode(LED, OUTPUT);
    pinMode(speaker, OUTPUT);
```

Next, you need to add the custom function named `checkButton()` that will check whether the D12 button is pressed, in order to "start" or "pause" the robot.

Add this custom function **after** the `loop()` function:

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

Now add this code **within** the `loop()` function:

```cpp
  checkButton();
  if (started == true) {
    // add code to perform when "started"
    
  }
  else {
    // add code to perform when "paused"
    
  }
```

Later, you'll add the code to be performed when the robot is started or paused.

## Add Custom Function to Check If Robot Upside-Down

You'll add a custom function named `checkUpsideDown()` which will contain code to use readings from the accelerometer to detect when the robot's pitch or roll is greater than 90° \(which indicates the robot has flipped over\).

The function will use the [absolute value](https://www.arduino.cc/reference/en/language/functions/math/abs/) for pitch and roll because 90° and -90° both indicate the robot is about to tip over.

This custom function will return a [boolean](https://www.arduino.cc/reference/en/language/variables/data-types/bool/) value when it is called:

* If the robot's pitch or roll is greater than 90 degrees, the function returns a value of `true`
* Otherwise, the function returns a value of `false`

Add this custom function **after** the `loop()` function:

```cpp
bool checkUpsideDown() {
  // if robot is upside-down, returns value of true
  // otherwise returns value of false

  // get new accelerometer data
  accel.read(); 

  // get absolute values for pitch and roll
  float pitch = abs(accel.angleXZ);
  float roll = abs(accel.angleYZ);

  // see if pitch or roll is greater than 90 degrees & return value
  if (pitch > 90 || roll > 90) return true;
  else return false;
}
```

Functions that do **not** return a value have `void` listed as the data type before the function's name.

If a function **does** return a value when called, the data type of the returned value must be listed before the function's name.

In this case, `bool` is listed before the `checkUpsideDown()` function's name because the function will return a value of either `true` or `false`.

## Add Code to Perform When Robot is Started

When the D12 button is pressed to "start" the robot, we want the robot to check whether it is upside-down by calling the `checkUpsideDown()` function and then performing appropriate actions based on the result:

* If the robot is upside-down, it should brake its motors and make a distress sound.
* Otherwise, the robot should drive forward.

The boolean value returned by the `checkUpsideDown()` function will be stored in a local variable named `upsideDown`.

Add this code **within** the `if` statement in the `loop()` function, so it will be performed when `started` is `true`:

```cpp
    bool upsideDown = checkUpsideDown();
    if (upsideDown == true) {
      // add code to perform special actions: brake, distress signal, etc.
        motors.brake();
        tone(speaker, 4000, 200);
        delay(400);
    }
    else {
        // add code to perform normal actions: drive, turn, etc.
        motors.drive(100);
    }
```

## Add Code to Perform When Robot is Paused

Once the robot has been "started," the D12 button can be pressed again to "pause" the robot.

When the robot is "paused," we want make the robot stop driving.

Add this code statement **within** the `else` statement in the `loop()` function, so it will be performed when `started` is `false`:

```cpp
    motors.brake();
```

## Upload App to Robot

Follow the steps to connect your robot to your computer, and upload the app.

Unplug the USB cable from the robot, and hold the robot in the air with both hands.

Press the D12 button to "start" the robot. Its motors will start as it "drives" forward.

Simulate the robot flipping upside-down by rotating it until the pitch \(front-to-back tilt\) or roll \(side-to-side tilt\) is greater than 90° in any direction. The robot should brake its motors and make a distress sound.

Then rotate the robot back to a "normal" position \(where its pitch and roll are less than 90°\). The distress sound should stop, and the motors should start again.

You can press the D12 button to "pause" the robot. If you want to repeat the test, press the button to "start" the robot again.

