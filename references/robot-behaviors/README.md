# Robot Behaviors

Here are direct links to certain custom functions in the coding references that can help you program your robot's tasks and behaviors. Be sure to review the the rest of the sensor's coding reference for additional code that may be necessary for the sensor and the function to work properly.

**TIP:** If any of the links below don't take you directly to the desired custom function on the destination page, just reload the destination page.

## Driving

These custom functions use the [wheel encoders](../physical-inputs/wheel-encoders.md):

* [`driveStraight()`](https://github.com/idewcomputing/code-robotics/tree/a64094b0d9c5c1da17c73efd3f8730c1ce974c2a/references/wheel-encoders.md#drive-straight-continuously) — drive straight continuously
* [`driveDistance()`](https://github.com/idewcomputing/code-robotics/tree/a64094b0d9c5c1da17c73efd3f8730c1ce974c2a/references/wheel-encoders.md#drive-straight-for-specific-distance) — drive straight for specific distance at specific motor power

## Turning

These custom functions also use the [wheel encoders](../physical-inputs/wheel-encoders.md):

* [`pivotAngle()`](https://github.com/idewcomputing/code-robotics/tree/a64094b0d9c5c1da17c73efd3f8730c1ce974c2a/references/wheel-encoders.md#pivot-both-wheels-by-specific-angle) — pivot on both wheels by specific angle
* [`turnAngle()`](https://github.com/idewcomputing/code-robotics/tree/a64094b0d9c5c1da17c73efd3f8730c1ce974c2a/references/wheel-encoders.md#turn-on-one-wheel-by-specific-angle) — turn on one wheel by specific angle

## Detecting Lines

These custom functions use the [IR line sensors](../physical-inputs/ir-line-sensors.md):

* [`followLine()`](https://github.com/idewcomputing/code-robotics/tree/a64094b0d9c5c1da17c73efd3f8730c1ce974c2a/references/ir-line-sensors.md#follow-line-automatically) — follow a line automatically
* [`avoidLine()`](https://github.com/idewcomputing/code-robotics/tree/a64094b0d9c5c1da17c73efd3f8730c1ce974c2a/references/ir-line-sensors.md#avoid-line-automatically) — avoid a line automatically \(acts like border to contain robot\)
* [`countLine()`](https://github.com/idewcomputing/code-robotics/tree/a64094b0d9c5c1da17c73efd3f8730c1ce974c2a/references/ir-line-sensors.md#count-lines-and-stop-at-target-number) — drive straight while counting lines crossed and stop at specific line number
* [`followCountLine()`](https://github.com/idewcomputing/code-robotics/tree/a64094b0d9c5c1da17c73efd3f8730c1ce974c2a/references/ir-line-sensors.md#follow-line-while-counting-lines-crossed) — follow a line while counting lines crossed and stop at specific line number

## Detecting Objects

These custom functions use the [mechanical bumpers](../physical-inputs/mechanical-bumpers.md), [ultrasonic sensor](../physical-inputs/ultrasonic-sensor.md), or [IR line sensors](../physical-inputs/ir-line-sensors.md):

* [`checkBumpers()`](https://github.com/idewcomputing/code-robotics/tree/a64094b0d9c5c1da17c73efd3f8730c1ce974c2a/references/mechanical-bumpers.md#check-bumpers-for-collisions) — check for bumper collision with object
* [`measureDistance()`](https://github.com/idewcomputing/code-robotics/tree/a64094b0d9c5c1da17c73efd3f8730c1ce974c2a/references/ultrasonic-sensor.md#measure-distance-to-object) — measure distance ahead to nearest object
* [`avoidCollision()`](https://github.com/idewcomputing/code-robotics/tree/a64094b0d9c5c1da17c73efd3f8730c1ce974c2a/references/ultrasonic-sensor.md#avoid-collisions) — avoid colliding with object if it is too close \(also works [while following a line](https://github.com/idewcomputing/code-robotics/tree/a64094b0d9c5c1da17c73efd3f8730c1ce974c2a/references/ultrasonic-sensor.md#avoid-collisions-while-following-line)\)
* [`findClosestObject()`](https://github.com/idewcomputing/code-robotics/tree/a64094b0d9c5c1da17c73efd3f8730c1ce974c2a/references/ultrasonic-sensor.md#find-closest-object) — performs 360° scan to find the closest object and then drive towards it
* [`detectSurfaceObjects()`](https://github.com/idewcomputing/code-robotics/tree/a64094b0d9c5c1da17c73efd3f8730c1ce974c2a/references/ir-line-sensors.md#detect-flat-objects-on-surface) — detects different types of flat paper objects on the surface
