# C-1 Driving

#### **STILL IN PROGRESS**

## Create New App Template

If necessary, log in to the Arduino Create web editor, or open the Arduino IDE desktop editor.

Create a new app template. If you need a reminder, here are [instructions for creating a new app template](../../references/arduino-code-editor/create-new-app.md).

## Rename App

Rename the the new app as:  `driving_test`

If you need a reminder, here are [instructions for how to rename an app](../../references/arduino-code-editor/save-and-rename-app.md).

## Add Block Comment

Add this block comment at the beginning of your app code. Modify the comment to list your information.

```cpp
/*
Driving Test App
Team 3 - Destiny, Katya, Lucas, Miguel
Ms. Hopper - Period 2
*/
```

## Include RedBot Library

Arduino apps can include one or more libraries. A library is a pre-built code file that makes it easier to program certain things in your app.

There is a **SparkFun RedBot Library** that makes it much easier to control the motors and sensors connected to your RedBot.

You will need to add a copy of the SparkFun RedBot Library to your code editor, which is a **one-time process**. Then you will also need to include a copy of this library in **each new robot app**.

[Follow these instructions to \(1\) add the SparkFun RedBot Library to your code editor, and \(2\) include the library in your current app](../../references/arduino-code-editor/include-library-in-app.md).

You should now have an `#include` statement for the RedBot library \(filename: `RedBot.h`\) listed at the beginning of your app code.

## Create RedBotMotors Object

The `RedBot.h` library contains Arduino code that defines different classes of objects. Each class defines a set of **properties** \(variables\) and **methods** \(functions\) for a specific type of object.

Your robot apps will use these classes to create objects in your app code. An object is a special type of variable that represents a specific **instance** \(member\) of a class. An object has all the properties and methods defined for that class.

The objects in your robot app code will correspond to real-life parts on your robot \(such as:  motors, wheel encoders, mechanical bumpers, etc.\).

One of the classes in the RedBot library that you'll use in your apps is the `RedBotMotors` class, which defines methods to control your robot's left and right motors.

You'll need to create a new `RedBotMotors` object as a global variable in your app, so you can use this object to control your robot's motors. Add this code statement **before** the `setup()` function:

```cpp
RedBotMotors motors;
```

This code statement does two things \(in order\):

1. **It declares the class for the object.**  This is similar to declaring a data type for a variable. In this case, `RedBotMotors` is the name of the class in the RedBot library being used to create the new object.
2. **It declares the object's name.** In this case, the object will be named `motors`. Just like with other variables, you get to decide what to name your objects. Choose a name that will make sense to anyone reviewing your code.

## Add Code for "Press to Start"

