# F-1 Detect Surface Drop-Off

First, you'll code an app that allows your robot to detect a surface drop-off \(such as:  a table edge, a stair step leading down, a hole in the surface, etc.\). This will allow your robot to take actions to protect itself from a fall \(by braking, reversing, changing direction, etc.\).

A surface drop-off can be easily detected using the IR line sensors. When the front edge of the robot is hanging over a surface drop-off, the IR sensor readings will be very high \(typically 1000 or higher\).

## Save Copy of App With New Name <a id="save-copy-of-app-with-new-name"></a>

In your Arduino code editor, use the "Save As" command to save a copy of the `line_sensors_test` app as a different app named:  `detect_dropoff_test`

Once you saved the new app name, modify the block comment near the beginning of the app code to change `Line Sensors Test` to `Detect Surface Drop-off Test`.

## Create Objects for Motors and Button

Your app will need to create new objects \(as global variables\) to represent the robot's motors and button. Add this code **before** the `setup()` function:

```cpp
RedBotMotors motors;
RedBotButton button;
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

This app does **not** need the `Serial.begin()` statement within the `setup()` function. You can turn this code statement into a **comment** by typing two forward slashes `//` at the beginning of the statement.

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

Next, **delete** the code statement that calls the `testLineSensors()` function **within** the `loop()` function. This will give you an "empty" `loop()` function.

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

Later, you'll add the code to be performed when the robot is started or paused.

## Add Custom Function to Check for Surface Drop-Off

You'll add a custom function named `checkDropOff()` which will contain code to use readings from the IR line sensors to detect a surface drop-off and avoid driving over the drop-off.

Add this custom function **after** the `loop()` function:

```cpp
void checkDropOff() {

  // IR threshold indicating surface drop-off (table edge, hole, etc.)
  int dropOff = 950; // adjust value if necessary

  // get IR sensor readings
  int leftSensor = leftLine.read();
  int centerSensor = centerLine.read();
  int rightSensor = rightLine.read();

  // see if any IR sensors detect drop-off
  if (leftSensor > dropOff || centerSensor > dropOff || rightSensor > dropOff) {
    // add code to perform (brake, reverse, change direction, etc.)
    motors.brake();
    tone(speaker, 1000, 200);
    
  }
}
```

As you can see, when a drop-off is detected, the robot will brake the motors and make an alert sound. Later, you'll add more code statements to perform additional actions.

## Add Code to Perform When Robot is Started

When the D12 button is pressed to "start" the robot, we want the robot to start driving forward and checking for a surface drop-off.

Add this code statement **within** the `if` statement in the `loop()` function, so it will be performed when `started` is `true`:

```cpp
    motors.drive(150);
    checkDropOff();
```

## Add Code to Perform When Robot is Paused

Once the robot has been "started," the D12 button can be pressed again to "pause" the robot.

When the robot is "paused," we want make the robot stop driving.

Add this code statement **within** the `else` statement in the `loop()` function, so it will be performed when `started` is `false`:

```cpp
    motors.brake();
```

## Modify Custom Function to Check for Drop-Off

You'll modify the `checkDropOff()` custom function by adding code statements to perform further actions when a surface drop-off is detected.

Right now, when a drop-off is detected, the `checkDropOff()` function will brake the motors and make an alert sound.

You'll add code to also make the robot back up \(drive in reverse\).  The code will also "pause" the robot \(by changing the value of `started` back to `false`\), so you can repeat this surface drop-off test multiple times.

Add this code **within** the `if` statement in the `checkDropOff()` function, so it will be performed when the IR sensors detect a drop-off \(add this code **after** the `tone()` statement\):

```cpp
    delay(1000);
    motors.drive(-150); // back up
    delay(1000);
    motors.brake();
    started = false; // allow test to be repeated
```

## Upload App to Robot

Follow the steps to connect your robot to your computer, and upload the app.

Unplug the USB cable from the robot, and place the robot on a desk or table, so the robot is about 12 inches away from the edge of the desk \(or table\) and pointed towards the edge.

Press the D12 button to "start" the robot driving forward. When the robot detects the edge of the desk or table, the robot should stop, make an alert sound, and back up.

If you want to repeat the test, press the button to "start" the robot again.



