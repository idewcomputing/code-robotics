# E-2 Follow Line

**STILL IN PROGRESS**

Next, you'll code an app that uses the IR line sensors to make your robot follow a line. The line determines the robot's path.

## Create Line Path on Surface



conditions required for accurate line following:

* line should form a closed loop \(otherwise, robot will drive off end of line and get lost\)
* line should turn using gentle curves \(no sharp turns\)
* line color should have high contrast compared to surface color:  typically you'll use a dark line \(black\) on a light surface \(white\), but you could use a light line on a dark surface
* line should be as uniform in color as possible and should be 0.25 to 0.75 inches wide
* surface must be relatively smooth \(may not work on uneven surface\)

get large sheet of paper \(such as: butcher paper, flip chart paper, etc.\), use black permanent marker \(not dry erase marker\) to draw 0.5 inch wide line that forms an oval about 3 feet in diameter



global variables for left and right motor powers

use followLine\(\) custom function - explain conceptually how it works

upload app to robot, and confirm it works - may need to adjust values in function \(such as: line threshold, etc.\) - test, adjust value, upload revised app, test again

