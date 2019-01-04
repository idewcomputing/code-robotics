# C-2 Turns \(Pivoting\)

#### **STILL IN PROGRESS**

turn on one wheel vs. pivoting on both wheels

3 most common turns required:  turn 90° right, turn 90° left, and turn 180° around

keep drive forward sequence, but remove drive backward in if statement

add pivot right sequence within if statement:

```cpp
motors.pivot(power);
delay(time);
motors.brake();
```

upload app to robot, and confirm it works - may need to adjust delay time to get as close to 90° right turn as possible - test, adjust delay, upload revised app, test again

modify app to pivot left:  use negative power to turn left - keep same delay time

upload app to robot, and confirm it works - may need to adjust delay time to get as close to 90° left turn as possible - test, adjust delay, upload revised app, test again

modify app to turn around \(pivot 180°\):  can use positive or negative power - should be approximately 2 times the delay time as turning right or left

upload app to robot, and confirm it works - may need to adjust delay time to get as close to 180° turn as possible - test, adjust delay, upload revised app, test again

Later in this tutorial, you'll use the wheel encoders to measure how far the wheels have turned, in order to make the robot pivot by a specific angle.

