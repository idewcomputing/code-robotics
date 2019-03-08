# Line Following + Counting Navigation

When using line following + counting navigation, the robot follow a line while counting other lines it crosses, and then turns at a specific line number to start driving on a new line. The robot's path is programmed as an ordered sequence of specific line counts and turns.

* **ADVANTAGE:**  You can create complex line patterns with straight paths, curved paths, and loops. Even if the robot's turns aren't perfect, the robot will usually self-correct its direction as it starts to follow its new line path.
* **DISADVANTAGE:**  The robot can only stop or turn at a line intersection. You have to create a continuous line for each path.

Line following + counting navigation is similar to the directions that a person might give you to get to a destination in the country \(such as "Follow this road as it curves around. At the second stop sign, turn right..."\).

## Example Task Scenario

In this task scenario, a restaurant robot will deliver a food order from the kitchen to Table 2 \(red rectangles are cardboard boxes representing a wall\), drive around the table \(delivering each person's order\), and then return to the "Start" line marker in the kitchen.

For the purposes of the demonstration, the distances traveled are much shorter than what would be required in an actual restaurant environment.

![](../../.gitbook/assets/robot-demo3.jpg)

## Example Code

Here is a possible way to code a custom function to perform this task scenario:

```cpp
void task1() {
  // Example of Line Following + Counting Navigation

  // drive out of kitchen from Start towards Table 2
  followCountLine(2); // 2nd line will be path to Table 2
  pivotAngle(-90); // turn left
  followCountLine(1); // next line is circle around table
  doubleBeep(); // alert guests that food has arrived
  pivotAngle(-90); // turn left
  followCountLine(1); // drive once around table

  // turn and return to kitchen
  pivotAngle(-90); // turn left
  followCountLine(1); // next line is main path
  pivotAngle(-90); // turn left
  followCountLine(1); // drive back into kitchen, next line is Start
  tripleBeep(); // alert staff that robot is ready for next order

  // at end of this task, reset for next task
  started = false;
  nextTask = 2;
}
```



