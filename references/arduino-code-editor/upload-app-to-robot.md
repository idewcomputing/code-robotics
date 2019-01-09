# Upload App to Robot

in progress

## Connect Robot to Computer

Your RedBot kit should have a USB to Mini-USB cable that allows you to connect the robot to a computer, in order to update the robot's app \(or to send serial data to the computer\).

If you haven't already done so, open the Arduino code editor on your computer.

Carefully plug the small end of the cable into the Mini-USB port on your RedBot circuit board. Plug the other end of the cable into a USB port on your computer.

## Turn On Robot Power

Your RedBot is powered by a battery pack containing 4 AA batteries. Be sure the battery pack cable is plugged into the barrel jack on your RedBot circuit board.

Slide the RedBot's **Power** switch to **ON**. The RedBot's green Power LED light should turn on.

If your robot's wheels start moving when the power is turned on \(because the robot is running an existing app saved on its microcontroller\), you can temporarily slide the **Motor** switch to **STOP** if desired.

## Select Correct Board and Port

in order to upload your app to your robot, the code editor must know which type of Arduino board the robot has and which port on your computer that the robot is connected to.

## Upload App to Robot

Click the **Upload** icon \(looks like a right arrow\) at the top of the code editor panel.

Once the upload is complete, the new app will immediately start running on your robot.

If necessary, you can press the **Reset** button on the robot's circuit board to restart the app.

If you used the **Motor** switch to temporarily stop the motors from running, you will need to slide the switch to **RUN** to allow the robot to drive around.

Confirm the app works as you intended. You can then revise the app to fix any coding issues or to add new code.

To stop the robot from running its app, slide the RedBot's **Power** switch to **OFF**.

## Arduino Devices Store and Run One App at a Time

Arduino devices, such as the RedBot, can only store and run **one** app at a time. If you want to change the app running on your robot, you have to upload a different app onto the robot's microcontroller.

However, you can create and save **multiple** apps in your Arduino account \(if using the Arduino Create web editor\) or on your computer \(if using the Arduino IDE desktop editor\).



