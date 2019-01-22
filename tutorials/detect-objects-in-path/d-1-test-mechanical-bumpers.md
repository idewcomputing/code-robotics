# D-1 Test Mechanical Bumpers

First, you'll code an app to test your mechanical bumpers.

Be sure that you've first checked the positions of your wire whiskers and bumper boards to make any necessary physical adjustments. \(If necessary, refer back to the introduction for this tutorial.\)

## Save Copy of App With New Name <a id="save-copy-of-app-with-new-name"></a>

In your Arduino code editor, open your existing app named `pivot_angle_test`. Use the "Save As" command to save a copy as a different app named:  `mechanical_bumper_test`

Once you saved the new app name, modify the block comment near the beginning of the app code to change `Pivot Angle Test` to `Mechanical Bumper Test`.

## Create Objects for Bumpers

The SparkFun RedBot Library also defines a class named `RedBotBumper` that is used to control the left and right mechanical bumpers.

You'll need to create two new `RedBotMotors` objects for your left and right mechanical bumpers as part of the global variables in your app. Add this code **before** the `setup()` function:

```cpp
RedBotBumper leftBumper(3);
RedBotBumper rightBumper(11);
```

Hopefully, the format for create new objects is starting to look familiar:

* `RedBotBumper` declares the class for the new object.
* `leftBumper` and `rightBumper` represent unique names for each object. Again, you decide what to name your objects. They should make sense to anyone reading the code.
* `3` and `11` represent the I/O pin numbers that the left and right bumpers should be connected to. If your bumpers were connected to different pins, you'd change these pin numbers.

## Add Custom Function to Check Bumpers

You'll add another custom function named `checkBumpers()` which will contain code to check whether the left or right mechanical bumpers have collided with an obstacle.

The `RedBotBumper` class defines a method named `read()` which is used to detect whether or not a bumper has collided with an obstacle. Each bumper acts like a switch or button.

The `read()` method will return a value of either `HIGH` or `LOW`:

* If the value is `LOW`, it means the bumper has collided with an obstacle \(i.e., the wire whisker has bent backwards far enough to make electrical contact with the metal screw on the bumper board\).

Add this custom function **after** the `loop()` function \(i.e., after its closing curly brace\):

```cpp
void checkBumpers() {
  if (leftBumper.read() == LOW) {
    // add code if left whisker collides: brake, back up, turn right
    motors.brake();
    tone(speaker, 1000, 200);
    
  }
  else if (rightBumper.read() == LOW) {
    // add code if right whisker collides: brake, back up, turn left
    motors.brake();
    tone(speaker, 1000, 200);
    
  }
}
```

You can see that the custom function contains an if-else statement to check the left and right bumpers. If a collision is detected, the first response is to brake the motors \(which hopefully makes sense\). It will also use the speaker to produce an "alert" sound.

You'll also notice that this function uses an alternate form of the `tone()` method, which saves a bit of coding.  Notice that three parameters \(instead of just two\) are listed inside the parentheses:

* `speaker` represents the speaker's pin number \(which was declared as a global variable\)
* `250` represents the frequency of the tone \(which can be any value between 20-20000\)
* `200` represents the duration \(in milliseconds\) to play the tone. After the duration is over, the tone will automatically stop playing.

By including a **third** parameter for the duration of the tone, you **don't** have to include the `delay()` and `noTone()` code statements, which is convenient.

Later, you'll add other code within the function to make the robot perform additional actions \(such as backing up, etc.\) when a collision is detected.

{% hint style="success" %}
**KEEP OTHER CUSTOM FUNCTIONS:**  Be sure to keep the `driveDistance()` and `pivotAngle()` custom functions in your app code. You'll use these custom functions when you modify this app in the next step.
{% endhint %}

## Call Custom Function in Loop

You'll need to call the `checkBumpers()` function within the `loop()` function.

However, you first need to **delete all the existing code within** the `loop()` function \(including the "Press to Start" code that checks if the button is pressed\).

Then add a code statement to call the `checkBumpers()` function within the `loop()` function.

For reference, your `loop()` function should now look like this:

```cpp
void loop() {
  // put your main code here, to run repeatedly:
  checkBumpers();  
}
```

## Upload App to Robot

Follow the steps to connect your robot to your computer, and upload the app.

For this app, you don't have to unplug the USB cable. You can also just keep the robot standing upright on its back end \(with its wheels in the air\).

Use your finger to press down on the wire whisker of the left bumper. When the wire has bent far enough to touch the metal screw on the bumper board, you should hear a tone. If you release the whisker, the tone should stop. Repeat this test for the right bumper.



