# B. Hello World Test

In this second tutorial, you'll program a "Hello World" app for your robot by using its LED light, speaker, and push button.

{% hint style="info" %}
**ALTERNATIVE TUTORIALS:**  Instead of completing these tutorials, your teacher might instruct your team to complete the [SparkFun Experiment Guide for RedBot](https://learn.sparkfun.com/tutorials/experiment-guide-for-redbot-with-shadow-chassis). If so, you should complete all the experiments **except** Experiment 9 \(Remote Control\).

Afterwards, if your robot has an **ultrasonic sensor**, be sure to also complete these tutorials:  [D-3 Test Ultrasonic Sensor](../detect-objects-in-path/d-3-test-ultrasonic-sensor.md) and [D-4 Avoid Collisions](../detect-objects-in-path/d-4-avoid-collisions.md)
{% endhint %}

## Tutorial Goals  <a id="tutorial-goals"></a>

The goals of this tutorial are to help you:

* Understand how to use the Arduino programming language to code apps for your robot
* Program a Hello World app that controls your robot's LED light, speaker, and push button

## Arduino Programming Language

The RedBot robot runs apps written in a programming language called [Arduino](https://www.arduino.cc/reference/en/). The Arduino language is designed to make it easier to write programs for microcontrollers. Many electronic kits and robotics kits use Arduino for programming.

Arduino is actually a code library written in another computer language called [C++](https://en.wikipedia.org/wiki/C%2B%2B) \(similar to how jQuery is a code library written in JavaScript\). If and when necessary, your Arduino program can also incorporate code written directly in C++.

An Arduino program \(or app\) is also referred to as a **sketch** because the Arduino language is designed to allow you to quickly create a program — just like a sketch is a quick drawing.

These tutorials will introduce you to some of the basics of programming with Arduino.  For additional help, the [Arduino Programming Language Reference](https://www.arduino.cc/reference/en/) is useful for learning more about the structure and syntax of Arduino code.

## What is a Hello World app? <a id="what-is-a-hello-world-app"></a>

When learning a new programming language, the first step that many people take is to create what is called a ["Hello World"](https://en.wikipedia.org/wiki/%22Hello,_World!%22_program) program. Traditionally, this program simply displays the text "Hello World" on the screen and only requires a few lines of code. The purpose is to demonstrate that you can create a simple yet functional program in the new coding language. It's a first step before creating more complex programs.

However, your robot does **not** have a built-in screen. The good news is your RedBot circuit board does have a built-in green LED light \(D13\) that can be controlled by your robot's app. So you'll first program a simple app that makes the built-in LED blink on and off repeatedly, as a way of saying "Hello World."

After that you'll modify the app to use the robot's speaker to produce a "beep" sound when the LED light blinks. Then you'll modify the app to detect when the built-in button \(D12\) on the circuit board is pressed, in order to make the LED blink and the speaker beep. Once all that is done, you'll start programming apps to make your robot drive around.

