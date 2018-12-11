# Robot Behaviors

A robot behavior can be defined as any action that the robot can perform. It can be helpful to think about robot behaviors in terms of their **level** \(depends on complexity of behavior\) and **type** \(depends on purpose of behavior\).

## Levels of Robot Behaviors

Robot behaviors can generally be categorized into different levels of complexity:

* **Basic Behaviors** – these are low-level behaviors that perform a single action, such as: turning on the motors, reading a sensor, etc. In the robot's program, basic behaviors can be performed with a single code statement.
* **Simple Behaviors** – these are mid-level behaviors that perform a simple task, such as: driving forward for 5 seconds, turning to the right, etc. A simple behavior consists of a sequence of basic behaviors. In the robot's program, simple behaviors require several code statements.
* **Complex Behaviors** – these are high-level behaviors that perform a complex task, such as: following a line, driving around an obstacle, etc.  A complex behavior consists of a sequence of simple behaviors. In the robot's program, complex behaviors require multiple code statements, which are often put into a custom function.

Here is some example code to help show different levels of robot behaviors:

```cpp
motors.drive(200);
delay(2800);
motors.brake();

motors.pivot(100);
delay(1300);
motors.brake();

motors.drive(200);
delay(2800);
motors.brake();
```

* Each code statement represents a **basic behavior**. For example, line 1 turns on the motors at a power of 200. Line 2 produces a delay of 2.8 seconds. Line 3 brakes the motors.
* Each code block represents a **simple behavior**. For example, lines 1-3 work together to make the robot drive forward about 4 feet. Lines 5-7 work together to make the robot turn around \(~ 180°\).
* All of this code represents a **complex behavior**:  the robot will drive forward, turn around, and return to its starting position.

The exact distinction between a "simple" behavior and a "complex" behavior is not necessarily clear.  The value of thinking about different levels of robot behaviors is to simply recognize that behaviors can combined \(or broken down\) into other behaviors:

* **Composition:**  Lower-level behaviors can be combined into a sequence that produces a more complex behavior.
* **Decomposition:**  A higher-level behavior can be broken down into a sequence of more simple behaviors.

Understanding composition and decomposition can help you plan out the structure of your robot's program and figure out how to program the higher-level behaviors that you need to demonstrate your task scenarios.

## Types of Robot Behaviors

The table below lists numerous robot behaviors that the RedBot can perform, which may be useful for coding your own robot program. Each behavior is linked to a reference that provides and explains the code necessary to perform the behavior.

The robot behaviors in this table could be categorized into different types based on their purpose:

* Producing Alerts
* Driving
* Turning
* Detecting Lines
* Detecting Objects
* Detecting Other Conditions

| Robot Behavior | Components Required |
| :--- | :--- |
| Turn light on/off | LED Light |
| Produce sound | Speaker \(Buzzer\) |
| Drive for specific amount of time | Motors |
| Drive straight continuously | Wheel Encoders, Motors |
| Drive straight for specific distance | Wheel Encoders, Motors |
| Turn for specific amount of time | Motors |
| Turn by specific angle \(90° right, etc.\) | Wheel Encoders, Motors |
| Follow a line | IR Line Sensors, Motors |
| Avoid a line | IR Line Sensors, Motors |
| Drive straight while counting lines crossed | Wheel Encoders, IR Line Sensors, Motors |
| Follow a line while counting lines crossed | IR Line Sensors, Motors |
| Detect bumper collision with object | Mechanical Bumpers |
| Measure distance ahead to closest object | Ultrasonic Sensor |
| Avoid collision with object in path | Ultrasonic Sensor, Wheel Encoders, Motors |
| Avoid collision with object while following line | IR Line Sensors, Ultrasonic Sensor, Wheel Encoders, Motors |
| Find closest object \(360° scan\) and drive towards it | Ultrasonic Sensor, Wheel Encoders, Motors |
| Check if button is pressed | Push Button |
| Check for surface drop-off | IR Line Sensors |
| Check if robot has been bumped | Accelerometer |
| Measure pitch angle \(tilt up or down\) | Accelerometer |
| Measure roll angle \(tilt left or right\) | Accelerometer |
| Check if robot is upside down | Accelerometer |

{% hint style="info" %}
**OTHER POSSIBLE BEHAVIORS:**  There are other possible behaviors **not** listed in the table \(such as:  solving a maze, etc.\) that you could program your robot to perform.
{% endhint %}

{% hint style="info" %}
**ULTRASONIC SENSOR:** The SparkFun RedBot Kit does **NOT** include an ultrasonic sensor as a standard component. However, SparkFun sells the [HC-SR04 Ultrasonic Sensor](https://www.sparkfun.com/products/13959), which can be easily connected to a RedBot. Your teacher may have added this sensor to your kit.
{% endhint %}

