# D-4 Avoid Collisions

As your last step of this tutorial, you'll code an app to make your robot drive around and use its ultrasonic sensor to avoid collisions with obstacles.

## Save Copy of App With New Name <a id="save-copy-of-app-with-new-name"></a>

In your Arduino code editor, use the "Save As" command to save a copy of the `ultrasonic_sensor_test` app as a different app named: `avoid_collisions_test`

Once you saved the new app name, modify the block comment near the beginning of the app code to change `Ultrasonic Sensor Test` to `Avoid Collisions Test`.

## Add Custom Function to Avoid Collision

You'll add another custom function named `avoidCollision()` which will contain code to use measurements from the ultrasonic sensor to avoid colliding with an obstacle.

Add this custom function **after** the `loop()` function:

```cpp
void avoidCollision() {

  // set minimum allowed distance between robot and obstacle
  float minDist = 8.0; // change value as necessary (need decimal)

  // measure distance to nearest obstacle
  float distance = measureDistance();

  // if obstacle is too close, avoid collision
  if (distance <= minDist) {
    // add code to perform (brake, change direction, etc.)
    motors.brake();

  }
}
```

## Add Other Code When Obstacle Too Close

Right now, when the `avoidCollision()` function detects that an obstacle in the robot's path is too close, it brakes the motors.

Depending on the purpose of your robot and the environment in which it operates, there are different options for what else you might want the robot to do when an obstacle is too close.

In this case, you'll add code so the robot will randomly turn right or left \(pivot 90°\) by generating a random number \(either 0 or 1 – similar to flipping a coin\) to decide which direction to turn.

Arduino has a [`random()`](https://www.arduino.cc/reference/en/language/functions/random-numbers/random/) method which can be used to generate a random number \(integer\) within a specific range.

Add this code **within** the `if` statement in the `avoidCollision()` function, so it will be performed when the **left bumper** detects a collision \(add this code **after** the `motors.brake()` statement\):

```cpp
    delay(1000);
    // turn right or left based on random number
    long randomNum = random(2); // generate random integer of either 0 or 1
    if (randomNum == 0) pivotAngle(90); // turn right
    else pivotAngle(-90); // turn left
```

## Modify Code to Perform When Robot is Started

When the D12 button is pressed to "start" the robot, we want make the robot drive forward continuously and also avoid any collisions.

First, **delete** the existing code statements **within** the `if` statement in the `loop()` function that are performed when `started` is `true`.

You can also **delete** the `Serial.begin()` statement within the `setup()` function.

Next, add this code **within** the `if` statement in the `loop()` function, so it will be performed when `started` is `true`:

```cpp
    motors.drive(150);
    avoidCollision();
```

## Upload App to Robot

Follow the steps to connect your robot to your computer, and upload the app.

Unplug the USB cable from the robot, and place the robot on the floor.

Press the D12 button to "start" the robot driving forward. You can use your leg as an obstacle in the robot's path. When the robot detects that it is too close to an obstacle, the robot should stop, back up, and then turn 90° right or left.

When you're done testing the robot, you can pick it up, and press the D12 button to "pause" the robot \(or you can press the Reset button\).

If you want to test further, place the robot on the floor, and press the button to "start" the robot again.

