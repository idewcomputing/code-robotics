# B-2 New App Template

An Arduino program \(or app\) is also referred to as a "sketch" because the Arduino language is designed to allow you to quickly create a program — just like a sketch is a quick drawing.

This guidebook will primarily use the term "app" but just keep in mind that **program**, **app**, and **sketch** all mean the same thing when coding in Arduino:  a set of coded software instructions to control the operation of a computing device \(which is your robot, in this case\).

## Open Code Editor

If you haven't already done so, open your Arduino code editor:

* **Arduino Create web editor:**  [Log in using your Arduino account](https://create.arduino.cc/editor/).
* **Arduino IDE desktop editor:**  Double-click the Arduino application icon on your desktop.

If you are using your Arduino code editor for the first time, it should display a new app template by default. The new app template will have some starter code automatically inserted.

{% hint style="success" %}
**CREATE NEW APP:**  If you do **not** see a new app template when you open your code editor, you can follow these instructions to [create a new app template](../../references/arduino-code-editor/create-new-app.md).
{% endhint %}

If you're using the **Arduino Create web editor**, your new app template will probably look like this:

```cpp
/*

*/

void setup() {
    
}

void loop() {
    
}

```

If you're using the **Arduino IDE desktop editor**, your new app template will probably look like this:

```cpp
void setup() {
  // put your setup code here, to run once:

}

void loop() {
  // put your main code here, to run repeatedly:

}
```

The starter code in the app template has two core functions that all Arduino programs **must** include:

* **Setup Function** — which will run only one time when your program first starts. Code statements added within the `setup()` function perform one-time startup actions such as:  set the pin modes for the device's inputs and outputs, initialize certain settings, etc.
* **Loop Function** — which starts to run after the `setup()` function is completed, and then repeats itself in an endless loop \(until the device is turned off\). Code statements added within `loop()` function perform the main tasks of your device's program.

During this tutorial, you will be adding certain code statements within the `setup()` function and within the `loop()` function. You'll also add certain code statements **outside** of these two functions.

Here are two rules to follow when coding an Arduino app:

1. Your app **must** have a `setup()` function and a `loop()` function — even if there are no code statements within these functions.
2. Your app **cannot** have more than one `setup()` function — or more than one `loop()` function.

## Add Comment

It's recommended to add a comment at the very top of your code to list a title for your app and any other information that might be helpful to you or to anyone else reviewing the program code.

Comments can be embedded throughout a program to provide information or to help clarify portions of the code. Comments are just written in plain language \(instead of using code\). Any comments added to the program are ignored when the program is compiled and uploaded to your robot.

A comment can be a [single-line](https://www.arduino.cc/reference/en/language/structure/further-syntax/singlelinecomment/) or a [block \(multiple lines\)](https://www.arduino.cc/reference/en/language/structure/further-syntax/blockcomment/).

A single-line comment starts with two forward slashes, like this:

```cpp
// this is a single line comment
```

A block comment uses a forward slash and asterisk to mark its beginning and end, like this:

```cpp
/*
this is a block comment
you can type as many lines of info as you want
anything written in a comment is ignored by the code editor
*/
```

Add a block comment at the beginning of your app code **before** the `setup()` function.

* If you're using the Arduino Create web editor, your new app template already has an empty block comment at the beginning of the code, which you can use.

Inside the block comment, list your app's title, your team's information, your teacher's name, and your class period.  \(Your teacher might have specific information to list in this block comment.\)

For example, your block comment might look like this:

```cpp
/*
Hello World App
Team 3 - Destiny, Katya, Lucas, Miguel
Ms. Hopper - Period 2
*/
```

