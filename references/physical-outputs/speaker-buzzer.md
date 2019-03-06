# Speaker \(Buzzer\)

The RedBot kit includes a "buzzer" — a small speaker that can produce simple sounds. The speaker can only play one tone \(sound\) at a time, but you can create different sounds or sound patterns. You can even program it to play simple music by playing one note at a time.

The speaker can be used to [provide alerts or feedback](../robot-behaviors/producing-alerts.md) to people interacting with your robot.

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

## Play Music Note by Note

You can use the speaker to play simple music by playing a song note by note. Each note corresponds to a specific frequency played for a specific duration \(such as: whole note, half note, quarter note, etc.\).

[RedBot Experiment 4.2](https://learn.sparkfun.com/tutorials/experiment-guide-for-redbot-with-shadow-chassis/experiment-4-push-to-start--making-sounds-sik) includes an example program that can play "Twinkle Twinkle Little Star" or "It's A Small World".

The example program uses a file named `notes.h` that defines the specific frequencies for each note on a piano keyboard. It also defines durations \(in milliseconds\) for a whole note, half note, quarter note, etc.

**IMPORTANT:** You will need to include a copy of the `notes.h` file in your robot app, similar to including a library.

The `notes.h` file should be located inside the SparkFun RedBot Library folder:  
**examples &gt; Exp4\_2\_Music &gt; notes.h**

* If necessary, [download a ZIP file of the SparkFun RedBot Library](https://cdn.sparkfun.com/assets/learn_tutorials/3/5/6/SparkFun_RedBot_Arduino_Library-V_2.1.0.zip), and then unzip it to find the file.

#### How to Play Song in Program:

1. Add `notes.h` file to program as separate tab
2. Include `notes.h` file in program code using: `#include "notes.h"`
3. Add custom function named `playNote()` to play musical notes
4. Create custom function named `playSong()` that calls the `playNote()` function for each note \(or rest\) in your song
5. Play your song by calling the `playSong()` function in your `setup()` or `loop()` function

**IMPORTANT:** You will need to know the specific piano notes \(and their durations\) for the song. You'll have to find this information on your own by using sheet music or searching online.

#### 1. Add `notes.h` File to Program as Separate Tab

Add the `notes.h` file as a separate tab in your current program:

* **Arduino Create Web Editor:** Click the tab with a drop-down icon, and select "Import File Into Sketch."
* **Arduino IDE Desktop Editor:** Under the “Sketch” menu, select “Add File…”

A file upload window will appear. Navigate to where the `notes.h` file is located on your computer. Select the `notes.h` file, and click the "Open" button to close the window.

The `notes.h` file should now appear in your program as a separate tab.

#### 2. Include `notes.h` File in Program Code

In the code editor, click the tab that contains your main program. Then add this line of code before your `setup()` function:

```cpp
#include "notes.h"
```

#### 3. Add Custom Function to Play Musical Notes

You will use a custom function named `playNote()` to play one musical note at a time. When calling the function, you include parameters for the note and its duration.

Add the `playNote()` custom function **after** your `loop()` function:

```cpp
void playNote(int note, int duration) {
    // variable names for notes and durations defined in "notes.h"
    tone(speaker, note, duration);
    delay(duration);
}
```

Variable names for the possible notes and durations are defined in the `notes.h` file:

* Each note on a piano keyboard is defined in the file with a variable name that represents a specific frequency. For example, `noteC4` \("Middle C"\) is defined as representing a frequency of 262 Hertz.
* Durations \(whole note, half note, quarter note, etc.\) are defined in the file with variable names that represent a specific amount of time \(in milliseconds\) to play the note.  For example, `WN` represents a whole note, which is defined as 800 milliseconds \(i.e., 4 beats when each beat is 200 milliseconds\).

For example, to play a note, call the `playNote()` function by passing in variable names for the specific note and its duration:

```cpp
playNote(noteC4, WN);
```

#### 4. Create Custom Function to Play Song Note by Note

To play a song, you play each note in order, one at a time, by calling the `playNote()` function separately for each note \(or rest\) in the song.

You should create a custom function that contains all the `playNote()` statements for your song.

Add your `playSong()` custom function **after** your `loop()` function:

```cpp
void playSong() {
    // add code to play each note of song in order using playNote()

}
```

So in order to play a specific song, you'll have to find out how it would be played on a piano: i.e., what are the specific notes \(in order\) and their durations \(whole note, half note, etc.\).

Then you'll have to use the `notes.h` file to determine what variable names to list for the note and its duration when calling the `playNote()` function for each note.

#### 5. Call Custom Function to Play Song

You can play your song by calling the `playSong()` function inside your `setup()` or `loop()` function:

```cpp
playSong();
```

If you want to play the song faster or slower, you can change the value for the `beatLength` defined in the `notes.h` file. By default, `beatLength` has been set to 200 milliseconds. For example, if the song should be played slightly faster, try a lower value such as 150.

#### Example Program — Do You Recognize This Song?

For example, here's a program that will play a song that you might recognize:

```cpp
#include "notes.h"

const int speaker = 9;
const int button = 12;

void setup() {
    pinMode(speaker, OUTPUT);
    pinMode(button, INPUT_PULLUP);
}

void loop() {
    // when button pushed, play song
    if (digitalRead(button) == LOW) {
        playSong();
    }
}

// custom functions

void playNote(int note, int duration) {
    // variable names for notes and durations defined in "notes.h"
    tone(speaker, note, duration);
    delay(duration);
}

void playSong() {
    // play each note of song in order using playNote()
    // Do you recognize this song?
    playNote(noteC4, QN);
    playNote(noteD4, QN);
    playNote(noteF4, QN);
    playNote(noteD4, QN);
    playNote(noteA4, QN);
    playNote(Rest, QN);
    playNote(noteA4, WN);
    playNote(noteG4, WN);
    playNote(Rest, HN);
    playNote(noteC4, QN);
    playNote(noteD4, QN);
    playNote(noteF4, QN);
    playNote(noteD4, QN);
    playNote(noteG4, QN);
    playNote(Rest, QN);
    playNote(noteG4, WN);
    playNote(noteF4, WN);
    playNote(Rest, HN);
}
```

Upload this example program to your RedBot, and push the D12 button on the mainboard to play the song. [Do you recognize the song?](https://www.youtube.com/watch?v=dQw4w9WgXcQ)

To speed up this particular example song to better match the beat of the original song, click the tab for the `notes.h` file, and change the value defined for `beatLength` from its default of `200` to `125` instead. Then re-upload the program to your RedBot, and test it.

{% code-tabs %}
{% code-tabs-item title="notes.h" %}
```cpp
// NEEDED TO PLAY MUSIC NOTE BY NOTE
// add as new tab named "notes.h"
#define beatLength 200  // milliseconds per beat

// Define length of each note
#define WN   beatLength*4  // whole note
#define HN   beatLength*2  // half note
#define QN   beatLength    // quarter note
#define EN   beatLength/2  // eighth note
#define SN   beatLength/4  // sixteenth note

// Define frequency for each note on a piano keyboard
#define Rest 0
#define noteC0 16
#define noteCs0 17
#define noteDb0 17
#define noteD0 18
#define noteDs0 19
#define noteEb0 19
#define noteE0 21
#define noteF0 22
#define noteFs0 23
#define noteGb0 23
#define noteG0 25
#define noteGs0 26
#define noteAb0 26
#define noteA0 28
#define noteAs0 29
#define noteBb0 29
#define noteB0 31
#define noteC1 33
#define noteCs1 35
#define noteDb1 35
#define noteD1 37
#define noteDs1 39
#define noteEb1 39
#define noteE1 41
#define noteF1 44
#define noteFs1 46
#define noteGb1 46
#define noteG1 49
#define noteGs1 52
#define noteAb1 52
#define noteA1 55
#define noteAs1 58
#define noteBb1 58
#define noteB1 62
#define noteC2 65
#define noteCs2 69
#define noteDb2 69
#define noteD2 73
#define noteDs2 78
#define noteEb2 78
#define noteE2 82
#define noteF2 87
#define noteFs2 93
#define noteGb2 93
#define noteG2 98
#define noteGs2 104
#define noteAb2 104
#define noteA2 110
#define noteAs2 117
#define noteBb2 117
#define noteB2 123
#define noteC3 131
#define noteCs3 139
#define noteDb3 139
#define noteD3 147
#define noteDs3 156
#define noteEb3 156
#define noteE3 165
#define noteF3 175
#define noteFs3 185
#define noteGb3 185
#define noteG3 196
#define noteGs3 208
#define noteAb3 208
#define noteA3 220
#define noteAs3 233
#define noteBb3 233
#define noteB3 247
#define noteC4 262
#define noteCs4 277
#define noteDb4 277
#define noteD4 294
#define noteDs4 311
#define noteEb4 311
#define noteE4 330
#define noteF4 349
#define noteFs4 370
#define noteGb4 370
#define noteG4 392
#define noteGs4 415
#define noteAb4 415
#define noteA4 440
#define noteAs4 466
#define noteBb4 466
#define noteB4 494
#define noteC5 523
#define noteCs5 554
#define noteDb5 554
#define noteD5 587
#define noteDs5 622
#define noteEb5 622
#define noteE5 659
#define noteF5 698
#define noteFs5 740
#define noteGb5 740
#define noteG5 784
#define noteGs5 831
#define noteAb5 831
#define noteA5 880
#define noteAs5 932
#define noteBb5 932
#define noteB5 988
#define noteC6 1047
#define noteCs6 1109
#define noteDb6 1109
#define noteD6 1175
#define noteDs6 1245
#define noteEb6 1245
#define noteE6 1319
#define noteF6 1397
#define noteFs6 1480
#define noteGb6 1480
#define noteG6 1568
#define noteGs6 1661
#define noteAb6 1661
#define noteA6 1760
#define noteAs6 1865
#define noteBb6 1865
#define noteB6 1976
#define noteC7 2093
#define noteCs7 2217
#define noteDb7 2217
#define noteD7 2349
#define noteDs7 2489
#define noteEb7 2489
#define noteE7 2637
#define noteF7 2794
#define noteFs7 2960
#define noteGb7 2960
#define noteG7 3136
#define noteGs7 3322
#define noteAb7 3322
#define noteA7 3520
#define noteAs7 3729
#define noteBb7 3729
#define noteB7 3951
#define noteC8 4186
#define noteCs8 4435
#define noteDb8 4435
#define noteD8 4699
#define noteDs8 4978
#define noteEb8 4978
```
{% endcode-tabs-item %}
{% endcode-tabs %}

