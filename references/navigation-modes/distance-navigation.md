# Distance Navigation

In this example, the robot will navigate by driving straight for specific distances and making turns \(or stops\) at specific points. The robot app will need to contain code instructions that break down the navigation path into an ordered sequence of specific distances and turns \(i.e., pivot angles\).

This navigation method is similar to the detailed "turn-by-turn" directions that a mapping app generates to route a car driver to a specific destination \(such as "Continue driving for 2 miles, and then turn right..."\).

## Example Task Scenario

The diagram below represents a task scenario where a hospital delivery robot will navigate through the hospital hallways \(red rectangles are cardboard boxes that represent walls\) towards an nurse's station \(labeled as "A"\), pick up blood samples \(simulated step\), and then transport the samples back to the hospital lab \(labeled as "Start"\).

![](../../.gitbook/assets/robot-demo1.jpg)

For the purposes of the demonstration, the distances traveled are obviously much shorter than a real hospital environment.

## Example Code

Here is a possible way to code a custom function to perform this task scenario:

```cpp
void task1() {
  // add code to perform task scenario 1

  // drive from Start to Nurse Station A
  driveDistance(24);
  pivotAngle(-90); // turn left
  driveDistance(48);
  pivotAngle(90); // turn right
  driveDistance(18);

  // Simulated Step: pause and pick up samples at Station A
  pauseRobot(); // wait until button pressed

  // turn around and drive back to Start
  pivotAngle(180); // turn around
  driveDistance(18);
  pivotAngle(-90); // turn left
  driveDistance(48);
  pivotAngle(90); // turn right
  driveDistance(24);

  // Simulated Step: Samples are delivered to lab at Start
  doubleBeep();

  // at end of this task, reset for next task
  started = false;
  nextTask = 2;
}
```



