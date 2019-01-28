# Detecting Other Conditions

These custom functions use the push button, IR line sensors, or accelerometer:

* `checkButton()` — check if button is being pressed
* `checkDropOff()` — check for surface drop-off \(e.g., stair step, etc.\)
* `checkUpsideDown()` — check if robot is upside down \(pitch or roll greater than 90°\)
* `checkBump()` — check if robot has been bumped

## checkButton\(\)

A custom function named `checkButton()` checks whether the built-in D12 button is being pressed. If the button is pressed, the function will toggle the value of a global variable named `started` from `false` to `true` \(or vice versa\).

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

This can be combined with code contained in the `loop()` function to perform different actions based on whether the robot is "started" \(`started == true`\) or "paused" \(`started == false`\):

```cpp
  checkButton();
  if (started == true) {
    // add code to perform when "started"
    
  }
  else {
    // add code to perform when "paused"
    
  }
```

## checkDropOff\(\)

A custom function named `checkDropOff()` uses the IR line sensors to allow your robot to detect a surface drop-off \(such as:  the edge of a table, a stair step leading down, a hole in the surface, etc.\).

When a surface drop-off is detected, the motors will be braked. You can add code to perform additional actions \(such as backing up, changing direction, etc.\). 

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

