# Push Button \(D12\)

The RedBot mainboard has a built-in push button that can be detected by your program. The button is hardwired to pin D12 on the RedBot mainboard and is located next to the USB port.

The button can be used as a way for a user to interact with the robot \(e.g., pressing the button to "start" the robot, etc.\).

## How to Use Button

There are three different ways to use the D12 button in your robot app:

* **Option 1:**  Read the button pin directly using the `digitalRead()` method
* **Option 2:**  Read the button using a `RedBotButton` object and its `read()` method
* **Option 3:**  Use a `OneButton` object and its `tick()` method to detect different types of button presses \(i.e., single-press, double-press, and long-press\)

Option 1 and Option 2 are similar. They both detect when the button is pressed. It is primarily a matter of personal preference, in terms of which option to use. Most of the coding tutorials and references in this guidebook use the second option.

Option 3 is useful if you want to detect up to 3 different types of button presses, so you can have the robot perform different actions or tasks based on the user's input. This option requires you to include the `OneButton` library in your app. 

## Read Button Directly

To read the button pin directly, your robot app will need to:

1. Declare a variable to store the button pin number
2. Set the pin mode for the button
3. Use the `digitalRead()` method to detect whether the button is being pressed
4. Add code statement\(s\) to perform certain action\(s\) if the button is pressed

You'll need to create a global variable to store the pin number of the RedBot's built-in button, which is connected to pin D12 \(via internal circuitry\)

Add this code statement **before** the `setup()` function:

```cpp
int button = 12;
```

Next, you need to set the button's pin mode to identify whether it will act as an input or output.

Add this code statement **within** the `setup()` function:

```cpp
pinMode(button, INPUT_PULLUP);
```

`INPUT_PULLUP` indicates the button pin will be used for input and will use a pull-up resistor \(which is something that buttons and switches typically use, but other inputs do not\).

The `digitalRead()` method can be used to detect whether or not the button is currently being pressed. It will return a value of either `HIGH` or `LOW`:

* `HIGH` indicates the button is **NOT** being pressed
* `LOW` indicates the button is being pressed

An `if` statement is typically used to perform a set of actions when the button is pressed.

This code is typically added within the `loop()` function or a custom function:

```cpp
if (digitalRead(button) == LOW) {
    // add code to perform if button is pressed

}
```

**Alternatively**, you can also include an `else` statement to perform a different set of actions when the button is **not** pressed. In this case, use this code instead:

```cpp
if (digitalRead(button) == LOW) {
    // add code to perform if button is pressed

}
else {
    // add code to perform if button NOT pressed
    
}
```

## Use RedBotButton Object

To read the button using a `RedBotButton` object, your robot app will need to:

1. Create a `RedBotButton` object for the button
2. Use the object's `read()` method to detect whether the button is being pressed
3. Add code statement\(s\) to perform certain action\(s\) if the button is pressed

The SparkFun `RedBot` library has a class named `RedBotButton` which contains methods \(functions\) to control the RedBot's built-in D12 push button. This class will automatically set the pin number \(`12`\) and pin mode \(`INPUT_PULLUP`\) for the button.

Before the `setup()` function, create a `RedBotButton` object for the button by assigning the object to a variable:

```
RedBotButton button;
```

{% hint style="success" %}
**REDBOT LIBRARY:**  Be sure your robot app has an `#include` statement for the SparkFun RedBot library. [Here's how to include the RedBot library](../arduino-code-editor/include-redbot-library.md).
{% endhint %}

The `RedBotButton` object has a `read()` method that can be used to detect whether or not the button is currently being pressed. It will return a value of either `true` or `false`:

* `true` indicates the button is being pressed
* `false` indicates the button is **NOT** being pressed

An `if` statement is typically used to perform a set of actions when the button is pressed.

This code is typically added within the `loop()` function or a custom function:

```cpp
if (button.read() == true) {
    // add code to perform if button is pressed

}
```

**Alternatively**, you can also include an `else` statement to perform a different set of actions when the button is **not** pressed. In this case, use this code instead:

```cpp
if (button.read() == true) {
    // add code to perform if button is pressed

}
else {
    // add code to perform if button NOT pressed
    
}
```

## Use OneButton Object

The RedBot mainboard only has one button, which normally can only be read as being pressed or not pressed. However, the `OneButton` library makes it possible to detect three different types of button input events:

* **Single-Press** = user presses the button once
* **Double-Press** = user presses the button twice in rapid succession
* **Long-Press** = user presses and holds the button down

To read the button using a `OneButton` object, your robot app will need to:

1. Include the `OneButton` library
2. Create a `OneButton` object for the button
3. Designate custom functions for each type of button input
4. Add the code to be performed in each custom function
5. Use the object's `tick()` method to detect the type of button input

First, you must add a copy of the `OneButton.h` library to your code editor. This is a **one-time process**. [Follow the same steps that you did to add the RedBot library to your code editor](../arduino-code-editor/include-redbot-library.md#add-redbot-library-to-code-editor), except enter `onebutton` into the search field.

Next, you must include a copy of the `OneButton` library in your robot app. The following `#include` statement should be inserted at the beginning of your app code:

```cpp
#include <OneButton.h>
```

Before the `setup()` function, create a `OneButton` object by assigning it to a variable and indicating its pin number and whether it will use a pull-up resistor in parentheses:

```cpp
OneButton button(12, true);
```

Within the `setup()` function, you must designate the names of custom functions that will be called when the different button input events are detected \(single-press, double-press, or long-press\):

```cpp
  // designate custom functions for different button inputs
  button.attachClick(singlePress);
  button.attachDoubleClick(doublePress);
  button.attachPress(longPress);
```

If desired, you can use other names for the custom functions.

If you don't need to detect a specific type of button input, just leave it out \(or make it into a comment\). For example, if you don't need to detect a long-press, then simply exclude the code statement that attaches a custom function to that input event.

After the `loop()` function, add the custom functions for each type of button input:

```cpp
void singlePress() {
    // add code to perform when single-press detected

}

void doublePress() {
    // add code to perform when double-press detected

}

void longPress() {
    // add code to perform when long-press detected

}
```

Be sure the names of the custom functions match the names that were designated in the `setup()` function.

Inside each custom function, you need to add code for the specific actions you want performed when that type of button input is detected.

{% hint style="success" %}
**RECOMMENDED:** Provide feedback to confirm to the user which type of button input was detected. For example, the speaker \(and LED light\) could be could be used to mimic the input by producing a single-beep, double-beep, or long-beep.
{% endhint %}

### 5. Use `button.tick()` to Detect Button Input Events

In your `loop()` function, use the `OneButton` object's `tick()` method to check for button input events. Whenever a specific button input event is detected, the custom function that you previously designated will automatically be called.

```cpp
void loop() {

    button.tick(); // check for button input events

    // OPTIONAL: can add other code to perform

}
```

**NOTE:** If you used a different name for your `OneButton` object, then change `button` to match the name of your variable. For example, if you used `switch` as your object variable name, your code should use `switch.tick()` to detect button input events.

