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

In order to upload your app to your robot, the code editor must know which type of Arduino board your robot has and which USB port on your computer that the robot is connected to.

If you previously selected your Arduino board type \(which should be "Arduino/Genuino Uno"\), the code editor should remember this selection.

#### Arduino Create \(Web Editor\)

1. Click "Select Other Board & Port" in the drop down menu at the top of the code editor panel.
2. In the pop-up, verify that "Arduino/Genuino Uno" is selected, and then select the correct USB port that your robot is connected to. Finally, click the **OK** button.

#### Arduino IDE \(Desktop Editor\)

Under the **Tools** menu, verify that "Arduino/Genuino" is selected in the **Board** sub-menu, and then select the correct USB port in the **Port** sub-menu.

* On Mac, the correct port will include "usbserial" as part of its name.
* On Windows, there should be one or more numbered COM ports listed. You may have to select one, try uploading your app — and then if the app won't upload, switch to another COM port instead.

Once you've selected the correct port, the code editor should remember this selection while you keep the code editor open. However, if you quit the code editor, you'll have to select the correct port again the next time you use the code editor.

## Upload App to Robot

Click the **Upload** icon \(looks like a right arrow\) at the top of the code editor panel.

Once the upload is complete, the new app will immediately start running on your robot.

If necessary, you can press the **Reset** button on the robot's circuit board to restart the app.

If you used the **Motor** switch to temporarily stop the motors from running, you will need to slide the switch to **RUN** to allow the robot to drive around.

Confirm the app works as you intended. You can then revise the app to fix any coding issues or to add new code.

To stop the robot from running its app, slide the RedBot's **Power** switch to **OFF**.

{% hint style="danger" %}
**UPLOAD ERROR:**  If the Arduino code editor indicates there was a problem uploading to the board, it most likely means that the correct port was **not** selected. Be sure the correct USB port is selected in the code editor.
{% endhint %}

## Arduino Devices Store and Run One App at a Time

Arduino devices, such as the RedBot, can only store and run **one** app at a time. If you want to change the app running on your robot, you have to upload a different app onto the robot's microcontroller.

However, you can create and save **multiple** apps in your Arduino account \(if using the Arduino Create web editor\) or on your computer \(if using the Arduino IDE desktop editor\).



