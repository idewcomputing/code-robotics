# C-3 Test Wheel Encoders

Next, you'll code an app to test your robot's wheel encoders by sending serial data to your computer.

## Wheel Encoders

Located directly behind each motor is a wheel encoder, which is a sensor that can count exactly how many times the motor has rotated. These left and right wheel encoder counts can be used to:

* **make the robot drive in a straight line** \(by adjusting the motor powers if one motor happens to be rotating slightly faster than the other\)
* **calculate how far the robot has driven** \(by determining how many times the wheel has rotated and multiplying that by the wheel circumference\)

The wheel encoder actually consists of two parts:

* a **Hall Effect sensor** that can measure the strength of a magnetic field
* a **ring magnet** \(looks like a metal washer\) attached to the motor shaft

![](../../.gitbook/assets/wheel-encoder.jpg)

When the motor rotates the wheel, it also rotates the ring magnet. The Hall effect sensor positioned near the ring detects changes in the magnetic field \(these are referred to as "ticks"\) as the ring rotates. This is how the wheel encoder can count how many times the motor has rotated.

## Check Wheel Encoder Alignments

In order to function accurately, each wheel encoder sensor must be positioned correctly, relative to its ring magnet. The sensor tip must be centered within the silver band of the ring magnet \(not too far inward or outward\) and must be close to the ring magnet's surface \(about ⅛" inch away\).

![How to Check Alignment of Wheel Encoder](../../.gitbook/assets/encoder-position.png)

Visually check the alignment of the left and right wheel encoders. If necessary, you might need to push \(or pull\) the sensor to position it correctly.

## Create New App

Open your Arduino code editor, and create a new app template.

Add a block comment at the beginning of the app code to identify your new app:

```cpp
/*
Wheel Encoder Test
Team Info
Teacher - Class Period
*/
```

## Include RedBot Library

