# B-6 Upload App to Robot

**STILL IN PROGRESS**

Let's upload your "Hello World" app to your robot to see if it works.

## Connect Robot to Computer

Your RedBot kit should have a USB to Mini-USB cable that allows you to connect the robot to a computer, in order to update the robot's app \(or to send serial data to the computer\).

Carefully plug the small end of this cable into the Mini-USB port on your RedBot circuit board. Plug the other end of the cable into a USB port on your computer.

## Turn On Robot Power

Your RedBot is powered by a battery pack containing 4 AA batteries. Be sure the battery pack cable is plugged into the barrel jack on your RedBot circuit board.

Slide the RedBot's **Power** switch to **ON**. The RedBot's green Power LED light should turn on.

If you were given an existing robot and its wheels start spinning when you turn the power on, you can temporarily slide the Motor switch to STOP.

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

{% hint style="danger" %}
**UPLOAD ERROR:**  If the Arduino code editor indicates there was a problem uploading to the board, it most likely means that the correct port was **not** selected. Be sure the correct USB port is selected in the code editor.
{% endhint %}

## Confirm App Works

Confirm that the built-in green D13 LED light blinks on and off in a repeating pattern \(changing every 0.5 second\).

Arduino devices, such as the RedBot, can only store and run **one** app at a time. If you want to change the app running on your robot, you have to upload a different app from your code editor to the robot.

## Modify App and Upload to Robot

Next, try modifying the code within the `loop()` function to change the LED blinking pattern. Here are some possible options your team could choose:

* Make the LED blink faster (hint: use a shorter delay)
* Make the LED blink slower
* Make the LED blink in a different pattern \(such as two quick blinks followed by a longer pause\)

Upload your modified app to your robot to see if your changes worked as you expected.
