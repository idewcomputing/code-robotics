# C-1 Driving

#### **STILL IN PROGRESS**

include RedBot library

create RedBotMotors object

keep "push to start" if statement \(if button pushed, then blink LED & produce tone\)

add drive forward sequence within if statement:

```cpp
motors.drive(power);
delay(time);
motors.brake();
```

upload app to robot, and confirm it works

#### TROUBLESHOOTING

If robot spins clockwise \(to the right\), reverse the red and black wires of the right motor

If robot spins counter-clockwise \(to the left\), reverse the red and black wires of the left motor

If robot drives backwards, reverse the red and black wires for each motor

NOTE: If the robot does not drive in a perfectly straight line, this is actually "normal." In theory, if both motors are being driven with the same amount of power, the robot should travel in a straight line. However, even though the two motors are supposed to be identical and are being driven with identical amount of power, they might not necessarily rotate at the exact same rate - even a minor difference in their rotation rate will cause the robot to slowly drift either to the left or to the right \(depending on which motor is rotating more slowly\), instead of driving perfectly straight.

Later in this tutorial, you'll use the wheel encoders to continuously measure and compare the rotation rates of the motors and make small power adjustments to keep the robot driving in a straight line. You'll also use the wheel encoders to calculate how far the wheels have rotated, in order to make the robot travel a specific distance.

#### DRIVE BACKWARDS \(REVERSE\)

keep drive forward sequence, and add drive backward sequence within if statement:

```cpp
motors.drive(-power);
delay(time);
motors.brake();
```

upload app to robot, and confirm it works



