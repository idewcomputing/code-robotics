# B-3 Global Variable

Let's add a variable in your app code to represent the built-in LED light.

## Add Global Variable for LED

Your "Hello World" app will make the RedBot circuit board's built-in green LED light turn on and off in a blinking pattern. This will be accomplished by sending separate "on" and "off" signals to the LED's pin.

Each I/O pin on the RedBot circuit board is identified by a pin number \(such as: A0, A1, A2, 3, 9, 10, etc.\). In this case, the RedBot's built-in green LED light is connected to pin D13 \(via internal circuitry\).

When coding an Arduino app, you will typically create global variables to store the pin numbers for the inputs and outputs connected to your circuit board that you want to control. This will help make your code easier to understand because the variable names help identify each input or output.

You'll need to "declare" \(create\) a global variable to store the pin number of the built-in LED. Add this code statement to your app by inserting it \(as a separate line of code\) **before** the `setup()` function:

```cpp
int LED = 13;
```

{% hint style="success" %}
**HOW TO COPY CODE:** When using this IoT code guidebook, you can copy a code block simply by clicking the **copy icon** displayed in the upper right of the code block.
{% endhint %}

This code statement does 3 things \(in order\):

1. **It declares a data type for the variable's value.**  In this case, `int` stands for integer \(whole number\). Arduino pin numbers are always treated as `int` values \(even if they contain letters\).
2. **It declares the variable's name.** In this case, the variable will be called `LED`. You get to decide what to name your variables. Choose names that will make sense to anyone reviewing your code.
3. **It assigns a value to the variable.**  In this case, the variable's value will be equal to `13`, which is the pin number for the RedBot's built-in LED light.

Notice that this code statement ends with a [semi-colon](https://www.arduino.cc/reference/en/language/structure/further-syntax/semicolon/). Typically, each code statement in your app will end with a semi-colon. The semi-colon separates code statements, similar to how periods separate sentences in written English.

* The exceptions to ending with a semi-colon are certain statements \(such as functions, conditionals, loops, etc.\) that use [curly braces](https://www.arduino.cc/reference/en/language/structure/further-syntax/curlybraces/) to enclose other code statements. However, within the curly braces, each code statement will end with a semi-colon.

Although you can actually list multiple code statements on the same line \(because their semi-colons will separate them\), each code statement is traditionally listed on its own separate line to make it easier to read the code.

## Save Your App Code

The Arduino code editor does **NOT** autosave as you type, so be sure to periodically save your code.

#### Arduino Create \(Web Editor\)

At the top of the code editor panel, hover your mouse cursor over the button with 3 dots, and then select "Save" from the pop-up menu.

#### Arduino IDE \(Desktop Editor\)

Under the **File** menu, select "Save" – alternatively, you can click the **Save** icon \(looks like a downward arrow\) at the top of the code editor window.

{% hint style="success" %}
**TURN ON AUTOSAVE:**  You can turn on autosave in the Arduino Create web editor \(but **not** the desktop editor\). Click the Preferences menu in the left navigation to display its menu options. Be sure "Enable Autosave" and "Save when verifying and uploading" are both checked.
{% endhint %}

## Tips for Naming Variables

You get to decide what to name each variable in your app's code. However, here are a few rules and recommendations to help you name your variables:

#### RULES

* Each global variable must have a unique name.
* A variable's name **cannot** be one of the [keywords in the Arduino programming language](https://www.arduino.cc/reference/en/).
* Variable names must be one word \(no spaces allowed\).
* Variable names can contain lowercase letters, uppercase letters, numbers, and certain special characters \(such as underscores, etc.\) – but the name **cannot** start with a number.

#### RECOMMENDATIONS

* Make each variable's name concise yet descriptive, so it will be easy to read and understand.
  * Example of variable name that's concise yet descriptive:  `LED`
  * Example of variable name that's **too** concise:  `L`
  * Example of variable name that's **too** descriptive:  `greenD13LEDlight`
* If your variable name combines multiple words, you can make the name easier to read by either using an underscore between words – or using "[camelCase](https://en.wikipedia.org/wiki/Camel_case)" \(lowercase letters, but new words start with an uppercase letter\).
  * Examples of variable name using underscore:  `push_button`
  * Examples of variable name using camelCase:  `pushButton`
* If you have multiple inputs or outputs of the same type \(mechanical bumpers, IR line sensors, etc.\), add an adjective \(or number\) to their variable names to help identify them in your app code.
  * Examples of variable names using adjectives:  `leftBumper`, `rightBumper`

