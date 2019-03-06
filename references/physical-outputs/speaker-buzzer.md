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

## Play Song Note by Note

You can use the speaker to play simple music by playing a song one note at a time. Each note corresponds to a specific frequency played for a specific duration \(such as: whole note, half note, quarter note, etc.\).

{% hint style="danger" %}
**IMPORTANT:**  Be aware that while the song is playing, the robot will **NOT** be able to perform other behaviors such as checking sensors, navigating, etc.
{% endhint %}

Playing a song requires a file named `notes.h` that defines the specific frequencies for each note on a piano keyboard. It also defines durations \(in milliseconds\) for a whole note, half note, quarter note, etc. based on a defined beat length \(in milliseconds\). If necessary, you can modify the beat length to speed up or slow down the song.

{% hint style="success" %}
**IMPORTANT:** To play a song, you need to know its specific sequence of piano notes \(and their durations\). You'll need to refer to sheet music or search online.
{% endhint %}

To play a song using the speaker, your robot app will need to:

1. Add `notes.h` as a separate tab \(separate file\) in your app
2. Add `#include` statement for `notes.h` in your app
3. Add `playNote()` custom function to play musical notes
4. Create custom function named `playSong()` to call the `playNote()` function for each note \(or rest\) in the song in sequence.
5. Call `playSong()` function to play the song

#### STEP 1. Add `notes.h` as Separate Tab in App

In your app, create a new blank tab named `notes.h`:

* **Arduino Create Web Editor:** Click the tab with a drop-down icon, and select "New Tab." In the pop-up, enter `notes.h` as the name of the new tab, and click the **OK** button.
* **Arduino IDE Desktop Editor:** Click the down arrow icon in the top-right corner of the code editor window, and then select "New Tab" in the drop-down list. A small dialog will appear at the bottom of the code editor window. Enter `notes.h` as the name of the new file, and click the **OK** button.

Copy the code below, and paste it into the blank tab named `notes.h`:

{% code-tabs %}
{% code-tabs-item title="notes.h" %}
```cpp
// NEEDED TO PLAY SONG NOTE BY NOTE
// add as new tab named "notes.h"

// define beat length - can modify to speed up or slow down song
#define beatLength 200  // milliseconds per beat

// define length of each note
#define WN   beatLength*4  // whole note
#define HN   beatLength*2  // half note
#define QN   beatLength    // quarter note
#define EN   beatLength/2  // eighth note
#define SN   beatLength/4  // sixteenth note

// define frequency of each note on a piano keyboard
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

#### STEP 2. Include `notes.h` File in App

Next you need to include the `notes.h` file in your app code, similar to including a library.

In the code editor, click the tab that contains your main app. Add this code statement at the beginning of your code:

```cpp
#include "notes.h"
```

#### STEP 3. Add Custom Function to Play Individual Note

A custom function named `playNote()` will be used to play one musical note at a time. When calling the function, you must include parameters for the note and its duration.

Add this `playNote()` function **after** your `loop()` function:

```cpp
void playNote(int note, int duration) {
    // variable names for notes and durations defined in "notes.h"
    tone(speaker, note, duration);
    delay(duration);
}
```

The variable names for the notes and durations are defined in the `notes.h` file:

* Each **note** on a piano keyboard is defined in `notes.h` with a variable name that represents a specific frequency. For example, `noteC4` is the variable name for "Middle C", which is defined as having a frequency of 262 Hertz.
* Each **duration** \(whole note, half note, quarter note, etc.\) is defined in `notes.h` with a variable name that represent a specific duration.  For example, `WN` is the variable name for a whole note, which is defined as 4 beats \(which will be 800 milliseconds if each beat length is defined as 200 milliseconds\).

To play a note, your app code will need to call the `playNote()` function and list the defined variable names for the specific note and its duration within the parentheses. For example, to play a "Middle C" whole note:

```cpp
playNote(noteC4, WN);
```

#### STEP 4. Create Custom Function to Play Song Note by Note

To play a song, your app code will need to play each note in order, one at a time, by calling the `playNote()` function separately for each note \(or rest\) in the song in sequence.

You'll create a custom function named `playSong()` that will contain all the `playNote()` statements for your song.

Add this blank `playSong()` function **after** your `loop()` function:

```cpp
void playSong() {
  // add code to play each note of song in order using playNote()

}
```

To play a specific song, you'll need to know how it would be played on a piano one note at a time:  i.e., what are the specific notes and their durations \(whole note, half note, etc.\)

Then you'll have to use the `notes.h` file to determine which variable names to list for the note and its duration. Then you'll need to list a code statement for each note to call the `playNote()` function.

For example, here's what the code inside the `playSong()` function would need to be in order to play the beginning of the song "Twinkle, Twinkle Little Star":

```cpp
void playSong() {
  // add code to play each note of song in order using playNote()
  // beginning of "Twinkle, Twinkle Little Star"
  playNote(noteC4, QN);
  playNote(noteC4, QN);

  playNote(noteG4, QN);    
  playNote(noteG4, QN);  

  playNote(noteA4, QN);    
  playNote(noteA4, QN);  

  playNote(noteG4, HN);

  playNote(noteF4, QN);    
  playNote(noteF4, QN);
}
```

{% hint style="info" %}
**MULTIPLE SONGS:**  If your app needs to play more than one song, create a separate custom function to play the notes for each song. Give each custom function a unique name, such as `playSong1()`, `playSong2()`, etc.
{% endhint %}

#### STEP 5. Call Custom Function to Play Song

You can play your song by calling the `playSong()` function **within** another function \(such as the `setup()`, `loop()`, or another custom function\) depending on when the song should be played:

```cpp
playSong();
```

If you need the song to play faster or slower, you can change the value for the `beatLength` defined in the `notes.h` file. By default, `beatLength` has been set to `200` milliseconds.

* If the song should be played **faster**, use a **lower** value for `beatLength`.
* If the song should be played **slower**, use a **higher** value for `beatLength`.



