# B-4 Setup Function

Next you'll add a command in your app code to designate the LED pin as an output.

## Set Pin Mode for LED

A variety of inputs and outputs can be connected to the I/O pins on your RedBot circuit board. Your app code needs to identify which I/O pins you are using and whether each of these pins will be used for an input or output. This is referred to as **setting the pin modes**.

Setting the pin modes for your inputs and outputs only needs to occur **one time** when your app first starts to run, so the code statements to do this should be added within the `setup()` function.

So you'll need to set the pin mode for the built-in LED that you'll be using. Add this code statement **within** the `setup()` function \(between the curly braces\):

```cpp
pinMode(LED, OUTPUT);
```

The `pinMode()` method requires two parameters inside its parentheses \(in this order\):

1. **The I/O pin number**, which can be the actual pin number \(such as: `13`, etc.\) or a variable that stores a pin number. In this case, the variable `LED` is listed \(which has a value equal to `13`\).
2. **The mode value**, which can be `INPUT`, `INPUT_PULLUP`, or `OUTPUT`. Your RedBot uses this value to change the electrical behavior of the pin, so the pin can either receive signals from an input or send signals to an output. In this case, the mode was set to `OUTPUT` because your app will be sending "on" and "off" signals to the LED light.

At this point, your app code should look similar to this:

```cpp
/*
Hello World App
Team Info
Teacher and Class Period
*/

int LED = 13;

void setup() {
  // put your setup code here, to run once:
  pinMode(LED, OUTPUT);

}

void loop() {
  // put your main code here, to run repeatedly:

}
```

Notice that the `pinMode()` statement shown in the app code above is indented \(using the tab key\). This is a useful practice when adding code statements **within curly braces** because it helps make the code easier to read and understand – especially if your app contains many code statements nested within each other.

## Verify Your App Code

The Arduino code editor does **NOT** check your code syntax as you type, so be sure to periodically verify your code to check for errors. You can verify your code even if you're not done creating your entire app.

Verify your app code by clicking the **Verify** icon \(looks like a checkmark\) at the top of the code editor panel. \(The Arduino code editor will first save your code before verifying it.\)

After the verification is done, a message will appear in a status bar at the bottom of the code editor panel:

* If your code compiled without any errors, the status bar will display a **success message**. \(In the web editor, the message will say "Success." In the desktop editor, the message will say "Done compiling."\)
* If your code contains an error, the status bar will display an **error message** with a description of the error, and the code editor will highlight the specific line number in your code where the error was detected \(although the actual cause of the error usually occurs on a previous line\). You'll want to fix the error and then try verifying your code again.

{% hint style="warning" %}
**MULTIPLE ERRORS:** Sometimes your app code might contain multiple errors. However, the Arduino code editor will stop verifying the code at the first error that is detected. Once you fix that error and verify the code again, you might see a **new** error message for another error that occurs later in the code.
{% endhint %}

