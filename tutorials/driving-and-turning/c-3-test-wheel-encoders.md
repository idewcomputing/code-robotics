# C-3 Test Wheel Encoders

#### **STILL IN PROGRESS**

explain wheel encoders \(refer back to tutorial A\)

check alignment of wheel encoders:  position of Hall effect sensor compared to ring magnet attached to motor shaft

create RedBotEncoder object using encoder pin numbers

create RedBotButton object \(slightly easier\)

begin Serial connection in setup\(\) function

add testWheelEncoders\(\) custom function to use serial monitor to view encoder counts during test \(verify each wheel encoder is working properly when driving forwards and backwards, verify encoder counts are relatively close to each other\)

call testWheelEncoders\(\) in loop\(\)

upload app, keep robot connected via USB cable and standing upright on its back end

press button to test wheel encoders & view data in serial monitor

if a wheel encoder is not working properly, check alignment again - this accounts for nearly all issues with the wheel encoder - last resort: swap out Hall effect sensor and/or ring magnet

IMPORTANT:  Whenever you change the robot's batteries, you should check the alignment of the wheel encoders after putting the battery pack back into position between the motors.  It is very common to accidentally push on the Hall effect sensor wires, moving the sensors out of alignment.





