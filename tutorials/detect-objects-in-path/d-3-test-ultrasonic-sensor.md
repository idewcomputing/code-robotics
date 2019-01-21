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

You'll need to set the pin modes for the ultrasonic sensor's transmitter \(Trig\) and receiver \(Echo\). The transmitter is an output because it will produces high-frequency sound. The receiver is an input because it will detect the echo of the high-frequency sound when it reflects back from nearby obstacles.

Add this code **within** the `setup()` function:

```cpp
pinMode(TRIG_PIN, OUTPUT);
pinMode(ECHO_PIN, INPUT);
digitalWrite(TRIG_PIN, LOW);
```

Notice that a `digitalWrite()` statement was included to ensure the transmitter is turned off \(`LOW`\) when the app first starts.



use measureDistance\(\) custom function - explain conceptually how it works

use testUltrasonicSensor\(\) custom function to use serial monitor to view distance measurements



