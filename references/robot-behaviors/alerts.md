# Alerts

These custom functions for producing alerts use the [speaker](../physical-outputs/speaker-buzzer.md) and [LED light](../physical-outputs/led-light.md):

* `singleBeep()` — produces a typical beep
* `doubleBeep()` — produces two quick beeps
* `longBeep()` — produces a longer beep

All of these functions use global variables that store the pin numbers for the LED and the speaker. Be sure you have these global variables listed **before** the `setup()` function:

```cpp
int LED = 13;
int speaker = 9;
```

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

