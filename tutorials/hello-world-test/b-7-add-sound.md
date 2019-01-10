# B-7 Add Sound

Next, you'll modify the "Hello World" app so your robot makes a "beep" sound with its speaker whenever the D13 LED blinks.

## Add Global Variable for Speaker

You'll need to create a global variable to store the pin number of the speaker \(buzzer\) that should be connected to I/O pin 9 on the RedBot's circuit board.

Add this code statement **before** the `setup()` function:

```cpp
int speaker = 9;
```

Your code should now have two separate code statements **before** the `setup()` function to declare a global variable for the LED and a global variable for the speaker. 

## Set Pin Mode for Speaker

Like the LED light, the speaker is also an output because your app will send signals to the speaker to produce sound. So you'll need to set the pin mode for the speaker to be an output.

Add this code statement **within** the `setup()` function:

```cpp
pinMode(speaker, OUTPUT);
```

Your code should now have two separate code statements **within** the `setup()` function to set the pin mode for the LED and set the pin mode for the speaker.

## Produce Tone \(Sound\)

The speaker can only play one tone \(sound\) at a time. The `tone()` method is used to produce a sound of a specific frequency \(pitch\).

Add this code statement \(as a separate line of code\) **within** the `loop()` function \(**after** the first `digitalWrite()` statement, which turns on the LED\):

```cpp
tone(speaker, 2000);
```

The `tone()` method requires two parameters inside its parentheses \(in this order\):

1. **The I/O pin number of the speaker**, which can be the actual pin number \(such as: `9`, etc.\) or a variable that stores a pin number. In this case, the variable `speaker` is listed \(which has a value equal to `9`\).
2. **The frequency for the tone**, which can be an integer value \(whole number\) or a variable that stores an integer. The frequency value can be between 20-20000 hertz. Lower numbers will have a lower pitch, while higher numbers will have a higher pitch. In this case, the frequency will be `2000` hertz.

{% hint style="info" %}
**VOLUME:** There **isn't** a way to change the volume of a tone produced by the speaker. However, you will notice that certain frequencies will naturally seem louder to your ears.
{% endhint %}

## Stop Tone

When you use the `tone()` method in your app code to produce a sound, the speaker will keep playing the sound until you use a separate method in the code to stop the sound.

Let's stop the speaker sound when the LED is turned off.

Add this code statement \(as a separate line of code\) **within** the `loop()` function \(**after** the second `digitalWrite()` statement, which turns off the LED\):

```cpp
noTone(speaker);
```

The `tone()` method requires just one parameter inside its parentheses:

1. **The I/O pin number**, which can be the actual pin number \(such as: `9`, etc.\) or a variable that stores a pin number. In this case, the variable `speaker` is listed \(which has a value equal to `9`\).

## Modify Delay Times

Modify the **first** `delay()` method within the `loop()` function, so the delay will be `200` milliseconds. This will allow the LED and speaker to blink and beep for only 0.2 seconds.

Modify the **second** `delay()` method within the `loop()` function, so the delay will be `1500` milliseconds. This will create a 1.5 second pause between each blink/beep.

## Upload Modified App to Robot

If your robot is still connected to your computer and powered on, you should be able to upload the modified app by clicking the **Upload** icon \(looks like a right arrow\) at the top of the code editor panel. The code editor will automatically save and verify the app before uploading it to your robot.

Otherwise, if you disconnected your robot from your computer, be sure to:

1. Connect Robot to Computer
2. Turn on Robot Power
3. Select Correct Board and Port
4. Upload App to Robot

Once the modified app is uploaded to your robot, confirm that it works correctly. The robot's LED and speaker should briefly blink and beep \(in sync\) in a repeating pattern \(with 1.5 second pause between each blink/beep\).