As a reminder, whenever you upload a new app to your robot, the new app starts running **immediately** \(even before you've had a chance to unplug the USB cable from your robot\). In a worst-case scenario, your robot might accidentally drive off the edge of your desk and crash onto the floor.

Therefore as a safety feature, most of the robot apps in these tutorials will use an `if` statement within the `loop()` function to check whether the D12 button on the circuit board has been pressed before making the robot drive around. When the button is pressed, the speaker and built-in LED will beep and blink as a confirmation before performing the other robot actions \(such as driving, etc.\).

Create global variables for the LED pin, speaker pin, and button pin by adding this code **before** the `setup()` function: 

```cpp
int LED = 13;
int speaker = 9;
int button = 12;
```

Set the pin modes for the LED, speaker, and button by adding this code **within** the `setup()` function:

```cpp
    pinMode(LED, OUTPUT);
    pinMode(speaker, OUTPUT);
    pinMode(button, INPUT_PULLUP);
```

Check whether the button has been pressed by adding this code **within** the `loop()` function:

```cpp
  if (digitalRead(button) == LOW) {
    // code to perform when button is pressed
    digitalWrite(LED, HIGH);
    tone(speaker, 2000);
    delay(200);
    digitalWrite(LED, LOW);
    noTone(speaker);
    // add code for other robot actions (driving, etc.)
    
  }
  delay(200);
```

Basically, this code for "Press to Start" is the same as the final version of the "Hello World" app you completed in the previous tutorial.

## Drive Forward

The `RedBotMotors` class defines a method named `drive()` that can be used to drive the motors either forward or backwards. The `RedBotMotors` class also defines a method named `brake()` that can be used to stop the motors.

Therefore, your `motors` object also has the `drive()` method and the `brake()` method \(as well as all the other methods defined in the `RedBotMotors` class\).

When the `drive()` method is used in your code, the motors will start driving and will stay on \(sort of like cruise control on a car\). Then you'll use the `delay()` method to wait for a certain period of time before turning the motors off with the `brake()` method.

When the robot's button is pressed, let's make your robot drive forward for 2 seconds and then brake. Add this code **within** the `if` statement in the `loop()` function \(**after** the `noTone()` statement\):

```cpp
    motors.drive(200);
    delay(2000);
    motors.brake();
```

The `drive()` method requires one parameter inside its parentheses:

* **The motor power**, which can be any integer \(whole number\) between `-255` and `255`. A positive power drives the robot forward, and a negative power drives the robot backwards. A larger absolute power produces a faster speed \(`-255` and `255` are the fastest speeds, while `-1` and `1` are the slowest speeds\). In this case, the motor power will be set to `200`.

{% hint style="danger" %}
**SLOW DOWN:**  Driving the motors at high power can sometimes cause the wheels to "spin out" due to insufficient traction with the surface. If you notice traction issues, use a lower motor power \(slower speed\). In general, use a motor power of 200 or less.
{% endhint %}

## Upload App to Robot

[Follow the steps to upload the app to your robot](../../references/arduino-code-editor/upload-app-to-robot.md):

1. Connect Robot to Computer
2. Turn on Robot Power
3. Select Correct Board and Port
4. Upload App to Robot

Unplug the USB cable from the robot, and place the robot on the floor. Be sure a path of at least 3 feet in front of the robot is clear of any obstacles. \(Just to be safe, also be sure a path of 3 feet **behind** the robot is clear — in case your robot's motor wires were accidentally reversed during assembly.\)

Press the D12 button on your robot's circuit board. Your robot should beep and then drive forward about 30 inches.

#### TROUBLESHOOTING

* **If your robot doesn't drive at all**, first check that its **Motor** switch is set to **RUN**. If the switch was correct, next check the left and right motor wires on the circuit board to verify the red and black wires are correctly plugged in. If the wires were correct, replace the batteries in the robot's battery pack.
* **If your robot spins clockwise \(to the right\)**, unplug and reverse the red and black wires of the right motor on the circuit board.
* **If your robot spins counter-clockwise \(to the left\)**, unplug and reverse the red and black wires of the left motor on the circuit board.
* **If your robot drives backwards**, first check your app code to make sure you used a positive value for the motor power \(**not** a negative value\). If the app code is correct, unplug and reverse the red and black wires for each motor on the circuit board.

**NOTE:**  If your robot drives forward but **not** in a perfectly straight line, this is actually normal. Even though the two motors are supposed to be identical and are receiving identical power, they might not necessarily rotate at the exact same rate. Even a minor difference in their rotation rates will cause the robot to drift either to the left or to the right as it drives \(depending on which motor is rotating more slowly\).

Later in this tutorial, you'll use the wheel encoders to continuously measure the rotation rates of the motors, in order to make small power adjustments to each motor so the robot will drive in a straight line.

## Drive Backwards \(Reverse\)

Next you'll modify the app so the robot will drive forward for 2 seconds, stop briefly, drive backwards for 2 seconds, and finally stop approximately at its starting point.

Add this code **within** the `if` statement in the `loop()` function \(**after** the `motors.brake()` statement\):

```cpp
    delay(1000); // pause for 1 second
    motors.drive(-200); // drive backwards
    delay(2000);
    motors.brake();
```

Upload the modified app to your robot. Unplug the USB cable from the robot, and place the robot on the floor. Be sure a path of at least 3 feet in front of the robot is clear of any obstacles.

Press the D12 button on your robot's circuit board. Your robot should beep and then drive forward about 30 inches. It should stop and pause for 1 second before driving backwards about 30 inches.

