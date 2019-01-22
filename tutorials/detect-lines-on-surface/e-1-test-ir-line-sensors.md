# E-1 Test IR Line Sensors

First, you'll code an app to test your robot's IR line sensors by sending serial data to your computer.

## Create New App

Open your Arduino code editor, and create a new app template.

Add a block comment at the beginning of the app code to identify your new app:

```cpp
/*
Line Sensors Test
Team Info
Teacher - Class Period
*/
```

## Rename App

Rename the the new app as:  `line_sensors_test`

If you need a reminder, here are [instructions for how to rename an app](../../references/arduino-code-editor/save-and-rename-app.md).

## Include RedBot Library

[Follow the steps to include the SparkFun RedBot Library in your app](../../references/arduino-code-editor/include-redbot-library.md#include-redbot-library-in-app). \(You **don't** need to add the library to your code editor again — just include the library in this new app.\)

## Create Objects for Line Sensors

The SparkFun RedBot Library also defines a class named `RedBotSensor` that can be used to control the IR line sensors.

You'll need to create three new `RedBotSensor` objects for your line sensors as part of the global variables in your app. Add this code **before** the `setup()` function:

```cpp
RedBotSensor leftLine(A3);
RedBotSensor centerLine(A6);
RedBotSensor rightLine(A7);
```

Hopefully, the format for create new objects looks familiar by now:

* `RedBotSensor` declares the class for the new object.
* `leftLine`, `centerLine`, and `rightLine` represent unique names for each object. Again, you decide what to name your objects. They should make sense to anyone reading the code.
* `A3`, `A6`, and `A7` represent the I/O pin numbers that the left, center, and right line sensors should be connected to. If your sensors were connected to different pins, you'd change these pin numbers.

## Begin Serial Communication

When your robot and computer are connected with a USB cable, they can communicate with each other by transferring serial data.

In this app, your robot will send data \(IR sensor measurements\) to your computer. Your Arduino code editor has a serial monitor window that can be used to view this serial data communication.

Add this code statement **within** the `setup()` function:

```cpp
Serial.begin(9600);
```

This starts the serial data communication and sets the data transfer rate to 9600 bits per second.

## Add Custom Function to Test Line Sensors

You'll add a custom function named `testLineSensors()` which will contain code to read the values from each IR line sensor and send these to your computer as serial data.

The `RedBotSensor` class defines a method named `read()` which is used to read the value from a specific IR line sensor. The `read()` method will return an integer value \(whole number\) between 0-1023 representing a measurement of how much reflected IR light was detected:

* **Lower values** indicate **more** IR light was reflected back. This indicates a **lighter-colored surface**.
* **Higher values** indicate **less** IR light was reflected back. This indicates a **darker-colored surface**.

If the values are **very high** \(greater than 950\), this probably indicates a **surface drop-off** \(such as: a stair step leading down, the edge of a table, a hole in the surface, etc.\).

Add this custom function **after** the `loop()` function:

```cpp
void testLineSensors() {
  // get IR sensor readings
  int leftSensor = leftLine.read();
  int centerSensor = centerLine.read();
  int rightSensor = rightLine.read();

  // send data to serial monitor
  Serial.print("L: ");
  Serial.print(leftSensor);
  Serial.print("\tC: ");
  Serial.print(centerSensor);
  Serial.print("\tR:");
  Serial.println(rightSensor);

  // brief delay before next reading
  delay(100);
}
```

## Call Custom Function in Loop

As you hopefully remember, the code within a custom function is only performed if the custom function is "called" by its name within another function, such as the `setup()` function or `loop()` function.

Add this code statement **within** the `loop()` function:

```cpp
testLineSensors();
```

By listing the name of the custom function, the custom function is "called" — so the code within that custom function will be performed one time.

For this app, this will be only code statement listed within the `loop()` function. Since the `loop()` function repeats itself continuously, the `testLineSensors()` function will be called repeatedly.

## Upload App to Robot

Connect your robot to your computer using the USB cable. Turn on your robot, and upload the app to your robot.

After the upload is complete, do **not** unplug the USB cable. You have to keep the robot connected to your computer to allow the serial data communication.

## View Data in Serial Monitor

In your Arduino code editor, open the serial monitor, so you can view the serial data communication from your robot:

* **Arduino Create \(Web Editor\):**  Click the **Monitor** menu link in the left navigation to display the serial monitor in the middle panel.
* **Arduino IDE \(Desktop Editor\):**  Under the **Tools** menu, select "Serial Monitor." A new window will appear displaying the serial monitor.

Place the robot on a sheet of white paper on your desk or table. View the IR sensor readings in the serial monitor. Even for a white sheet of paper, the sensor readings will probably be between 400-700. Your sensor readings will probably have different values. All of this normal — the IR sensor readings can be affected by the ambient light in the room.

Next, use a black permanent marker to draw a line \(about 0.5 inch wide and about 3 inches long\) in the middle of the paper.  [Alternatively, you could print this test page](https://drive.google.com/open?id=1_mJCy-WdcnZ7QPPBrMELXCgFrpG-g6VV).

Position the robot so only the **center** line sensor is above the dark line. View the IR sensor readings in the serial monitor. You should see that the center sensor reading is higher than the left and right sensors \(which are positioned above a white surface\). For a uniform black line, the center sensor reading should be around 800 \(or more\).

Then rotate the robot so all three line sensors are "on" the dark line. View the sensor readings in the serial monitor. All three sensor readings should be around 800 \(or more\).

Finally, position the robot near the edge of your desk or table. Then slowly roll the robot towards the edge until the IR line sensors are just hanging over the edge \(be sure the robot won't roll off\). View the sensor readings in the serial monitor. All three sensor readings should be around 1000 \(or more\).

{% hint style="success" %}
**POWER DOWN:**  When you're done testing the IR line sensors, turn off your robot's power to conserve battery power.
{% endhint %}

