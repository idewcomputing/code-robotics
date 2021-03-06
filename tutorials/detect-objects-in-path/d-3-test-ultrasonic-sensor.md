# D-3 Test Ultrasonic Sensor

Next, you'll code an app to test your ultrasonic sensor \(if your robot is equipped with one\).

{% hint style="info" %}
**ADD-ON COMPONENT:** The SparkFun RedBot Kit does **NOT** include an ultrasonic sensor as a standard component. However, SparkFun sells the [HC-SR04 Ultrasonic Sensor](https://www.sparkfun.com/products/13959), which can be easily connected to a RedBot. Your teacher may have added this sensor to your kit.
{% endhint %}

If necessary, follow these [instructions to attach an ultrasonic sensor to the robot](../../references/physical-inputs/ultrasonic-sensor.md#connect-ultrasonic-sensor-to-redbot-mainboard).

## How Ultrasonic Sensor Works

The ultrasonic sensor has a transmitter \(i.e., a speaker\) that can produce high-frequency sound, which cannot be heard by the human ear. The sensor also has a receiver \(i.e., a microphone\) that detects the echo of the high-frequency sound when it is reflected back from a nearby object. By measuring how much time it takes for the echo to arrive, you can calculate the distance between the sensor and the object.

![Ultrasonic Sensor](../../.gitbook/assets/ultrasonic-sensor.jpg)

This ultrasonic sensor measures distances in a narrow cone of about 15° in front of the sensor. This sensor can detect obstacles located up to 400 cm away \(about 13 feet\). The distance measurements from the sensor are very accurate, within about 3 mm \(about 0.1 inch\) of the actual distance.

## Save Copy of App With New Name <a id="save-copy-of-app-with-new-name"></a>

In your Arduino code editor, open your existing app named `detect_collisions_test`. Use the "Save As" command to save a copy as a different app named:  `ultrasonic_sensor_test`

Once you saved the new app name, modify the block comment near the beginning of the app code to change `Detect Collisions Test` to `Ultrasonic Sensor Test`.

## Add Variables for Sensor

You'll need to create global variables to store the pin numbers of the ultrasonic sensor's transmitter \(Trig\) and receiver \(Echo\), which should be connected to I/O pins A0 and A1 on the RedBot's circuit board.

Add this code **before** the `setup()` function:

```cpp
int TRIG_PIN = A0;
int ECHO_PIN = A1;
```

## Set Pin Modes for Sensor

You'll need to set the pin modes for the ultrasonic sensor's transmitter \(Trig\) and receiver \(Echo\). The transmitter is an output because it will produce high-frequency sound. The receiver is an input because it will detect the echo of the high-frequency sound when it reflects back from nearby obstacles.

Add this code **within** the `setup()` function:

```cpp
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  digitalWrite(TRIG_PIN, LOW);
```

Notice that a `digitalWrite()` statement was included to ensure the transmitter is turned off \(`LOW`\) when the app first starts.

## Begin Serial Communication

When your robot and computer are connected with a USB cable, they can communicate with each other by transferring serial data.

In this app, your robot will send data \(distance measurements\) to your computer. Your Arduino code editor has a serial monitor window that can be used to view this serial data communication.

Add this code statement **within** the `setup()` function:

```cpp
Serial.begin(9600);
```

This starts the serial data communication and sets the data transfer rate to 9600 bits per second.

## Add Custom Function to Measure Distance

You'll add another custom function named `measureDistance()` which will contain code that uses the ultrasonic sensor to measure the distance between the sensor and the closest object ahead in the robot's path.

When this custom function is called, it will return the distance measurement as a decimal value \(`float`\), which your app will need to store in a local variable.

The comments embedded in the custom function help explain how it works.

Add this custom function **after** the `loop()` function:

```cpp
float measureDistance() {
  // uses HC-SR04 ultrasonic sensor
  unsigned long start_time, end_time, pulse_time;

  // trigger ultrasonic signal for 10 microseconds
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);

  // wait until echo received
  while (digitalRead(ECHO_PIN) == 0);

  // measure how long echo lasts (pulse time)
  start_time = micros(); // get start time in microseconds
  while (digitalRead(ECHO_PIN) == 1); // wait until echo pulse ends
  end_time = micros(); // get end time
  pulse_time = end_time - start_time; // subtract to get duration

  // pulse time of 23200 represents maximum distance for this sensor
  if (pulse_time > 23200) pulse_time = 23200;

  // calculate distance to object using pulse time
  float dist_cm = pulse_time / 58.0;
  float dist_in = pulse_time / 148.0;

  // need 60 ms delay between ultrasonic sensor readings
  delay(60);

  // return distance value
  return dist_in; // or can return dist_cm
}
```

## Modify Code to Perform When Robot is Started

When the D12 button is pressed to "start" the robot, we want the ultrasonic sensor to continuously measure the distance to the closest object and send this data to the serial monitor.

First, **delete** the existing code statements **within** the `if` statement in the `loop()` function that drive the motors and call the `checkBumpers()` custom function when `started` is `true`.

Next, add this code **within** the `if` statement in the `loop()` function, so it will be performed when `started` is `true`:

```cpp
    float distance = measureDistance();
    Serial.print(distance);
    Serial.println(" inches");
```

As you can see, this code declares a local variable named `distance` which has a data type of `float`\(decimal number\). The `distance` variable is assigned a value equal to the value returned by calling the `measureDistance()` function.

Next, the value of `distance` is sent \(`print`\) to the serial monitor followed by a text string \(`" inches"`\).

## Upload App to Robot

Connect your robot to your computer using the USB cable. Turn on your robot, and upload the app to your robot.

After the upload is complete, do **not** unplug the USB cable. You have to keep the robot connected to your computer to allow the serial data communication.

## View Data in Serial Monitor

In your Arduino code editor, open the serial monitor, so you can view the serial data communication from your robot:

* **Arduino Create \(Web Editor\):**  Click the **Monitor** menu link in the left navigation to display the serial monitor in the middle panel.
* **Arduino IDE \(Desktop Editor\):**  Under the **Tools** menu, select "Serial Monitor." A new window will appear displaying the serial monitor.

Press the D12 button on your robot's circuit board. Your robot's ultrasonic sensor will start measuring the distance to the closest object in front of the sensor. In the serial monitor, view the data showing the distance measurements.

The sensor can accurately measure distances within a range from 2 cm up to 400 cm \(about 1 inch up to about 13 feet\).

Place your hand \(or another object\) in front of the ultrasonic sensor, and move your hand \(or the object\) further or closer to confirm that the distance measurements change. If necessary, you can use a ruler or measuring tape to verify the accuracy of the distance measurements.

Small objects \(such as your hand\) can be detected accurately if they are within about 24 inches of the sensor. For farther distances, the object may need to have a larger surface area to produce an accurate measurement \(large flat surfaces such as walls work really well\).

When you're done testing the ultrasonic sensor, press the D12 button again to "pause" the robot \(and save battery power by stopping the ultrasonic sensor measurements\) – or you can turn off the robot's power.





