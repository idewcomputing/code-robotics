# B-8 Use Button

As your last step of this tutorial, you'll modify the "Hello World" app so your robot's LED and speaker will "blink" and "beep" whenever the D12 button on the robot's circuit board is pressed.

## Add Global Variable for Button <a id="add-global-variable-for-speaker"></a>

You'll need to create a global variable to store the pin number of the RedBot's built-in button, which is connected to pin D12 \(via internal circuitry\)

Add this code statement **before** the `setup()` function:

```cpp
int button = 12;
```

Your code should now have three separate code statements **before** the `setup()` function to declare a global variable for the LED, a global variable for the speaker, and a global variable for the button. 

## Set Pin Mode for Button

The button is an example of an input because your app will use it to receive data \(i.e., to detect when someone presses the button\). So you'll need to set the pin mode for the button to be an input.

Add this code statement **within** the `setup()` function:

```cpp
pinMode(button, INPUT_PULLUP);
```

`INPUT_PULLUP` indicates that the button pin will be used for input and will also use a pull-up resistor \(which is something that buttons and switches typically require, but other inputs do not\).

Your code should now have three separate code statements **within** the `setup()` function to set the pin mode for the LED,  set the pin mode for the speaker, and set the pin mode for the button.

## Check If Button Pressed

Your app can **receive signals from inputs** using the `digitalRead()` or `analogRead()` methods, depending on whether the values being received will be digital or analog.

{% hint style="info" %}
**DIGITAL VS. ANALOG:** Digital inputs and outputs use **binary values** \(such as: HIGH vs. LOW, etc.\). Analog inputs and outputs use a **range of values** \(such as: 0-255, etc.\)
{% endhint %}

The button can be read as a **digital input** that is either "pressed" or "not pressed."

Your app will need to use an [`if`](https://www.arduino.cc/reference/en/language/structure/control-structure/if/) statement and the `digitalRead()` method to check if the button is being pressed. Add this code **within** the `loop()` function \(**before** the first `digitalWrite()` statement that turns on the LED\):

```cpp
  if (digitalRead(button) == LOW) {
    // add code to perform when button is pressed
    
  }
```

The `digitalRead()` method requires one parameter insides its parentheses:

1. **The I/O pin number**, which can be the actual pin number \(such as: `12`, etc.\) or a variable that stores a pin number. In this case, the variable named `button` is listed \(which has a value equal to `12`\).

The `digitalRead()` method will check the button and return a value of either `HIGH` or `LOW`:

* `HIGH` indicates the button is **NOT** currently pressed.
* `LOW` indicates the button is currently pressed.

An `if` statement checks whether a specific condition \(listed insides its parentheses\) is true or false.

In this case, the condition being checked is whether the value returned from `digitalRead(button)` is equal to `LOW`:

* If this condition is **true**, the app will perform whatever code statements are listed within the curly braces of the `if` statement.
* If this condition is **false**, the app will **not** perform the code statements within the curly braces of the `if` statement.

Here's what we want to happen:  if the button is pressed, the LED will blink and the speaker will beep at the same time. 

To do that, you're going to move the existing code statements in the `loop()` that make the LED blink and speaker beep, so those code statements are now listed **within** the curly braces of the `if` statement.

1. Select the code statements to be moved, cut them \(choose "Cut" from **Edit** menu – or press Control-X on keyboard\), and then paste them in their new location \(choose "Paste" from **Edit** menu – or press Control-V on keyboard\).
2. You may want to use the tab key to indent the code statements that you moved \(so it is more visually clear that they are contained within the curly braces of the `if`statement\).
3. Modify the **second** `delay()` method, so the delay is `200` milliseconds. This will act as a 0.2 second pause between each check of the button \(to allow sufficient time for a person to release the button, so the code doesn't read a single button press as if it were multiple presses\).

Just for reference, here's what your `loop()` function should now look like:

```cpp
void loop() {
  // put your main code here, to run repeatedly:
  if (digitalRead(button) == LOW) {
    // add code to perform when button is pressed
    digitalWrite(LED, HIGH);
    tone(speaker, 2000);
    delay(200);
    digitalWrite(LED, LOW);
    noTone(speaker);
    delay(200);
  }
}
```

## Upload Modified App to Robot

Upload the modified app to your robot, confirm that it works correctly.

The robot's LED and speaker should briefly blink and beep \(in sync\) only when you press the D12 button on the RedBot circuit board.

If your teacher requires you to submit a file containing your completed "Hello World" app code, [follow these instruction to download a copy of your app](../../references/arduino-code-editor/download-copy-of-app.md).

In the next tutorial, you'll program apps to make your robot drive around and make turns.



