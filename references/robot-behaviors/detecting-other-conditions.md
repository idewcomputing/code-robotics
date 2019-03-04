# Detecting Other Conditions

These custom functions use the [push button](../physical-inputs/push-button.md), [IR line sensors](../physical-inputs/ir-line-sensors.md), or [accelerometer](../physical-inputs/accelerometer.md):

* `checkButton()` — check if button is being pressed
* `pauseRobot()` — wait until button is pressed before performing next step in task
* `checkDropOff()` — check for surface drop-off \(e.g., stair step, etc.\)
* `checkUpsideDown()` — check if robot is upside down \(pitch or roll greater than 90°\)
* `checkBump()` — check if robot has been bumped

## checkButton\(\)

A custom function named `checkButton()` checks whether the built-in D12 button is being pressed. If the button is pressed, the function will toggle the value of a global variable named `started` from `false` to `true` \(or vice versa\). The function will also provide feedback by blinking the built-in D13 LED light and beeping with the speaker.

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

{% hint style="info" %}
**ONE BUTTON LIBRARY:**  Another option is to [use the OneButton library](../physical-inputs/push-button.md#use-onebutton-object) to detect different types of button presses \(single-press, double-press, or long-press\).
{% endhint %}

## pauseRobot\(\)

A custom function named `pauseRobot()` can be used to add "pauses" in a robot's task. The robot will wait until the built-in D12 button is pressed before performing the next step in the task. This could be useful in a robot task demonstration.

For example, you could add a "pause" for a simulated step in a task. The robot will "pause" while you complete or explain the simulated step. Once you press the button, the robot will continue with the next step in the task.

This "pause" is created using a `while()` loop that keeps repeating itself until the button is pressed. The `while()` loop contains a short delay before it checks the button again.

Add this code statement in the `loop()` function or a custom function wherever you want the robot to pause and wait for the button to be pressed:

```cpp
void pauseRobot() {
  motors.stop(); // be sure robot is stopped
  while (button.read() == false) delay(10); // wait until button pressed
}
```

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

Add this code **within** the `loop()` function \(if you are using the `started` variable, add this code within the `if` statement, so it will be performed when `started` is `true`\):

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

