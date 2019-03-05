# LED Light \(D13\)

The RedBot mainboard has a built-in green LED light that can be controlled by your program. The LED is hardwired to pin D13 on the RedBot mainboard and is located near the center-right of the mainboard.

The LED can be used to [provide alerts or feedback](../robot-behaviors/producing-alerts.md) \(usually in combination with sound from the speaker\).

## How to Code LED

To use the LED light in your robot app, you will need to:

1. Declare a global variable to store the LED's pin number
2. Set the pin mode for the LED
3. Use the `digitalWrite()` and `delay()` methods to turn the LED on and off

## Declare Variable for LED Pin Number

You'll need to create a global variable to store the pin number of the LED, which is connected to pin D13. Add this code statement **before** the `setup()` function:

```cpp
int LED = 13;
```

## Set Pin Mode for LED

You'll need to set the pin mode for the LED. Add this code statement **within** the `setup()` function:

```cpp
pinMode(LED, OUTPUT);
```

## Turn LED On and Off

The `digitalWrite()` method can be used to send an "on" or "off" signal to the LED by using a value of either `HIGH` or `LOW`:

* `HIGH` will **turn on** the LED
* `LOW` will **turn off** the LED

After turning on the LED, you will typically use the `delay()` method to add a waiting period \(in milliseconds\) before turning off the LED.

For example, the following code will turn on the LED for 0.5 seconds and then turn it off:

```cpp
digitalWrite(LED, HIGH); // turn on
delay(500); // wait 0.5 seconds
digitalWrite(LED, LOW); // turn off
```

You can code your own sequence of `digitalWrite()` and `delay()` statements to make the LED turn on and off in different patterns \(e.g., double blink, slow blink, fast blink, etc.\)