[Follow the steps to include the SparkFun RedBot Library in your app](../../references/arduino-code-editor/include-redbot-library.md#include-redbot-library-in-app). \(You **don't** need to add the library to your code editor again — just include the library in this new app.\)

## Create Objects for Motors, Encoders, and Button

There are three classes defined in the RedBot library that you'll use in this app:

* `RedBotMotors` class — used to control the left and right motors
* `RedBotButton` class — used to control the built-in D12 button
* `RedBotEncoder` class — used to control the left and right wheel encoders

Your app will need to create new objects \(as global variables\) for these three classes. Add these code statements **before** the `setup()` function:

```cpp
RedBotMotors motors;
RedBotButton button;
RedBotEncoder encoder(A2, 10);
```

As you can see, the first code statement creates a `RedBotMotors` object named `motors`, which your app will use to control your left and right motors.

The second code statement creates a `RedBotButton` object named `button`, which your app will use to check whether the D12 button is pressed. We're doing this to show you another possible way to check the button. The difference is your code **won't** need to identify the button's pin number and **won't** need to set the button's pin mode — because the `RedBotButton` object does this automatically when it is created. In addition, the code statement that you'll use to read the button is slightly different \(as you'll see later\).

The third code statement creates a `RedBotEncoder` object named `encoder`, which your app will use to control both wheel encoders. This code statement does three things \(in order\):

1. **It declares the class for the object.**  This is similar to declaring a data type for a variable. In this case, `RedBotEncoder` is the name of the class in the RedBot library being used to create the new object.
2. **It declares the object's name.** In this case, the object will be named `encoder`. Just like with other variables, you get to decide what to name your objects.
3. **It indicates the I/O pin numbers for the encoders.** In this case, `A2` is the I/O pin used by the left wheel encoder, and `10` is the I/O pin used by the right wheel encoder.

## Begin Serial Communication

When your robot and computer are connected with a USB cable, they can communicate with each other by transferring serial data.

In this app, your robot will send data from the wheel encoders to your computer. Your Arduino code editor has a serial monitor window that can be used to view this serial data communication.

Add this code statement **within** the `setup()` function:

```cpp
Serial.begin(9600);
```

This starts the serial data communication and sets the data transfer rate to 9600 bits per second.

## Add Custom Function to Test Wheel Encoders

As you've learned, every Arduino app must have one `setup()` function and one `loop()` function. In addition, you can add your own custom functions to your app.

A custom function is typically used to contain code that performs a specific task or subtask. Custom functions are useful for breaking up your app into smaller code modules that are easier to understand and easier to re-use.

Custom functions are typically listed after the `loop()` function. Each custom function added to your app must be given a unique name to identify it. You get to decide what to name your custom functions, but choose names that will make sense to anyone reading your code. \(The same rules and recommendations for naming variables apply to naming functions\).

In this case, you'll add a custom function that contains all the code to perform a test of the wheel encoders. The function will be named `testWheelEncoders()`.

Add this custom function **after** the `loop()` function \(i.e., after its closing curly brace\):

```cpp
void testWheelEncoders() {

    // when button is pressed, reset encoder counters and start motors
    if (button.read() == true) {
        encoder.clearEnc(BOTH);
        motors.drive(150);
    }
    
    // get current encoder counts
    long leftCount = encoder.getTicks(LEFT);
    long rightCount = encoder.getTicks(RIGHT);

    // send data to serial monitor
    Serial.print("Left: ");
    Serial.print(leftCount);
    Serial.print("\t"); // insert tab
    Serial.print("Right: ");
    Serial.println(rightCount);

    // if either count reaches 1000, brake motors
    if (leftCount >= 1000 || rightCount >= 1000) {
        motors.brake();
    }
}
```

In line 4 above, you can see that the code statement used to check whether the built-in D12 button is pressed is slightly different when you use a RedBotButton object:

* The `RedBotButton` object named `button` has a `read()` method that can be used to detect whether or not the button is being pressed.
* If the `button.read()` method returns a value equal to `true`, it means the button is pressed. \(Otherwise, a value of `false` means the button is **not** pressed.\)

When the button is pressed, two things will occur:

* Both wheel encoder counters will be reset back to zero by using the code statement: `encoder.clearEnc(BOTH);`
* Both motors will start driving at a power of 150.

Then two local variables called `leftCount` and `rightCount` are declared.  Each variable has a data type of [`long`](https://www.arduino.cc/reference/en/language/variables/data-types/long/) \(special type of integer\) because that's what the wheel encoders use. The value assigned to each of these variables is the current encoder count \(i.e., the number of magnetic "ticks" counted\) returned by the `encoder.getTicks()` method.

Then the wheel encoder data is sent to the computer using `Serial.print()` statements. This is the data that will be displayed in the computer's serial monitor window.

Finally, if either the left or right encoder count reaches 1000 or higher \(which will happen after the motors have been driving for a few seconds\), the motors will be braked.

## Call Custom Function in Loop

The code within a custom function is only performed if the custom function is "called" by its name within another function, such as the `setup()` function or `loop()` function.

Add this code statement **within** the `loop()` function:

```cpp
testWheelEncoders();
```

By listing the name of the custom function, the custom function is "called" — so the code within that custom function will be performed one time.

For this app, this will be only code statement listed within the `loop()` function. Since the `loop()` function repeats itself continuously, the `testWheelEncoders()` function will be called repeatedly.

## Upload App

Connect your robot to your computer using the USB cable. Be sure the robot is standing upright on its back end \(with its wheels in the air\), so the robot won't drive way while it's connected to your computer.

Turn on your robot, and upload the app to your robot. After the upload is complete, do **not** unplug the USB cable. You have to keep the robot connected to your computer to allow the serial data communication.

## View Data in Serial Monitor

In your Arduino code editor, open the serial monitor, so you can view the serial data communication from your robot:

* **Arduino Create \(Web Editor\):**  Click the **Monitor** menu link in the left navigation to display the serial monitor in the middle panel.
* **Arduino IDE \(Desktop Editor\):**  Under the **Tools** menu, select "Serial Monitor." A new window will appear displaying the serial monitor.

Press the D12 button on your robot's circuit board. Your robot's wheels should start driving. In the serial monitor, view the data showing the wheel encoder counts.  When either one of the wheel encoder counts reaches 1000 \(which should take about 3-4 seconds\), the motors will brake.

Each line of serial data \(one set of left and right encoder counts\) represents the `testWheelEncoders()` function being performed one time. Each time the `loop()` function repeats, it calls the custom function, which sends another line of serial data to the serial monitor.

You'll probably notice that the wheel encoder counts do **not** stop exactly at 1000. This is normal —  it takes a brief amount of time for the braking to occur. The final counts should be less than 1050.

You'll probably notice that your left and right wheel encoder counts are **not** exactly the same. This is normal — they should be close to each other \(within about 25\), but they probably won't be identical.

If one or both wheel encoders are **not** working properly \(the count stays at zero\), then turn off the robot's power, and check the wheel encoder alignment again. After correcting the alignment, turn the robot's power back on to restart the app.

{% hint style="success" %}
**CHECK ENCODERS AFTER CHANGING BATTERIES:**  Whenever you change the robot's batteries, be sure to check the wheel encoder alignments **afterwards**. It's very common to accidentally move the wheel encoder sensors when changing the battery pack.
{% endhint %}





