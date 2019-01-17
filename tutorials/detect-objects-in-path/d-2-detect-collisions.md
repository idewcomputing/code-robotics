# D-2 Detect Collisions

**STILL IN PROGRESS**

## Save Copy of App With New Name <a id="save-copy-of-app-with-new-name"></a>

In your Arduino code editor, use the "Save As" command to save a copy of the `mech_bumper_test` app as a different app named: `detect_collisions_test`

Once you saved the new app name, modify the block comment near the beginning of the app code to change `Mechanical Bumper Test` to `Detect Collisions Test`.

## Add Code for "Press to Start"

This app will use a different version of the "Press to Start" code. You'll press the D12 button to "start" the robot. Once the robot is "started," you can press the button again to "pause" the robot. \(Pressing the button yet again will "start" the robot again.\)

You'll use a global variable to keep track of whether or not the robot has been "started." Add this code statement before the setup\(\) function:

```cpp
bool started = false;
```

This code statement does three things \(in order\):

1. **It declares a data type for the variable's value.**  In this case, `bool` stands for boolean. A boolean value can either be `true` or `false`.  In this case, `true` will mean the robot is "started," and `false` will mean the robot is "paused."
2. **It declares the variable's name.** In this case, the variable will be called `started`. You get to decide what to name your variables. Choose names that will make sense to anyone reviewing your code.
3. **It assigns a value to the variable.**  In this case, the variable's initial value will be equal to `false` because we don't want to "start" the robot until the D12 button is pressed.

Next, you'll add a custom named `checkButton()` that will check whether the D12 button is pressed. If the button is pressed, the function will reverse the current value of `started` from `true` to `false` \(or from `false` to `true`\).

Add this custom function **after** the `loop()` function \(i.e., after its closing curly brace\):

```cpp
void checkButton() {
  if (button.read() == true) {
    // reverse value of started
    started = !started;
    
    // beep and blink as feedback
    digitalWrite(LED, HIGH);
    tone(speaker, 2000);
    delay(200);
    digitalWrite(LED, LOW);
    noTone(speaker);
    delay(200);
  }
}
```



