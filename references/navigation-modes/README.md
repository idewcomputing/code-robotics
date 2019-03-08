# Navigation Modes

During your demonstration, your robot will need to navigate within your team's 6 ft × 6 ft testing environment. You will need to decide which basic navigation mode\(s\) to use to control your robot's movements as it completes its tasks:

* **Distance Navigation** — robot drives straight for specific distances and turns \(or stops\) at specific points
* **Line Counting Navigation** — robot drives straight while counting line markers it crosses, and then turns at specific line numbers to start driving on a new path
* **Line Following Navigation** — robot follows a line while also counting other lines it crosses, and then turns at specific line numbers to start following a new line
* **Autonomous Navigation** — robot uses its sensors to detect features in its environment \(obstacles, lines, drop-offs, etc.\) and make decisions about what actions to take \(stop, turn, drive, etc.\)

Your team's robot demonstration might use just one navigation mode for your task scenarios. However, you could also use different navigation modes for different tasks — or combine different navigation modes in the same task \(e.g., using line following plus autonomous collision avoidance\) — or even create your own navigation mode\(s\).

{% hint style="success" %}
**CHOOSE WISELY:**  ****Choose the navigation mode\(s\) that would make the most sense for the real-world environment of your robot concept.
{% endhint %}

The specific task and environment associated with the real-world context will determine what navigation mode\(s\) make logical sense for your team's demonstration.

To help you determine the navigation mode\(s\), you should:

1. First, decide whether to use "lines" vs. "no lines"
2. Second, if you're using lines, decide whether to use "line counting" vs. "line following"

## Lines vs. No Lines

If it wouldn't make sense for the real-world environment to have lines, then your robot should **NOT** navigate using line following or line counting. The one exception is that you could use "line avoiding" to keep your robot within the outline of your 6 ft × 6 ft testing environment.

* For example, a robot that transports items within a warehouse could navigate using line following \(because a real warehouse could easily have lines placed on its floors to indicate the robot pathways\).
* However, a lawn-mowing robot would **not** navigate by following lines \(because you wouldn't install lines all over a lawn\). Instead, it would need to navigate autonomously or by using distances \(or by some other method\).

So first decide whether or not it would make sense to use lines for your robot concept. This will help narrow your choices down to two navigation modes. Then select the final method that makes more sense for your team use.

* **LINES:** Line Counting Navigation — or Line Following Navigation
* **NO LINES:** Distance Navigation — or Autonomous Navigation

## Line Counting vs. Line Following

What is the difference between the navigation in Example 2 versus Example 3?

**When navigating by line counting alone,** the robot drives in a straight path between each line marker. The robot must drive in a straight path in order to cross over the line markers that you place in its path. The robot can be made to stop or turn at any line marker. All paths must be straight and must intersect at 90° angles.

* **ADVANTAGE:** The advantage of this navigation mode is you only have to place line markers for stops or turns \(instead of placing complete lines for each individual path\).

**When navigating by line following plus line counting,** the robot follows a line while counting other lines it crosses. The line that the robot is currently following can be straight, curved, or even form a loop — as long as all lines or line markers intersect at 90° angles. 

* **ADVANTAGE:** The advantage of this navigation mode is that you can create complex patterns with straight paths, curved paths, and loops \(instead of being limited to only straight sections\).

