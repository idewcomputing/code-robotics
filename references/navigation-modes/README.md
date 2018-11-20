# Navigation Modes

During your demonstration, your robot will need to navigate within your team's 6 ft × 6 ft testing environment. You will need to decide which basic navigation mode\(s\) to use to control your robot's movements:

* Distance Navigation — robot drives straight for specific distances and turns \(or stops\) at specific points
* Line Counting Navigation — robot drives straight while counting line markers it crosses, and then turns \(or stops\) at specific line numbers
* Line Following Navigation — robot follows a line while also counting other lines it crosses, and then turns \(or stops\) at specific line numbers
* Autonomous Navigation — robot uses its sensors \(such as mechanical bumpers, IR line sensors, ultrasonic sensor, etc.\) to detect features in its environment \(such as obstacles, lines, etc.\) and then make decisions about what actions to take \(such as: stop, turn, drive, etc.\)

Your team's robot demonstration might use just one particular navigation mode for your scenarios. However, some teams might combine different navigation modes in their demo \(for example, using line following plus autonomous collision avoidance\) — or even create their own navigation mode.

**IMPORTANT: Choose a navigation mode that makes the most sense for the real-world context of your robot concept.** The specific task and environment associated with the real-world context will determine what navigation mode\(s\) make logical sense. The next two sections on this page will help you decide.

## Lines versus No Lines

If it wouldn't make sense for the real-world environment to have lines, then your robot shouldn't navigate using line following or line counting. The one exception is that you can use "line avoiding" to keep your robot within the outline of your 6 ft × 6 ft testing environment.

* For example, a robot that transports packages within a warehouse by always following specific paths could navigate using line following \(because a real warehouse could have lines on its floors\).
* However, a lawn-mowing robot would not navigate by following lines \(because you wouldn't install lines all over a lawn\). Instead, it would need to navigate autonomously or by using distances.

So first decide whether or not it would make sense to use lines for your robot concept. This will help narrow your choices down to two navigation modes. Then select the final method that either makes more sense or seems more feasible for your team to program successfully.

* **LINES:** Line Counting Navigation — or Line Following Navigation
* **NO LINES:** Distance Navigation — or Autonomous Navigation

## Line Counting versus Line Following

What is the difference between the navigation in Example 2 versus Example 3?

**When navigating by line counting alone \(Example 2\),** the robot drives in a straight path \(by using the wheel encoders\) between each line marker. The robot must drive in a straight path in order to cross over the line markers that you place in its path.

* **ADVANTAGE:** The advantage of this navigation mode is you only have to place line markers for stops or turns \(whereas Example 3 requires you to place complete lines for each individual path\).

**When navigating by line following plus line counting \(Example 3\),** the robot follows a line \(by using the IR line sensors\) while counting other lines it crosses. The line that the robot is currently following can be straight, curved, or even form a loop — just be sure that all lines or line markers cross each other at 90° right angles.

* **ADVANTAGE:** The advantage of this navigation mode is that paths can be curved \(whereas Example 2 requires each individual path to be straight\).

