# Navigation Modes

In order to complete its tasks, your robot will need to navigate within its demo environment.

Here are several possible navigation modes your robot could use:

* **Distance Navigation** — robot drives straight for specific distance, and then turns to start driving in a new direction
* **Line Counting Navigation** — robot drives straight while counting line markers it crosses, and then turns at specific line number to start driving on a new path
* **Line Following + Counting Navigation** — robot follows a line while also counting other lines it crosses, and then turns at specific line number to start following a new line
* **Autonomous Navigation** — robot uses sensors to detect features in environment \(obstacles, etc.\), and then decides what actions to take \(stop, turn, drive, etc.\)

Your team's robot demonstration might use the same navigation mode for all your task scenarios. However, you could use a different navigation mode for each task — or combine different navigation modes in the same task \(e.g., using line following plus autonomous collision avoidance\) — or create your own navigation mode.

{% hint style="success" %}
**CHOOSE WISELY:**  ****Choose the navigation mode\(s\) that would make the most sense for the real-world tasks and environment of your robot concept.
{% endhint %}

If it would **NOT** make sense for the robot's real-world environment to have lines, then your robot should **NOT** navigate using line counting or line following. The one exception is that you could use "line avoiding" to keep the robot within the outline of your demo environment.

* For example, a robot that transports items within a warehouse could navigate using line following because you could place lines on a warehouse floor to create robot pathways.
* However, a lawn-mowing robot would **not** navigate by following lines because you wouldn't place lines on a grass lawn. Instead, the robot would probably use distance or autonomous navigation.

So first decide whether or not it would make sense to use lines for your robot concept. This will help narrow your choices down to two possible navigation modes. Then select the one that makes more sense for your team use.

* **LINES:** Line Counting — or Line Following + Counting
* **NO LINES:** Distance — or Autonomous

## Distance Navigation

The robot drives straight for a specific distance, and then turns to start driving in a new direction. The robot's path is programmed as an ordered sequence of specific driving distances and specific turns \(i.e., pivot angles\).

* **ADVANTAGE**:  The robot can be programmed to follow any path needed \(i.e., path is not defined by lines or markers\).
* **DISADVANTAGE**:  The robot's turns may not be perfectly accurate every time. After making several turns, the robot might be off-course from its intended path.

## Line Counting

* **ADVANTAGE:**  You only have to place line markers for stops or turns along a path.
* **DISADVANTAGE:**  The robot can only stop or turn at a line marker. The robot's turns may not be perfectly accurate every time. If the robot gets too far off-course from its intended path, it may not detect the line marker\(s\).

## Line Following + Counting

* **ADVANTAGE:**  You can create complex line patterns with straight paths, curved paths, and loops. Even if the robot's turns aren't perfect, the robot will self-correct its direction as it starts to follow its new line path.
* **DISADVANTAGE:**  The robot can only stop or turn at a line intersection. You have to create a continuous line for each path.

## Autonomous Navigation

The robot uses its sensors to detect features in environment \(obstacles, etc.\), and then decides what actions to take \(stop, turn, drive, etc.\). The robot doesn't necessarily follow a pre-defined path, instead it follows a set of pre-defined rules for how to respond to its environment.

* **ADVANTAGE:**  The robot can adapt to changes in its environment \(e.g., obstacles in different positions, etc.\). The robot can be programmed to perform more complex behaviors \(e.g., solving maze, etc.\).
* **DISADVANTAGE:**  The robot doesn't necessarily a pre-determined path. The robot is limited by which sensors it has. Depending on the behavior needed, it may be more challenging to program the robot's rules.

