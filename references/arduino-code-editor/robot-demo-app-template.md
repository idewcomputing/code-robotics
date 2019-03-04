# Robot Demo App Template

Here is an app template that can be used as "starter" code to program your team's robot demonstration.

This app template has been designed to demonstrate 3 task scenarios:

* The `loop()` function checks to see if the button has been pressed to "start" the robot.
* If the robot is "started", it performs the next task \(represented by a number\) by calling a custom function for that task, such as `task1()`, `task2()`, etc.
* At the end of each task, the robot is "paused," and the next task number is changed \(so the robot will perform the tasks in order and start over once it reaches the last task\).
* Pressing the button again will start the next task.

If necessary, you can easily modify the app code to demonstrate more \(or fewer\) tasks.

You'll need to add other code to complete your app:

* You may need to add code to declare other global variables or create other objects. For example, if your robot will use the IR line sensors, you'll need to add code to create an object for each line sensor.
* You may need to add code within the `setup()` function. For example, if your robot will use an ultrasonic sensor, you'll need to add code to set the pin modes for the ultrasonic sensor's transmitter and receiver pins.
* You may need to **modify** the code within the `loop()` function if your robot will demonstrate more than 3 tasks \(or fewer\). Otherwise, this code should work as is.
* You'll need to add code within the `task1()` function, `task2()` function, and `task3()` function to perform your specific task scenarios.
* You will need to add other custom functions depending on the navigation mode\(s\) and other behaviors that your robot will use to complete its tasks. For example, you'll most likely need to add the `driveDistance()` and `pivotAngle()` functions — as well other custom functions.
* You may want or need to create some of your own custom functions to perform specific actions or decisions. This is especially helpful if the same set of actions will be performed multiple times within your robot tasks.

**APP TEMPLATE FOR ROBOT DEMO**

```cpp
#include <RedBot.h>

/*
Robot Demo
Team Info
Teacher - Class Period
*/

// GLOBAL VARIABLES AND OBJECTS
RedBotButton button;
RedBotMotors motors;
RedBotEncoder encoder(A2, 10);

int LED = 13;
int speaker = 9;

int nextTask = 1;
bool started = false;

// SETUP FUNCTION
void setup() {
  // put your setup code here, to run once:
  pinMode(LED, OUTPUT);
  pinMode(speaker, OUTPUT);
}

// LOOP FUNCTION
void loop() {
  // put your main code here, to run repeatedly:
  checkButton();
  if (started == true) {
    // add code to perform when "started"
    if (nextTask == 1) task1();
    else if (nextTask == 2) task2();
    else if (nextTask == 3) task3();
  }
  else {
    // add code to perform when "paused"
    motors.stop();
  }
}

// CUSTOM FUNCTIONS
void task1() {
  // add code to perform task scenario 1


  // at end of this task, reset for next task
  started = false;
  nextTask = 2;
}

void task2() {
  // add code to perform task scenario 2


  // at end of this task, reset for next task
  started = false;
  nextTask = 3;
}

void task3() {
  // add code to perform task scenario 3


  // at end of this task, reset for next task
  started = false;
  nextTask = 1; // start over
}

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

{% hint style="info" %}
**ONE BUTTON LIBRARY:**  If desired, you could modify this app template to [use the OneButton library](../physical-inputs/push-button.md#use-onebutton-object), so your robot will perform its different tasks based on different types of button presses \(single-press, double-press, or long-press\).
{% endhint %}

