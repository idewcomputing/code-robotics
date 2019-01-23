# E. Detect Lines on Surface

In this fifth tutorial, you'll learn how to make your robot detect lines on the surface by using its IR line sensors.

## Tutorial Goals <a id="tutorial-goals"></a>

The goals of this tutorial are to help you:

* Program a robot app that uses the IR line sensors to follow a line
* Program a robot app that uses the IR line sensors to avoid a line
* Program a robot app that uses the IR line sensors to count lines crossed

## How IR Line Sensors Work

The RedBot has three IR line sensors \(left, center, and right\) mounted at its front close to the surface. The bottom of each line sensor has an LED that transmits infrared \(IR\) light, which is invisible to the human eye. The bottom of each sensor also has an IR detector, which measures how much of the IR light is reflected back by the surface that the robot is driving on.

![Bottom View of IR Line Sensor](../../.gitbook/assets/line-sensor.jpg)

The amount of reflected IR light that is detected depends on several factors, including the color of the surface, as well as the distance between the sensor and the surface:

* A light-colored surface reflects more IR light, while a dark-colored surface reflects less IR light.
* If the surface is farther away from the sensor, the IR light becomes more scattered, and less IR light will be reflected back to the detector. Even a small increase in the distance between the sensor and the surface will significantly reduce the amount of reflected IR light.

The most common use of the IR sensors is to detect a line on the surface. The robot can be programmed to follow the line, avoid the line, count the number of lines crossed, etc.

The IR sensors can also be used to detect a surface drop-off \(such as a stair step leading down, a hole in the surface, etc.\). The robot can be programmed to avoid driving over the drop-off by stopping, changing direction, etc.

## Adding Lines to Surface

Detecting lines with the IR sensors works best with a uniform dark line on a uniform light surface \(or vice versa\). The line also needs to be the right width:  not too wide – but not too narrow. The line must be at least 0.25 inch wide – but no more than 1 inch wide.

### Making Lines with Tape

If you have a light-colored hard surface \(such as tile floor, etc.\), black electrical tape works very well for making lines.

If you have a dark-colored hard surface, white electrical tape or white masking tape works well for making lines.

If you are using large sheets of paper \(e.g., butcher paper, flip chart paper, etc.\) for your surface, you might be able to use tape to make lines on the paper. However, be aware that black electrical tape is elastic and can pull on the paper \(causing the paper to wrinkle, which interferes with line detection\). To minimize this, use short sections of electrical tape, and avoid stretching the electrical tape when applying it to the paper.

### Drawing Lines with Marker

If you are drawing lines on large sheets of paper, be sure to use a black felt-tip permanent marker \(e.g., Sharpie\) to make lines. Dry erase markers generally do **not** work well \(pigment is not dark enough on paper\).

Also be sure to keep the paper as flat as possible when using \(or when storing\). Wrinkles and folds in the paper interfere with line detection.

