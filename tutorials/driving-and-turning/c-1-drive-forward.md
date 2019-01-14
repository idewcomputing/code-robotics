# C-1 Driving

#### **STILL IN PROGRESS**

## Create New App Template

If necessary, log in to the Arduino Create web editor, or open the Arduino IDE desktop editor.

Create a new app template. If you need a reminder, here are [instructions for creating a new app template](../../references/arduino-code-editor/create-new-app.md).

## Rename App

Rename the the new app as:  `driving_test`

If you need a reminder, here are [instructions for how to rename an app](../../references/arduino-code-editor/save-and-rename-app.md).

## Add Block Comment

Add this block comment at the beginning of your app code. Modify the comment to list your information.

```cpp
/*
Driving Test App
Team 3 - Destiny, Katya, Lucas, Miguel
Ms. Hopper - Period 2
*/
```

## Include RedBot Library

Arduino apps can include one or more libraries. A library is a pre-built code file that makes it easier to program certain things in your app.

There is a **SparkFun RedBot Library** \(filename: `RedBot.h`\) that makes it much easier to control the motors and sensors connected to your RedBot.

You will need to add a copy of the SparkFun RedBot Library to your code editor, which is a **one-time process**. Then you will also need to include a copy of this library in **each new robot app**.

[Follow these instructions to \(1\) add the SparkFun RedBot Library to your code editor, and \(2\) include the library in your current app](../../references/arduino-code-editor/include-library-in-app.md).

You should now have an `#include` statement for the RedBot library \(filename: `RedBot.h`\) listed at the beginning of your app code.

## Create RedBotMotors Object



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



