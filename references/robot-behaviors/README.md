# Robot Behaviors

## Levels of Robot Behaviors

A robot behavior can be defined as any action that the robot can perform.  Robot behaviors can generally be categorized into different levels:

* **Basic Behaviors** – these are low-level behaviors that perform a single action, such as: turning on the motors, reading a sensor, etc.  In the robot's program, basic behaviors can be performed with a single code statement.
* **Simple Behaviors** – these are mid-level behaviors that perform a simple task, such as: driving forward for 5 seconds, turning to the right, etc. A simple behavior consists of a sequence of basic behaviors. In the robot's program, simple behaviors require several code statements.
* **Complex Behaviors** – these are high-level behaviors that perform a complex task, such as: following a line, driving around an obstacle, etc.  A complex behavior consists of a sequence of simple behaviors. In the robot's program, complex behaviors require multiple code statements, which are typically put into a custom function.

The exact distinction between a "simple" behavior and a "complex" behavior is not necessarily clear.  The value of thinking about different levels of robot behaviors is to simply recognize that behaviors can combined \(or broken down\) into other behaviors:

* **Composition:**  Lower-level behaviors can be combined into a sequence that produces a more complex behavior.
* **Decomposition:**  A higher-level behavior can be broken down into a sequence of more simple behaviors.

Understanding composition and decomposition can help you plan out the structure of your robot's program and figure out how to program the higher-level behaviors that you need to demonstrate your task scenarios.

## Types of Robot Behaviors

Here is a list of robot behaviors that the RedBot can perform that may be useful for coding your own robot program. There are also other behaviors **not** listed here \(such as:  solving a maze, etc.\) that you could program your RedBot to perform.

The robot behaviors in this list could be categorized into different types based on their purpose:

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

Again, there are other behaviors **not** listed here \(such as:  solving a maze, etc.\) that you could program your robot to perform.

{% hint style="info" %}
**ULTRASONIC SENSOR:** The SparkFun RedBot Kit does **NOT** include an ultrasonic sensor as a standard component. However, SparkFun sells the [HC-SR04 Ultrasonic Sensor](https://www.sparkfun.com/products/13959), which can be easily connected to a RedBot. Your teacher may have added this sensor to your kit.
{% endhint %}

