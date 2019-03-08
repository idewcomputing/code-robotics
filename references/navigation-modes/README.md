# Navigation Modes

In order to complete its tasks, your robot will need to navigate within its demo environment.

Here are several possible navigation modes your robot could use:

* \*\*\*\*[**Distance Navigation**](distance-navigation.md) — robot drives straight for specific distance, and then turns to start driving in a new direction
* \*\*\*\*[**Line Counting Navigation**](line-counting-navigation.md) — robot drives straight while counting line markers it crosses, and then turns at specific line number to start driving on a new path
* \*\*\*\*[**Line Following + Counting Navigation**](line-following-counting-navigation.md) — robot follows a line while also counting other lines it crosses, and then turns at specific line number to start following a new line
* \*\*\*\*[**Autonomous Navigation**](autonomous-navigation.md) — robot uses sensors to detect features in environment \(obstacles, etc.\), and then decides what actions to take \(stop, turn, drive, etc.\)

Your team's robot demonstration might use the same navigation mode for all your task scenarios. However, you could use a different navigation mode for each task — or combine different navigation modes in the same task \(e.g., using line following plus autonomous collision avoidance\) — or create your own navigation mode.

{% hint style="success" %}
**CHOOSE WISELY:**  ****Choose the navigation mode\(s\) that would make the most sense for the real-world tasks and environment of your robot concept.
{% endhint %}

If it would **NOT** make sense for the robot's real-world environment to have lines, then your robot should **NOT** navigate using line counting or line following. The one exception is that you could use "line avoiding" to keep the robot within the outline of your demo environment.

* For example, a robot that transports items within a warehouse could navigate using line following because you could place lines on a warehouse floor to create robot pathways.
* However, a lawn-mowing robot would **not** navigate by following lines because you wouldn't place lines on a grass lawn. Instead, the robot would probably use distance or autonomous navigation.

So first decide whether or not it would make sense to use lines for your robot concept. This will help narrow your choices down to two possible navigation modes. Then select the one that makes more sense for your team use.

* **LINES:**  Line Counting Navigation — or Line Following + Counting Navigation
* **NO LINES:**  Distance Navigation — or Autonomous Navigation

