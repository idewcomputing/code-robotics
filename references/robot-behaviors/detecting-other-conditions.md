# Detecting Other Conditions

These custom functions use the push button, IR line sensors, or accelerometer:

* `checkButton()` — check if button is being pressed
* `checkDropOff()` — check for surface drop-off \(e.g., stair step, etc.\)
* `checkBump()` — check if robot has been bumped
* `measurePitch()` — measure pitch angle \(robot tilted up or down\)
* `measureRoll()` — measure roll angle \(robot tilted left or right\)
* `checkUpsideDown()` — check if robot is upside down \(pitch or roll greater than 90°\)

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

