# F-4 Detect If Upside-Down

**STILL IN PROGRESS**

use accelerometer to check if robot has turned upside-down \(i.e., robot has flipped over, etc.\) - which is true if the pitch or roll angle is greater than 90° in any direction

use checkUpsideDown\(\) custom function - explain conceptually how it works

upload app to robot, pick up and rotate robot more than 90° in any direction to confirm it works

could modify this to create a different custom function that prevents the robot from driving on a surface that is too steep \(i.e., robot could be in danger of tipping over\) - for example, you could create custom function called checkSurfaceAngle that detects when the pitch or roll angle of the surface is greater than 45° \(or whatever specific value you choose\) - and make the robot perform certain actions when those conditions are true \(such as reverse or change direction, etc.\)

