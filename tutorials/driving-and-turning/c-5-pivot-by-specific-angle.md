# C-5 Pivot By Specific Angle

**STILL IN PROGRESS**

Next, you'll code an app that uses the wheel encoders to make your robot pivot by a specific angle \(measured in degrees\).

## Using Wheel Encoder Counts to Calculate Pivot Angle

The wheel encoders can also be used to pivot \(turn\) your RedBot by a specific angle by measuring the distance traveled by the wheels while pivoting.

When pivoting, the robot turns in a circle centered between the robot's wheels. The distance between the centers of the RedBot wheel treads is 6.125 inches, which represents the diameter of the robot's pivot circle. If the robot pivoted 360°, the distance traveled by each wheel would be equal to the circumference of this pivot circle:

**C = 𝛑 × d = 3.14 × 6.125 = 19.23 inches**

Usually you will want your RedBot to pivot by a specific angle that is less than 360° — such as 45°, 90°, 180°, etc. For any specific angle, you can calculate its **arc length** \(i.e., a "partial circumference"\):

**L = 𝛂 / 360° × 𝛑 × d**

The arc length \(**L**\) represents the distance each wheel will travel while pivoting by a specific angle \(𝛂\).

For example, when pivoting by 90°, the arc length is:

L = 90° / 360° × 𝛑 × d = 0.25 × 3.14 × 6.125 = 4.81 inches

Once this arc length is calculated for a specific angle, the wheel encoders can be used to control how long the wheels are pivoted.

## Save Copy of App With New Name

In your Arduino code editor, use the "Save As" command to save a copy of your existing `drive_distance_test` app as a different app named:  `pivot_angle_test`

If necessary, here are [instructions for how to save a copy of an app with a new name](../../references/arduino-code-editor/save-and-rename-app.md).

Once you saved the new app name, modify the block comment near the beginning of the app code to change `Drive Distance Test` to `Pivot Angle Test`.

## Add Custom Function to Pivot Specific Angle

You'll add a custom function named `pivotAngle()` which contains code to make your robot pivot by a specified angle by using the wheel encoders.

Add this custom function **after** the `loop()` function \(i.e., after its closing curly brace\):



upload app to robot, and confirm it works - may need to adjust correction value in function to get as close to intended angle as possible - test, adjust correction value, upload revised app, test again

