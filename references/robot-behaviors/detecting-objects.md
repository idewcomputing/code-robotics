# Detecting Objects

These custom functions use the [mechanical bumpers](../physical-inputs/mechanical-bumpers.md) or [ultrasonic sensor](../physical-inputs/ultrasonic-sensor.md):

* [`checkBumpers()`](https://github.com/idewcomputing/code-robotics/tree/a64094b0d9c5c1da17c73efd3f8730c1ce974c2a/references/mechanical-bumpers.md#check-bumpers-for-collisions) — check for bumper collision with object
* [`measureDistance()`](https://github.com/idewcomputing/code-robotics/tree/a64094b0d9c5c1da17c73efd3f8730c1ce974c2a/references/ultrasonic-sensor.md#measure-distance-to-object) — measure distance ahead to nearest object
* [`avoidCollision()`](https://github.com/idewcomputing/code-robotics/tree/a64094b0d9c5c1da17c73efd3f8730c1ce974c2a/references/ultrasonic-sensor.md#avoid-collisions) — avoid colliding with nearby object \(also works [while following a line](https://github.com/idewcomputing/code-robotics/tree/a64094b0d9c5c1da17c73efd3f8730c1ce974c2a/references/ultrasonic-sensor.md#avoid-collisions-while-following-line)\)
* [`findClosestObject()`](https://github.com/idewcomputing/code-robotics/tree/a64094b0d9c5c1da17c73efd3f8730c1ce974c2a/references/ultrasonic-sensor.md#find-closest-object) — performs 360° scan to find the closest object and then drive towards it

