# Navigation Modes

During your demonstration, your robot will need to navigate within your team's 6 ft × 6 ft testing environment. You will need to decide which basic navigation mode\(s\) to use to control your robot's movements as it completes its tasks:

* **Distance Navigation** — robot drives straight for specific distances and turns \(or stops\) at specific points
* **Line Counting Navigation** — robot drives straight while counting line markers it crosses, and then turns at specific line numbers to start driving on a new path
* **Line Following Navigation** — robot follows a line while also counting other lines it crosses, and then turns at specific line numbers to start following a new line
* **Autonomous Navigation** — robot uses its sensors to detect features in its environment \(obstacles, lines, drop-offs, etc.\) and make decisions about what actions to take \(stop, turn, drive, etc.\)

Your team's robot demonstration might use just one navigation mode for your task scenarios. However, you could also combine different navigation modes \(e.g., using line following plus autonomous collision avoidance\) — or even create your own navigation mode.

**IMPORTANT: Choose a navigation mode that would make the most sense for the real-world environment of your robot concept.** The specific task and environment associated with the real-world context will determine what navigation mode\(s\) make logical sense for the demo . The next two sections on this page will help you decide.

## Lines vs. No Lines

If it wouldn't make sense for the real-world environment to have lines, then your robot shouldn't navigate using line following or line counting. The one exception is that you can use "line avoiding" to keep your robot within the outline of your 6 ft × 6 ft testing environment.

* For example, a robot that transports items within a warehouse could navigate using line following \(because a real warehouse could have lines placed on its floors to indicate the robot pathways\).
* However, a lawn-mowing robot would **not** navigate by following lines \(because you wouldn't install lines all over a lawn\). Instead, it would need to navigate autonomously or by using distances.

So first decide whether or not it would make sense to use lines for your robot concept. This will help narrow your choices down to two navigation modes. Then select the final method that either makes more sense or seems more feasible for your team to program successfully.

* **LINES:** Line Counting Navigation — or Line Following Navigation
* **NO LINES:** Distance Navigation — or Autonomous Navigation

## Line Counting vs. Line Following

What is the difference between the navigation in Example 2 versus Example 3?

**When navigating by line counting alone,** the robot drives in a straight path between each line marker. The robot must drive in a straight path in order to cross over the line markers that you place in its path. The robot can stop at a Any side paths must be placed at 90° angles.

* **ADVANTAGE:** The advantage of this navigation mode is you only have to place line markers for stops or turns \(instead of placing complete lines for each individual path\).

**When navigating by line following plus line counting,** the robot follows a line while counting other lines it crosses. The line that the robot is currently following can be straight, curved, or even form a loop — just be sure that all lines or line markers cross each other at 90° right angles. The 

* **ADVANTAGE:** The advantage of this navigation mode is that paths can be curved \(instead of having to use only straight sections\).

