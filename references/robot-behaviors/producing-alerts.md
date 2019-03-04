# Producing Alerts

These custom functions for producing alerts use the [speaker](../physical-outputs/speaker-buzzer.md) and [LED light](../physical-outputs/led-light.md):

* `singleBeep()` — produces a typical beep
* `doubleBeep()` — produces two quick beeps
* `longBeep()` — produces a longer beep

All of these functions use global variables that store the pin numbers for the LED and the speaker. Be sure you have these global variables listed **before** the `setup()` function:

```cpp
int LED = 13;
int speaker = 9;
```

An alert can be used as feedback to a user when the robot's built-in D12 button is pressed.

Alerts can also be useful as feedback to indicate when other events or conditions have occurred \(such as:  detecting an obstacle, reaching a destination, completing a task, etc.\).

You can modify these custom functions \(e.g., change frequency and duration of sound, etc.\) and/or create your own alert functions for different situations \(e.g., alarm sound, distress signal, obstacle alert, success signal, etc.\).

## singleBeep\(\)

The `singleBeep()` custom function produces a typical beep sound:

```cpp
void singleBeep() {
  digitalWrite(LED, HIGH);
  tone(speaker, 3000);
  delay(200);
  digitalWrite(LED, LOW);
  noTone(speaker);  
}
```

## doubleBeep\(\)

The `doubleBeep()` custom function produces two short, high-pitched beeps:

```cpp
void doubleBeep() {
  for (int i=0; i < 2; i++) {
    digitalWrite(LED, HIGH);
    tone(speaker, 4000);
    delay(100);
    digitalWrite(LED, LOW);
    noTone(speaker); 
    delay(100);    
  }
}
```

## longBeep\(\)

The `longBeep()` custom function produces a longer, low-pitched beep:

```cpp
void longBeep() {
  digitalWrite(LED, HIGH);
  tone(speaker, 1000);
  delay(750);
  digitalWrite(LED, LOW);
  noTone(speaker);
}
```

