# Detecting Other Conditions

These custom functions use the [push button](../physical-inputs/push-button.md), [IR line sensors](../physical-inputs/ir-line-sensors.md), or [accelerometer](../physical-inputs/accelerometer.md):

* `checkButton()` — check if button is pressed in order to "start" or "pause" robot
* `pauseRobot()` — pause until button is pressed before performing next step in task
* `checkDropOff()` — check for surface drop-off \(e.g., stair step, etc.\)
* `checkUpsideDown()` — check if robot is upside down \(pitch or roll greater than 90°\)
* `checkBump()` — check if robot has been bumped

You can also use the `millis()` method as a clock to set a timer for a `while()` loop to perform a continuous task \(such as:  avoiding a line, etc.\) for a certain duration of time.

## while\(\) loop timer

You can make your robot perform a task for a certain duration of time, similar to setting a timer. This is useful for behaviors that need to be continuously called within a loop \(such as:  drive straight, check bumpers, avoid collision, avoid line, check drop-off, etc.\) and don't have a distinct stopping point.

Arduino has a `millis()` method which acts like a clock. It keeps track of how many milliseconds have passed since your robot app first started running. The timer duration is used to set an end time for the task.

A `while()` loop is used to perform the task continuously until the timer runs out \(i.e., until the current time exceeds the end time\). In this example code, the timer is set for 30 seconds, but you can change the timer to whatever duration you need.

Add this code **within** another custom function, such as `task1()`, etc.

```cpp
  // get current time (in milliseconds)
  unsigned long time = millis();
  
  // set end time (in milliseconds)
  unsigned long duration = 30000; // change if necessary
  unsigned long endTime = time + duration;

  // while current time is less than end time, loop performs task
  while (time < endTime) {
    // add code to perform continuous task (avoid line, etc.)
    
    
    time = millis(); // check current time again
  }
  // time's up
  motors.stop();
```

{% hint style="success" %}
**ADD CODE TO WHILE LOOP:**  You need to add code statement\(s\) within the `while()` loop to perform the continuous task\(s\).
{% endhint %}

## checkButton\(\)

A custom function named `checkButton()` checks whether the built-in D12 button is being pressed. If the button is pressed, the function will toggle the value of a global variable named `started` from `false` to `true` \(or vice versa\). The function will also provide feedback by blinking the built-in D13 LED light and producing a beep with the speaker.

The `checkButton()` function uses a `RedBotButton` object to read the button. Create this object as part of your global variables **before** the `setup()` function:

```cpp
RedBotButton button;
```

The `checkButton()` function uses global variables that store the pin numbers for the LED and speaker and that track whether the robot is "started" \(`true`\) or "paused" \(`false`\). Add this code **before** the `setup()` function:

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

Add the `checkButton()` custom function **after** the `loop()` function:

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

You can add this code **within** the `loop()` function to perform different actions based on whether the robot is "started" \(`started == true`\) or "paused":

```cpp
  checkButton();
  if (started == true) {
    // add code to perform when "started"
    
  }
  else {
    // add code to perform when "paused"
    
  }
```

{% hint style="success" %}
**ADD CODE:**  You need to add code to perform different actions based on whether the robot is "started" \(e.g., drive, etc.\) or "paused" \(e.g., stop motors, etc.\).
{% endhint %}

