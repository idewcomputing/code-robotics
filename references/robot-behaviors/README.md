# Robot Behaviors

A robot behavior can be defined as any action that the robot can perform. It can be helpful to think about robot behaviors in terms of their **level** \(depends on complexity of behavior\) and **type** \(depends on purpose of behavior\).

## Levels of Robot Behaviors

Robot behaviors can generally be categorized into different levels of complexity:

* **Basic Behaviors** – these are low-level behaviors that perform a single action, such as: turning on the motors, reading a sensor, etc. In the robot's program, basic behaviors can be performed with a single code statement.
* **Simple Behaviors** – these are mid-level behaviors that perform a simple task, such as: driving forward for 5 seconds, turning to the right, etc. A simple behavior consists of a sequence of basic behaviors. In the robot's program, simple behaviors require several code statements.
* **Complex Behaviors** – these are high-level behaviors that perform a complex task, such as: following a line, driving around an obstacle, etc.  A complex behavior consists of a sequence of simple behaviors. In the robot's program, complex behaviors require multiple code statements, which are often put into a custom function.

The value of thinking about different levels of robot behaviors is to simply recognize that behaviors can combined \(or broken down\) into other behaviors:

* **Composition:**  Lower-level behaviors can be combined into a sequence that produces a more complex behavior.
* **Decomposition:**  A higher-level behavior can be broken down into a sequence of more simple behaviors.

Understanding composition and decomposition can help you plan out the structure of your robot's program and figure out how to program the higher-level behaviors that you need to demonstrate your task scenarios.

## Types of Robot Behaviors

Robot behaviors can also be categorized into different types based on their purpose. This guidebook has grouped robot behaviors into the following categories:

* [Producing Alerts](producing-alerts.md)
* [Driving](driving.md)
* [Turning](turning.md)
* [Detecting Objects](detecting-objects.md)
* [Detecting Lines](detecting-lines.md)
* [Detecting Other Conditions](detecting-other-conditions.md)

There are other behaviors **not** included in this code guidebook that you could program your robot to perform. For example, you could [program your robot to solve mazes](https://www.instructables.com/id/Robot-Maze-Solver/), etc.

