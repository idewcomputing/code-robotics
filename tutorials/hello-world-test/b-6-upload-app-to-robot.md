# B-6 Upload App to Robot

**STILL IN PROGRESS**

Let's upload your "Hello World" app to your robot to see if it works.

## Connect Robot to Computer

Your RedBot kit should have a USB to Mini-USB cable that allows you to connect the robot to a computer, in order to update the robot's app \(or to send serial data to the computer\).

Carefully plug the small end of this cable into the Mini-USB port on your RedBot circuit board. \(The cable only plugs in one way, so turn it over if it doesn't seem to fit.\) Plug the other end of the cable into a USB port on your computer.

## Turn On Robot Power

Your RedBot is powered by a battery pack containing 4 AA batteries. Be sure the battery pack cable is plugged into the barrel jack on your RedBot circuit board.

Slide the RedBot's **Power** switch to **ON**. The RedBot's green Power LED light should turn on.

If you were given an existing robot and its wheels start spinning when you turn the power on, you can temporarily slide the Motor switch to STOP.

## Select Correct Board and Port

In order to upload your app to your robot, the code editor must know which type of Arduino board your robot has and which port on your computer that the robot is connected to.



## Upload App to Robot

Click the **Upload** icon \(looks like a right arrow\) at the top of the code editor panel.

## Confirm App Works

Once the upload is complete, the new app will immediately start running on your robot.

Confirm that the built-in blue D13 LED light blinks on and off in a repeating pattern \(changing every 0.5 second\).

## Arduino Devices Store and Run One Program at a Time

Arduino devices, such as the RedBot, can only store and run **one** program at a time. If you want to change the program running on your robot, you have to upload a different program onto the robot.

However, you can create and save **multiple** programs in your Arduino account \(if using the Arduino Create web editor\) or on your computer \(if using the Arduino IDE desktop editor\).

## Modify App and Upload to Robot

Next, try modifying the code within the `loop()` function to change the LED blinking pattern. Here are some possible options your team could choose:

* Make the LED blink faster
* Make the LED blink slower
* Make the LED blink in a different pattern \(such as two quick blinks followed by a longer pause\)

Upload your modified app to your robot to see if your changes worked as you expected.

