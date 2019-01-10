# Upload App to Robot

Uploading an app to your robot from your code editor requires several steps:

1. Connect Robot to Computer
2. Turn on Robot Power
3. Select Correct Board and Port
4. Upload App to Robot

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

* On Mac, the correct port should include "usbserial" as part of its name.
* On Windows, there should be one or more numbered COM ports listed. You may have to select one, try uploading your app — and then if the app won't upload, switch to another COM port instead until you identify the correct port.

#### Arduino IDE \(Desktop Editor\)

Under the **Tools** menu, verify that "Arduino/Genuino" is selected in the **Board** sub-menu, and then select the correct USB port in the **Port** sub-menu:

* On Mac, the correct port should include "usbserial" as part of its name.
* On Windows, there should be one or more numbered COM ports listed. You may have to select one, try uploading your app — and then if the app won't upload, switch to another COM port instead until you identify the correct port.

Once you've selected the correct port, the code editor should remember this selection while you keep the code editor open. However, if you close the code editor, you'll have to select the correct port again the next time you open and use the code editor.

## Upload App to Robot

Click the **Upload** icon \(looks like a right arrow\) at the top of the code editor panel. The code editor will automatically save and verify the app before uploading it to your robot.

During the upload process, you may notice two green LED lights \(labeled TX and RX, located next to the Mini USB port\) blinking rapidly as the app code is transferred to the robot.

Once the upload is complete, the new app will immediately start running on your robot.

If you used the **Motor** switch to temporarily stop the motors from running, you will need to slide the switch to **RUN** to allow the robot to drive around.

If necessary, you can press the **Reset** button on the robot's circuit board to restart the app.

Confirm the app works as you intended.  If the robot doesn't do what you expected, you'll have to modify your app code, and then upload the modified app to your robot.

To stop the robot from running its app, slide the RedBot's **Power** switch to **OFF**.

{% hint style="danger" %}
**UPLOAD ERROR:**  If the Arduino code editor indicates there was a problem uploading to the board, it most likely means that the correct port was **not** selected. Be sure the correct USB port is selected in the code editor.
{% endhint %}

{% hint style="info" %}
**ONE APP AT A TIME:**  Arduino devices, such as the RedBot, can only store and run **one** app at a time. If you want to change the app running on your robot, you have to upload a different app to your robot from your code editor.
{% endhint %}



