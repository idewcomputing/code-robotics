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

The SparkFun `RedBot` library has a class named `RedBotMotors` which contains methods \(functions\) to control the left and right motors.

Before the `setup()` function, create a `RedBotMotors` object by assigning it to a variable name:

```cpp
RedBotMotors motors;
```

{% hint style="success" %}
**REDBOT LIBRARY:**  Be sure your robot app has an `#include` statement for the SparkFun RedBot library. [Here's how to include the RedBot library](../arduino-code-editor/include-redbot-library.md).
{% endhint %}

## Driving

The RedBotMotors objects has several methods for driving the robot's motors.

The  `drive()` method rotates **both** motors to move the RedBot either forwards or backwards:

* When moving the RedBot forward, the right motor rotates clockwise \(CW\), while the left motor rotates counter-clockwise \(CCW\).
* When moving the RedBot backwards, the right motor rotates counter-clockwise \(CCW\), while the left motor rotates clockwise \(CW\).

Even though this might seem like the wheels would be moving in opposite directions, it actually makes the wheels move in the **same** direction because the wheels are oriented as mirror images of each other.

### Drive Both Motors

The `RedBotMotors` object has a `drive()` method that rotates both motors in order to drive the robot forward \(or in reverse\):

```cpp
motors.drive(power);
```

`power` represents the power applied to the motors, which can be any integer value between `-255` and `255`:

* Positive values drive the robot forward.
* Negative values drive the robot in reverse.
* A larger absolute value results in a faster speed \(i.e., `255` is the fastest speed for driving forward, `-255` is the fastest speed for driving in reverse, etc.\).

{% hint style="warning" %}
**NOT TOO FAST:** If you run the motors at a very high power, the wheels might "spin out" due to insufficient traction. If you notice this issue, use a lower motor power. In general, use a power of 200 or less, depending on the surface.
{% endhint %}

{% hint style="warning" %}
**NOT TOO SLOW:**  If you run the motors at a very low power, they may not have enough torque to actually rotate the wheels. If you notice this issue, use a higher motor power. In general, use a power of 50 or more, depending on the surface.
{% endhint %}

When driving both motors at the same power, you may notice that your RedBot drifts slightly to the left \(or right\), instead of driving in a perfectly straight line. If this occurs, it is because the motors are rotating at slightly different speeds, even though they are receiving the same amount of power.

If necessary, you can use the [wheel encoders](https://github.com/idewcomputing/code-robotics/tree/64cdad2dc649e653442a139dd557784bf73edac0/references/physical-outputs/wheel-encoders.md) to help adjust the left and right motor powers while the RedBot is driving, in order to make it drive in a straight line.

You can also drive the left and right motors independently by using different powers for each motor \(or even stopping one motor while the other keeps driving\). In certain situations, this may be useful. For example, this can be used to make the RedBot curve or turn.

### Drive Individual Motor

Use the `leftMotor()` method to drive just the left motor:

```cpp
motors.leftMotor(power);
```

* `power` represents the power applied to the left motor, which can be any integer value between `-255` and `255`.
  * Positive values rotate the left motor clockwise \(backwards\).
  * Negative values rotate the left motor counter-clockwise \(forwards\).
  * A larger absolute value results in a faster speed. \(`-255` and `255` are the fastest speeds. `-1` and `1` are the slowest speeds.\)

Alternatively, you can use the `leftDrive()` method, which does the exact **same** thing — except positive values are used to drive forwards \(and negative values are used to drive backwards\):

```cpp
motors.leftDrive(power);
```

* `power` represents the power applied to the left motor, which can be any integer value between `-255` and `255`.
  * Positive values rotate the left motor forwards \(counter-clockwise\).
  * Negative values rotate the left motor backwards \(clockwise\).
  * A larger absolute value results in a faster speed. \(`-255` and `255` are the fastest speeds. `-1` and `1` are the slowest speeds.\)

For example, if the left motor rotates counter-clockwise \(forwards\) while the right motor is stopped, the RedBot will turn clockwise \(to the right\).

#### Drive Right Motor

Use the `rightMotor()` method to drive just the right motor:

```cpp
motors.rightMotor(power);
```

* `power` represents the power applied to the right motor, which can be any integer value between `-255` and `255`.
  * Positive values rotate the right motor clockwise \(forwards\).
  * Negative values rotate the right motor counter-clockwise \(backwards\).
  * A larger absolute value results in a faster speed. \(`-255` and `255` are the fastest speeds. `-1` and `1` are the slowest speeds.\)

Alternatively, you can use the `rightDrive()` method, which does the exact **same** thing:

```cpp
motors.rightDrive(power);
```

* `power` represents the power applied to the right motor, which can be any integer value between `-255` and `255`.
  * Positive values rotate the right motor forwards \(clockwise\).
  * Negative values rotate the right motor backwards \(counter-clockwise\).
  * A larger absolute value results in a faster speed. \(`-255` and `255` are the fastest speeds. `-1` and `1` are the slowest speeds.\)

For example, if the right motor rotates clockwise \(forwards\) while the left motor is stopped, the RedBot will turn counter-clockwise \(to the left\).

**NOTE:** You can accomplish the same results using either the `drive()` method or by combining the `leftMotor()` and `rightMotor()` methods:

```cpp
motors.drive(150); // move forwards
/*  does same as:
    motors.leftMotor(-150);
    motors.rightMotor(150);
*/

motors.drive(-150); // move backwards
/*  does same as:
    motors.leftMotor(150);
    motors.rightMotor(-150);
*/
```

When driving both motors at the same power, you may notice that your RedBot drifts slightly to the left \(or right\), instead of driving in a perfectly straight line. If this occurs, it is because the motors are rotating at slightly different speeds, even though they are receiving the same amount of power.

If necessary, you can use the [wheel encoders](https://github.com/idewcomputing/code-robotics/tree/64cdad2dc649e653442a139dd557784bf73edac0/references/physical-outputs/wheel-encoders.md) to help adjust the left and right motor powers while the RedBot is driving, in order to make it drive in a straight line.

## Stopping

### Stop Both Motors

#### Brake Motors \(Abrupt Stop\)

The `brake()` method actively brakes **both** motors and causes the RedBot to abruptly stop.

#### Brake Both Motors

```cpp
motors.brake();
```

You can also brake the left and right motors independently. In certain situations, this may be useful.

#### Stop Both Motors

```cpp
motors.coast();
```

Alternatively, you can use the `stop()` method, which does the exact **same** thing:

```cpp
motors.stop();
```

You can also stop \(coast\) the left and right motors independently. In certain situations, this may be useful.

### Stop Individual Motor

#### Brake Left Motor

```cpp
motors.leftBrake();
```

#### Brake Right Motor

```cpp
motors.rightBrake();
```

The `coast()` method turns off **both** motors and allows the RedBot to coast to a stop.

#### Stop Left Motor

```cpp
motors.leftCoast();
```

Alternatively, you can use the `leftStop()` method, which does the exact **same** thing:

```cpp
motors.leftStop();
```

#### Stop Right Motor

```cpp
motors.rightCoast();
```

Alternatively, you can use the `rightStop()` method, which does the exact **same** thing:

```cpp
motors.rightStop();
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



