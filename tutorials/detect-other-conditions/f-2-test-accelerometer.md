# F-2 Test Accelerometer

Next, you'll code an app to test your robot's accelerometer by measuring the robot's pitch \(front-to-back tilt\) and roll \(side-to-side tilt\) and sending these measurements to your computer as serial data.

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

You may have noticed that you **didn't** have to indicate which I/O pins the accelerometer is connected to. This is because the RedBot library assumes the accelerometer is connected to pins A4 and A5 on the RedBot circuit board.

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

For your apps, you probably **won't** use the raw accelerometer measurements. Instead, you'll most likely want to know the calculated angles for the XZ, YZ, and XY planes.

This diagram shows how the accelerometer's X, Y, and Z axes are oriented on the RedBot and what the XZ, YZ, and XY angles represent.

![](../../.gitbook/assets/redbot-pitch-roll-yaw.jpg)

Add this custom function **after** the `loop()` function:

```cpp
void testAccelerometer() {

  // get new accelerometer data
  accel.read();

  // send data to serial monitor
  Serial.print("Pitch: ");
  Serial.print(accel.angleXZ);
  Serial.print("\tRoll: ");
  Serial.print(accel.angleYZ);
  Serial.print("\tYaw: ");
  Serial.println(accel.angleXY);

  // brief delay before next reading
  delay(100);
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

Place the robot on a level surface, such as your desk or table. View the accelerometer readings in the serial monitor. If the surface is perfectly level, the values for pitch \(angle XZ\) and roll \(angle YZ\) will be zero. However, you may discover that your values are close to zero \(instead of exactly zero\).

Follow the steps below to test pitch, roll, and yaw by rotating your robot's body in different directions.

#### PITCH

Pitch \(angle XZ\) is the front-to-back rotation on the device's Y axis. Pitch can range from -180° to 180°.

1. Hold the robot in the air, and slowly rotate the robot from front-to-back to tilt the front end up. Watch the pitch value change in the serial monitor as you change the tilt. When the robot's front end is tilted straight up, the pitch will be 90°.
2. Rotate the robot so it is level from front-to-back. When it is level, the pitch will be 0°.
3. Rotate the robot so its front end is tilts down. When the robot's front end is tilted straight down, the pitch will be -90°.

#### ROLL

Roll \(angle YZ\) is the side-to-side rotation on the device's X axis. Roll can range from -180° to 180°.

1. Hold the robot in the air, and slowly rotate the robot from side-to-side, so the left side is tilted up. Watch the pitch change in the serial monitor as you change the tilt. When the robot's left side is tilted straight up, the roll will be 90°.
2. Rotate the robot so it is level from side-to-side. When it is level, the roll will be 0°.
3. Rotate the robot so its left side is tilted down. When the robot's left side is tilted straight down, the roll will be -90°.

#### YAW

Yaw \(angle XY\) is the right-to-left rotation on the device's Z axis. Yaw can range from -180° to 180°.

However, when the RedBot is on a level surface, the yaw value **cannot** be accurately determined because the acceleration due to Earth's gravity is acting in the same direction \(i.e., downward\) as the Z axis.

1. Place the robot back down on a level surface, such as your desk or table. Check the yaw value in the serial monitor.
2. Rotate the robot clockwise to the right, while checking the yaw value in the serial monitor. You'll notice that the yaw value changes **randomly** – and does **not** represent which direction the robot is pointed \(i.e., the robot's rotation on the Z axis\).
3. Rotate the robot counter-clockwise to the left, while checking the yaw value in the serial monitor. Again, the yaw value changes randomly – and does **not** represent the robot's direction.

This is why your robot apps will probably **not** use yaw values from the accelerometer. \(However, there are other types of sensors – not included in this kit – which can be used to accurately measure yaw.\)

{% hint style="success" %}
**POWER DOWN:** When you're done testing the accelerometer, turn off your robot's power to conserve battery power.
{% endhint %}



