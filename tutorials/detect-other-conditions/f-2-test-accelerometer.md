# F-2 Test Accelerometer

**STILL IN PROGRESS**

Next, you'll code an app to test your robot's accelerometer by sending serial data to your computer.

## Create New App

Open your Arduino code editor, and create a new app template.

Add a block comment at the beginning of the app code to identify your new app:

```cpp
/*
Accelerometer Test
Team Info
Teacher - Class Period
*/
```

## Rename App

Rename the the new app as:  `accelerometer_test`

If you need a reminder, here are [instructions for how to rename an app](../../references/arduino-code-editor/save-and-rename-app.md).

## Include RedBot Library

[Follow the steps to include the SparkFun RedBot Library in your app](../../references/arduino-code-editor/include-redbot-library.md#include-redbot-library-in-app). \(You **don't** need to add the library to your code editor again — just include the library in this new app.\)

## Create Object for Accelerometer

The SparkFun RedBot Library also defines a class named `RedBotAccel` that can be used to control the accelerometer.

You'll need to create a new `RedBotAccel` object for your accelerometer as part of the global variables in your app. Add this code **before** the `setup()` function:

```cpp
RedBotAccel accel;
```

Hopefully, the code syntax for creating new objects looks familiar:

* `RedBotAccel` declares the class for the new object.
* `accel` represents a name for the object. Again, you decide what to name your objects and variables, as long as the names are unique and will make sense to anyone reading the code.

## Begin Serial Communication

When your robot and computer are connected with a USB cable, they can communicate with each other by transferring serial data.

In this app, your robot will send data \(accelerometer readings\) to your computer. Your Arduino code editor has a serial monitor window that can be used to view this serial data communication.

Add this code statement **within** the `setup()` function:

```cpp
Serial.begin(9600);
```

This starts the serial data communication and sets the data transfer rate to 9600 bits per second.

## Add Custom Function to Test Accelerometer

You'll add a custom function named `testAccelerometer()` which will contain code to take measurements using the accelerometer and send these to your computer as serial data.

The `RedBotAccel` class defines a method named `read()` which is used to take new measurements using the accelerometer. This method will store the measurements as different properties \(variables\) of your `RedBotAccel` object.

Here are the different properties for a `RedBotAccel` object named `accel`:

* `accel.x` – raw X-axis accelerometer measurement
* `accel.y` – raw Y-axis accelerometer measurement
* `accel.z` – raw Z-axis accelerometer measurement
* `accel.angleXZ` – calculated angle between the X and Z axes of the accelerometer \(represents the front-to-back rotation on the device's Y axis, which is also called **pitch**\)
* `accel.angleYZ` – calculated angle between the Y and Z axes of the accelerometer \(represents the side-to-side rotation on the device's X axis, which is also called **roll**\)
* `accel.angleXY` – calculated angle between the X and Y axes of the accelerometer \(represents the left-to-right rotation on the device's Z axis, which is also called **yaw**\)

Add this custom function **after** the `loop()` function:

```cpp
void testAccelerometer() {

  // get new accelerometer data
  accel.read();

  // send data to serial monitor
  // raw measurements for X, Y, and Z axes
  Serial.print("X: ");
  Serial.println(accel.x);
  Serial.print("Y: ");
  Serial.println(accel.y);
  Serial.print("Z: ");
  Serial.println(accel.z);

  // angles for X-Z (pitch), Y-Z (roll), and X-Y (yaw)
  Serial.print("Angle XZ (pitch): ");
  Serial.println(accel.angleXZ);
  Serial.print("Angle YZ (roll): ");
  Serial.println(accel.angleYZ);
  Serial.print("Angle XY (yaw): ");
  Serial.println(accel.angleXY);
  Serial.println();

  // brief delay before next reading
  delay(250);  
}
```

## Call Custom Function in Loop

As you remember, the code within a custom function is only performed if the custom function is "called" by its name within another function, such as the `setup()` function or `loop()` function.

Add this code statement **within** the `loop()` function:

```cpp
testAccelerometer();
```

By listing the name of the custom function, the custom function is "called" — so the code within that custom function will be performed one time.

For this app, this will be only code statement listed within the `loop()` function. Since the `loop()` function repeats itself continuously, the `testAccelerometer()` function will be called repeatedly.

## Upload App to Robot

Connect your robot to your computer using the USB cable. Turn on your robot, and upload the app to your robot.

After the upload is complete, do **not** unplug the USB cable. You have to keep the robot connected to your computer to allow the serial data communication.

## View Data in Serial Monitor

In your Arduino code editor, open the serial monitor, so you can view the serial data communication from your robot:

* **Arduino Create \(Web Editor\):**  Click the **Monitor** menu link in the left navigation to display the serial monitor in the middle panel.
* **Arduino IDE \(Desktop Editor\):**  Under the **Tools** menu, select "Serial Monitor." A new window will appear displaying the serial monitor.

Place the robot on a level surface, such as your desk or table. View the accelerometer readings in the serial monitor. If the surface is perfectly level, the values for angle XZ \(pitch\) and angle YZ \(roll\) will be zero \(though you may notice your surface is not perfectly level\).