{% hint style="info" %}
**ONE BUTTON LIBRARY:**  Another option is to [use the OneButton library](../physical-inputs/push-button.md#use-onebutton-object) to detect different types of button presses \(single-press, double-press, or long-press\).
{% endhint %}

## pauseRobot\(\)

A custom function named `pauseRobot()` can be used to add "pauses" in a robot's task. The robot will wait until the built-in D12 button is pressed before performing the next step in the task. This could be useful in a robot task demonstration.

For example, you could add a "pause" for a simulated step in a task. The robot will "pause" while you complete or explain the simulated step. Once you press the button, the robot will continue with the next step in the task.

This "pause" is created using a `while()` loop that keeps repeating itself until the button is pressed. The `while()` loop contains a short delay before it checks the button again.

The `pauseRobot()` function uses a `RedBotButton` object to read the button. Create this object as part of your global variables **before** the `setup()` function:

```cpp
RedBotButton button;
```

The `pauseRobot()` function will produce a "beep" as an alert when the robot is paused and produce another beep as feedback once the button is pressed. This uses a global variable that stores the pin number for the speaker. Add this code **before** the `setup()` function:

```cpp
int speaker = 9;
```

Set the pin mode for the speaker by adding this code **within** the `setup()` function:

```cpp
pinMode(speaker, OUTPUT);
```

Add the `pauseRobot()` custom function **after** the `loop()` function:

```cpp
void pauseRobot() {
  motors.stop(); // make sure robot is stopped
  tone(speaker, 2000, 200); // beep as alert
  while (button.read() == false) delay(10); // wait until button pressed
  tone(speaker, 2000, 200); // beep as feedback
  delay(200); // allow button to be released
}
```

Then you can call the `pauseRobot()` function within the `loop()` function or within a custom function whenever you want the robot to pause its task until the button is pressed.

For example, the code below shows how the `pauseRobot()` function could be used within a task to add a "pause" for a simulated step. The robot will pause until the button is pressed.

```cpp
// drive to destination
driveDistance(36);
pivotAngle(90);
driveDistance(24);

// pause for simulated step
pauseRobot();

// drive back to start
pivotAngle(180);
driveDistance(24);
pivotAngle(-90);
driveDistance(36);
```

## checkDropOff\(\)

A custom function named `checkDropOff()` uses the IR sensors to allow your robot to detect a surface drop-off \(such as:  the edge of a table, a stair step leading down, a hole in the surface, etc.\).

Even a small increase in the distance between the IR sensors and the surface \(as little as 0.25 inch\) will greatly reduce the amount of reflected IR light that is detected.

When a surface drop-off is detected, the motors will be braked. You can add code to perform additional actions \(such as backing up, changing direction, etc.\).

In order to work, the `checkDropOff()` function must be continuously called by the `loop()` function \(or continuously called by a loop within another function\).

The `checkDropOff()` function requires these objects as part of your global variables **before** the `setup()` function:

```cpp
RedBotMotors motors;
RedBotSensor leftLine(A3);
RedBotSensor centerLine(A6);
RedBotSensor rightLine(A7);
```

Add the `checkDropOff()` custom function **after** the `loop()` function:

```cpp
void checkDropOff() {

  // IR threshold indicating drop-off (table edge, hole, etc.)
  int dropOff = 950; // adjust value if necessary

  // get IR sensor readings
  int leftSensor = leftLine.read();
  int centerSensor = centerLine.read();
  int rightSensor = rightLine.read();

  // see if any IR sensors detect drop-off
  if (leftSensor > dropOff || centerSensor > dropOff || rightSensor > dropOff) {
    // add code to perform (brake, reverse, change direction, etc.)
    motors.brake();
    
  }
}
```

{% hint style="success" %}
**ADD CODE TO FUNCTION:**  You need to add code within the `checkDropOff()` function to perform actions \(brake, back up, etc.\) when a drop-off is detected.
{% endhint %}

## checkUpsideDown\(\)

A custom function named `checkUpsideDown()` uses the accelerometer to detect whether the robot's pitch or roll is greater than 90° \(which indicates the robot has flipped over\).

When the `checkUpsideDown()` function is called, it will return a `bool` value \(boolean\) of either `true` or `false`. Your app will typically store this value in a local variable, and then do something with the value.

For example, this code statement declares a local variable named `upsideDown` to store the `bool` value returned by calling the `checkUpsideDown()` function:

```cpp
bool upsideDown = checkUpsideDown();
```

In order to work, the `checkUpsideDown()` function must be continuously called by the `loop()` function \(or continuously called by a loop within another function\).

The `checkUpsideDown()` function requires these objects as part of your global variables before the `setup()` function:

```cpp
RedBotMotors motors;
RedBotAccel accel;
```

Add the `checkUpsideDown()` custom function **after** the `loop()` function:

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

Add this code **within** the `loop()` function \(if you are using the `started` variable, add this code within the `if` statement, so it will be performed when `started` is `true`\) or within a loop in a custom function:

```cpp
    bool upsideDown = checkUpsideDown();
    if (upsideDown == true) {
      // add code to perform special actions: brake, distress signal, etc.
        motors.brake();

    }
    else {
        // add code to perform normal actions: drive, turn, etc.
        
    }
```

{% hint style="success" %}
**ADD CODE:**  You need to add code to perform special actions \(brake, etc.\) when the robot is upside-down, as well as to perform normal actions \(drive, etc.\) when the robot isn't upside-down.
{% endhint %}

## checkBump\(\)

A custom function named `checkBump()` uses the accelerometer to detect when the robot is physically bumped as the result of a collision or other force.

The accelerometer detects a bump by checking for a "pulse" acceleration.

The `checkBump()` function requires these objects as part of your global variables before the `setup()` function:

```cpp
RedBotMotors motors;
RedBotAccel accel;
```

To enable bump detection, add this code statement **within** the `setup()` function:

```cpp
accel.enableBump();
```

Add the `checkBump()` custom function **after** the `loop()` function:

```cpp
void checkBump() {

  bool bump = accel.checkBump();
  
  if (bump == true) {
    // add code to perform special actions: brake, distress signal, etc.
    motors.brake();
    
  }
}
```

{% hint style="success" %}
**ADD CODE TO FUNCTION:**  You need to add code within the `checkBump()` function to perform actions \(brake, distress signal, etc.\) when a bump occurs.
{% endhint %}

