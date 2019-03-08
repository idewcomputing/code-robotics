# Distance Navigation

In this example, the robot will navigate by driving straight for a specific distance, and then turning to start driving in a new direction. The robot app will need to contain code instructions that break down the navigation path into an ordered sequence of specific distances and specific turns \(i.e., pivot angles\).

## Example Task Scenario

In this task scenario, a hospital lab delivery robot will navigate through the hospital hallways \(red rectangles represent walls\) to an nurse's station \(labeled as "A"\), pick up blood samples \(simulated step\), and deliver the samples to the hospital lab for analysis \(labeled as "Start"\).

For the purposes of the demonstration, the distances traveled are obviously much shorter than a real hospital environment.

![](../../.gitbook/assets/robot-demo1.jpg)

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



