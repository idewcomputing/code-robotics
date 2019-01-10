# B-5 Loop Function

Next you'll add commands in your app code to turn the LED on and off in a repeating pattern.

## Turn On LED

Your app can **receive signals from inputs** using the `digitalRead()` or `analogRead()` methods, depending on whether the values being received will be digital or analog.

Your app can **send signals to outputs** using the `digitalWrite()` or `analogWrite()` methods, depending on whether the values being sent will be digital or analog.

{% hint style="info" %}
**DIGITAL VS. ANALOG:** Digital inputs and outputs use **binary values** \(such as: HIGH vs. LOW, etc.\). Analog inputs and outputs use a **range of values** \(such as: 0-255, etc.\)
{% endhint %}

The LED can be controlled as a **digital output** that is either "on" or "off".

You'll need to send an "on" signal to the LED pin, in order to turn on the LED light. Add this code statement **within** the `loop()` function \(between the curly braces\):

```cpp
digitalWrite(LED, HIGH);
```

The `digitalWrite()` method requires two parameters inside its parentheses \(in this order\):

1. **The I/O pin number**, which can be the actual pin number \(such as: `13`, etc.\) or a variable that stores a pin number. In this case, the variable `LED` is listed \(which has a value equal to `13`\).
2. **The signal value**, which can be `HIGH` or `LOW`. Your RedBot uses this value to send an electrical signal through the pin: `HIGH` is a signal of 5 volts which represents "on," while `LOW` is a signal of 0 volts which represents "off."  In this case, the signal was set to `HIGH` because you want to turn on the LED light.

## Add Time Delay

You'll want to leave the LED turned on for a certain amount of time before you send the "off" signal.

Because the RedBot's app code runs very fast, there will be certain situations where you'll want to insert delays into the code, in order to allow time for certain events to occur.

Your app can use the `delay()` method to insert a time delay. It acts like a timer that makes the app wait before performing the next line of code.

You'll need to add a delay after the LED has been turned on. Add this code statement \(as a separate line of code\) **within** the `loop()` function \(**after** the `digitalWrite()` statement\):

```cpp
delay(500);
```

The `delay()` method requires one parameter inside its parentheses:

* **The time value**, which can be an integer number \(whole number\) or a variable that stores an integer. The value represents the number of milliseconds for the time delay \(1000 ms = 1 second\). In this case, the delay was set to `500` ms \(0.5 second\).

## Turn Off LED

Next, you'll send an "off" signal to the LED pin. Add this code statement \(as a separate line of code\) **within** the `loop()` function \(**after** the `delay()` statement\):

```cpp
digitalWrite(LED, LOW);
```

You can see that the second parameter in this `digitalWrite()` statement was set to `LOW`, which represents "off" for a digital output.

## Add Another Delay

When all the code within the `loop()` function has been performed, the `loop()` will automatically repeat itself. Since the first line of code in your `loop()` turns on the LED, you'll want to add another delay to leave the LED turned off for a brief amount of time before the `loop()` repeats itself \(which will start by turning the LED back on again\).

Add this code statement \(as a separate line of code\) **within** the `loop()` function \(**after the second** `digitalWrite()` statement\):

```cpp
delay(500);
```

At this point, the code within your `loop()` function should perform these actions \(in order\):

1. Turn On LED light
2. Wait 0.5 second
3. Turn Off LED light
4. Wait 0.5 second
5. Repeat

{% hint style="success" %}
**REPEATING LOOP:** You **don't** need to add a command to make the `loop()` function repeat – it **automatically** repeats itself after its last code statement has been performed.
{% endhint %}

This represents all the code needed for your first version of the "Hello World" app. In the next step, you'll upload the app to your robot to test it out.

