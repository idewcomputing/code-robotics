# B. Hello World Test

**STILL IN PROGRESS**

In this second tutorial, you'll program a "Hello World" app for your robot by using its LED light, speaker, and push button.

{% hint style="info" %}
**ALTERNATIVE TUTORIALS:** Instead of completing these tutorials, your teacher might instruct your team to complete the [SparkFun Experiment Guide for RedBot](https://learn.sparkfun.com/tutorials/experiment-guide-for-redbot-with-shadow-chassis). If so, you should complete all the experiments **except** Experiment 9 \(Remote Control\).

If your robot has an **ultrasonic sensor**, be sure to complete these tutorials for that sensor:  [D-3 Test Ultrasonic Sensor](../detect-objects-in-path/d-3-test-ultrasonic-sensor.md) and [D-4 Avoid Collisions](../detect-objects-in-path/d-4-avoid-collisions.md)
{% endhint %}

## Tutorial Goals  <a id="tutorial-goals"></a>

The goals of this tutorial are to help you:

* Understand how to use Arduino to program apps for your robot
* Create a Hello World app to learn how to control your robot's LED light, speaker, and push button

## What is a Hello World app? <a id="what-is-a-hello-world-app"></a>

When learning a new programming language, the first step that many people take is to create what is called a ["Hello World"](https://en.wikipedia.org/wiki/%22Hello,_World!%22_program) program. Traditionally, this program simply displays the text "Hello World" on the screen and only requires a few lines of code. The purpose is to demonstrate that you can create a simple yet functional program in the new coding language. It's the first step before creating more complex programs.

However, your robot does **not** have a built-in screen. The good news is your RedBot circuit board has a built-in blue LED light \(D13\) that can be controlled by your device's app. So you'll program a simple app that **makes the built-in LED blink on and off repeatedly**, as a way of saying "Hello World."

After that you'll modify the app to also produce a sound using the speaker. Then you'll modify the app to detect when the built-in button \(D12\) is pressed. Once all of that is done, you'll be ready to start programming apps to make your robot drive around.

