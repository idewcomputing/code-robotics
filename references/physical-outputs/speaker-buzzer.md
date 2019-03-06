# Speaker \(Buzzer\)

The RedBot kit includes a "buzzer" — a small speaker that can produce simple sounds. The speaker can only play one tone \(sound\) at a time, but you can create different sounds or sound patterns.

The speaker can be used to [provide alerts or feedback](../robot-behaviors/producing-alerts.md) to people interacting with your robot.

You can also use the speaker to [play a song](../robot-behaviors/producing-alerts.md#play-song-note-by-note) one note at a time.

## How to Code Speaker

To use the speaker in your robot app, you will need to:

1. Declare a gloabl variable to store the speaker's pin number
2. Set the pin mode for the speaker
3. Use the `tone()` method to produce a sound

## Declare Variable for Speaker

You'll need to create a global variable to store the pin number of the speaker, which is normally connected to pin 9. Add this code statement **before** the `setup()` function:

```cpp
int speaker = 9;
```

## Set Pin Mode for Speaker

You'll need to set the pin mode for the speaker. Add this code statement **within** the `setup()` function:

```cpp
pinMode(speaker, OUTPUT);
```

## Produce Tone

The `tone()` method is used to produce a sound of a specific frequency using the speaker.

The frequency should be an integer value \(whole number\) between 20-20000 Hertz:

* Lower values \(lower frequencies\) produce a lower pitched sound \(more bass\).
* Higher values \(higher frequencies\) produce a higher pitched sound \(more treble\).

To produce a sound that most people can easily hear, use a frequency value between 50 and 8000 Hertz. Try using a value of 3000, and then decide whether you want the sound to have a higher or lower pitch.

Typically, you will only want to play a tone for a certain duration of time and then turn it off.

For example, the following code will use the speaker to play a tone with a frequency of 2000 Hertz for 0.5 seconds and then turn it off:

```cpp
tone(speaker, 2000);
delay(500); // wait 0.5 seconds
noTone(speaker);
```

Notice that the `noTone()` method was used to turn the speaker off. Otherwise, the tone would keep playing continuously.

**Alternatively**, you can include the duration of the sound \(in milliseconds\) when using the `tone()` method. In this case, the tone will **automatically turn off** once the duration is over:

```cpp
tone(speaker, 2000, 500); // frequency 2000 Hz, duration 500 ms
```

{% hint style="info" %}
**VOLUME:** There is **NOT** a way to change the volume of the tone. However, you will notice that certain frequencies will naturally seem louder to your ears.
{% endhint %}



