# D-3 Test Ultrasonic Sensor

**STILL IN PROGRESS**

Next, you'll code an app to test your ultrasonic sensor \(if your robot is equipped with one\).

{% hint style="info" %}
**ADD-ON COMPONENT:** The SparkFun RedBot Kit does **NOT** include an ultrasonic sensor as a standard component. However, SparkFun sells the [HC-SR04 Ultrasonic Sensor](https://www.sparkfun.com/products/13959), which can be easily connected to a RedBot. Your teacher may have added this sensor to your kit.
{% endhint %}

If necessary, follow these [instructions to attach an ultrasonic sensor to the robot](../../references/physical-inputs/ultrasonic-sensor.md#connect-ultrasonic-sensor-to-redbot-mainboard).

## Save Copy of App With New Name <a id="save-copy-of-app-with-new-name"></a>

In your Arduino code editor, open your existing app named `detect_collisions_test`. Use the "Save As" command to save a copy as a different app named:  `ultrasonic_sensor_test`

Once you saved the new app name, modify the block comment near the beginning of the app code to change `Detect Collisions Test` to `Ultrasonic Sensor Test`.

## Add Global Variables for Sensor

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

You'll add another custom function named `measureDistance()` which will contain code that uses the ultrasonic sensor to measure the distance between the sensor and the closest object ahead in the robot's path. The custom function will return this distance as a decimal value \(`float`\), which your app will store in a local variable.

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



use testUltrasonicSensor\(\) custom function to use serial monitor to view distance measurements



