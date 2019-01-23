# Detecting Objects

These custom functions use the [mechanical bumpers](../physical-inputs/mechanical-bumpers.md) or [ultrasonic sensor](../physical-inputs/ultrasonic-sensor.md):

* `checkBumpers()` — check for bumper collision with object
* `measureDistance()` — measure distance ahead to nearest object
* `avoidCollision()` — avoid colliding with nearby object \(also works [while following a line](https://github.com/idewcomputing/code-robotics/tree/a64094b0d9c5c1da17c73efd3f8730c1ce974c2a/references/ultrasonic-sensor.md#avoid-collisions-while-following-line)\)
* `findClosestObject()` — performs 360° scan to find the closest object and then drive towards it

## measureDistance\(\)



```cpp
float measureDistance() {
  // uses HC-SR04 ultrasonic sensor
  unsigned long start_time, end_time, pulse_time;

  // trigger ultrasonic signal for 10 microseconds
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);

  // wait until echo received
  while (digitalRead(ECHO_PIN) == 0);

  // measure how long echo lasts (pulse time)
  start_time = micros(); // get start time in microseconds
  while (digitalRead(ECHO_PIN) == 1); // wait until echo pulse ends
  end_time = micros(); // get end time
  pulse_time = end_time - start_time; // subtract to get duration

  // pulse time of 23200 represents maximum distance for this sensor
  if (pulse_time > 23200) pulse_time = 23200;

  // calculate distance to object using pulse time
  float dist_cm = pulse_time / 58.0;
  float dist_in = pulse_time / 148.0;

  // need 60ms delay between ultrasonic sensor readings
  delay(60);

  // return distance value
  return dist_in; // or can return dist_cm
}
```

