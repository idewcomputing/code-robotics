# Motors

The RedBot is a two-wheeled robot. It also has a semi-circular plastic "nub caster" on the underside of its chassis at the back. This caster acts as a third point of contact to balance the robot \(similar to a third wheel, except the caster doesn't rotate\).

Each wheel is driven by its own motor, which is connected to the RedBot circuit board by a pair of red and black wires. These left and right motors can be controlled as a set or independently, in order to make the robot drive forward, backwards, or make turns.

You can also determine how much power each motor receives, in order to rotate the wheels faster or slower, to control the speed of your robot as it drives and turns.

![Motors](../../.gitbook/assets/redbot-motors.jpg)

## How to Code Motors

To use the motors in your robot app, you will need to:

1. Create `RedBotMotors` object for the motors
2. Use the object's methods to control the motors:  `drive()`, `brake()`, `pivot()`, etc.

## Create RedBotMotors Object

The SparkFun `RedBot` library has a class named `RedBotMotors` which defines methods \(functions\) to control the left and right motors.

Before the `setup()` function, create a `RedBotMotors` object by assigning it to a variable name:

```cpp
RedBotMotors motors;
```

{% hint style="success" %}
**REDBOT LIBRARY:**  Be sure your robot app has an `#include` statement for the SparkFun RedBot library. [Here's how to include the RedBot library](../arduino-code-editor/include-redbot-library.md).
{% endhint %}

## Driving

The `RedBotMotors` object has several methods for driving the robot's motors forward \(or in reverse\). Both motors can be driven together, or each motor can be driven separately:

* `drive()` — drives both motors
* `leftDrive()` or `leftMotor()` — drives the left motor only
* `rightDrive()` or `rightMotor()` – drives the right motor only

Each of these methods requires a **motor power** to be listed within the parentheses. The motor power can be can be any integer value \(whole number\) between `-255` and `255`:

* **Positive** values drive the robot **forward**.
* **Negative** values drive the robot in **reverse**.
* A **larger absolute value** produces a **faster speed** \(i.e., `255` is the fastest speed for driving forward, `-255` is the fastest speed for driving in reverse, etc.\).

{% hint style="warning" %}
**ONE EXCEPTION TO RULE:**  The `leftMotor()` method works differently. Positive values rotate the left motor clockwise, which is actually in reverse. Negative values rotate the left motor counterclockwise, which is forward.
{% endhint %}

For example, to drive both motors forward at a power \(speed\) of 150: 

```cpp
motors.drive(150);
```

For example, to drive both motors in **reverse** at a power \(speed\) of 100: 

```cpp
motors.drive(-100);
```

For example, to drive just the **left** motor forward at a power \(speed\) of 125: 

```cpp
motors.leftDrive(125);
```

{% hint style="info" %}
**KEEP ON DRIVING:**  Once a code statement is used to start one or both motors driving, the motor\(s\) will keep driving at that same power until another code statement is used to **stop** the motor\(s\).
{% endhint %}

#### NOT TOO FAST – AND NOT TOO SLOW

If you run the motors at a **very high power**, the wheels might "spin out" due to insufficient traction with the surface. If you notice this issue, use a lower motor power. In general, use a motor power of 200 or less, depending on the surface.

If you run the motors at a **very low power**, they might not have enough torque to actually rotate the wheels. If you notice this issue, use a higher motor power. In general, use a motor power of 50 or more, depending on the surface.

#### DRIFTING WHILE DRIVING

When driving both motors, you may notice your robot drifts slightly to the left \(or right\), instead of driving in a perfectly straight line. This is actually a common occurrence with independent wheel drive vehicles. This happens because the motors are rotating at slightly different speeds, even though they may be receiving the same amount of power.

If necessary, there are custom functions that use the wheel encoders to adjust the left and right motor powers while the robot is driving, in order to make it [drive in a straight line](../robot-behaviors/driving.md).

## Stopping

The `RedBotMotors` object has several methods for stopping the robot's motors. Both motors can be stopped together, or each motor can be stopped separately:

* `brake()` — abruptly stops both motors \(quick braking\)
* `coast()` or `stop()` — stops both motors \(coast to a stop\)
* `leftBrake()` — abruptly stops the left motor only
* `rightBrake()` — abruptly stops the right motor only
* `leftCoast()` or `leftStop()` – stops the left motor only
* `rightCoast()` or `rightStop()` – stops the left motor only 

For example, to brake both the motors:

```cpp
motors.brake();
```

For example, to stop just the **left** motor: 

```cpp
motors.leftStop();
```

## Turning

There are several ways to turn the RedBot left or right, depending on how tight the turn needs to be. The RedBot is capable of pivoting on both wheels, which results in a "zero turn radius" \(tightest possible turn\).

| Type of Turn | How Turn Works |
| :--- | :--- |
| Pivot on Both Wheels | Both wheels rotate in **same** direction \(both CW or both CCW\) at **same** motor power |
| Turn on One Wheel | Only one wheel rotates \(either CW or CCW\) while other wheel is **stopped** |
| Gentle Turn | Wheels rotate in **opposite** directions \(one CW and other CCW\) at **different** motor powers |

Here is a visual comparison of pivoting on both wheels versus turning on one wheel:

![](../../.gitbook/assets/pivot-both-vs-turn-one.png)

### Pivot on Both Wheels

The `pivot()` method results in a perfectly tight turn, as the RedBot's axis of rotation is centered between its wheels. As a result, the RedBot doesn't move forward while pivoting.

The `pivot()` method rotates **both** motors to pivot \(turn\) the RedBot either clockwise \(to the right\) or counter-clockwise \(to the left\):

* When pivoting the RedBot clockwise \(to the right\), both motors rotate counter-clockwise \(CCW\) at the same power.
* When pivoting the RedBot counter-clockwise \(to the left\), both motors rotate clockwise \(CW\) at the same power.

To pivot \(either clockwise or counter-clockwise\):

```cpp
motors.pivot(power);
```

* `power` represents the power applied to the motors, which can be any integer value between `-255` and `255`.
  * Positive values pivot the RedBot clockwise \(to the right\).
  * Negative values pivot the RedBot counter-clockwise \(to the left\).
  * A larger absolute value results in a faster speed. \(`-255` and `255` are the fastest speeds. `-1` and `1` are the slowest speeds.\)

**IMPORTANT:** Use a lower power when pivoting the RedBot, as compared to driving the RedBot. A power of about 100 should be sufficient to quickly pivot on most surfaces.

**NOTE:** You can accomplish the same results using either the `pivot()` method or by combining the `leftMotor()` and `rightMotor()` methods:

```cpp
motors.pivot(100); // turn CW to right
/*  same as:
    motors.leftMotor(-100);
    motors.rightMotor(-100);
*/

motors.pivot(-100); // turn CCW to left
/*  same as:
    motors.leftMotor(100);
    motors.rightMotor(100);
*/
```

### Turn on One Wheel

Alternatively, you can turn the RedBot on one wheel by driving only one motor forward while stopping the other motor.

This will help retain more of the RedBot's forward momentum \(whereas pivoting requires the RedBot to stop moving forward\). However, the turn radius will be larger compared to using the `pivot()` method because the RedBot's axis of rotation is centered on the stopped wheel.

```cpp
// turn CW to right
motors.leftDrive(100);
motors.rightStop();

// turn CCW to left
motors.leftStop();
motors.rightDrive(100);
```

### Drive in Curve

Furthermore, you can make gentle turns or curves by simply applying different amounts of power to the two motors:

* Applying more power to the **left motor** will cause the RedBot to curve to the **right**.
* Applying more power to the **right motor** will cause the RedBot to curve to the **left**.
* A larger difference in the motor powers will make the RedBot curve more sharply, while a smaller difference will make the RedBot curve more gently.

This will help maintain even more of the RedBot's forward momentum, compared to turning on one wheel \(which is an extreme version of using different motor powers that applies a power of zero to one wheel\).

```cpp
// curve to left
motors.leftMotor(-100);
motors.rightMotor(150);

// curve to right
motors.leftMotor(-150);
motors.rightMotor(100);

// curve to right more sharply
motors.leftMotor(-175);
motors.rightMotor(100);

// curve to right more gently
motors.leftMotor(-125);
motors.rightMotor(100);
```



