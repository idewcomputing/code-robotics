# Include RedBot Library

Arduino apps can include one or more libraries. A library is a pre-built code file that makes it easier to program certain things in your app.

There is a **SparkFun RedBot Library** \(filename: `RedBot.h`\) that makes it much easier to control the motors and sensors connected to your RedBot. You will need to add a copy of this library to your code editor, which is a **one-time process**. Then you will also need to include a copy of this library in **each new robot app**.

{% hint style="info" %}
**OTHER LIBRARIES:**  You can follow the same steps below to add other Arduino code libraries \(such as the [OneButton](http://www.mathertel.de/Arduino/OneButtonLibrary.aspx) library, etc.\) to your code editor, and then include the library in an app.
{% endhint %}

## SparkFun RedBot Library

The `RedBot.h` library contains Arduino code that defines different classes of objects. Each class defines a set of **properties** \(variables\) and **methods** \(functions\) for a specific type of object.

Your robot apps will use these classes to create objects in your app code. An object is a special type of variable that represents a specific **instance** \(member\) of a class. An object has all the properties and methods defined for that class.

The objects in your robot app code will correspond to real-life parts on your robot \(such as:  motors, wheel encoders, mechanical bumpers, etc.\).

The `RedBot.h` library defines the following classes:

* `RedBotButton` class — used to control the built-in D12 button
* `RedBotMotors` class — used to control the left and right motors
* `RedBotBumper` class — used to control the left and right mechanical bumpers
* `RedBotSensor` class — used to control analog sensors, such as the IR line sensors
* `RedBotEncoder` class — used to control the left and right wheel encoders
* `RedBotAccel` class — used to control the accelerometer

## Add RedBot Library to Code Editor

You must add a copy of the `RedBot.h` library to your code editor. This is a **one-time process**.

### Arduino Create \(Web Editor\)

If you're using the Arduino Create web editor, you should add the SparkFun RedBot library to your "Favorites" tab in the **Libraries** menu.

**You only need to do this once**, and then you'll be able to quickly and easily include a copy of the `RedBot.h` library in each of your robot apps.

1. Login to the [Arduino Create](https://create.arduino.cc/editor/) web editor.
2. Click **Libraries** in the navigation menu on the left.
3. Click the **Library Manager** button at the top of the middle panel. This will allow you to search the libraries contributed by Arduino community members.
4. In the pop-up, type `redbot` into the "Search Library" field, and press enter.
5. In the search results, click the star icon to the right of "SparkFun RedBot Library" to add this library to your Favorites. Then click the **Done** button to close the pop-up.

### Arduino IDE \(Desktop Editor\)

If you're using the desktop version of the Arduino IDE code editor, you need to download and install the SparkFun RedBot library on your computer, which will add it to your list of libraries in the **Sketch** menu.

**You only need to do this once**, and then you'll be able to quickly and easily include a copy of the `RedBot.h` library in each of your robot apps.

1. Open the Arduino IDE application on your computer.
2. Under the **Sketch** menu, select "Include Library" and then select "Manage Libraries" in the sub-menu.
3. A pop-up will appear. It will list all the Arduino libraries available for downloading. \(If you have a slower Internet connection, it make take a few seconds for the full list to populate\). Type `redbot` into the search field at the top-right, and press enter.
4. In the search results, select the most recent version of the "SparkFun RedBot Library" and then click the **Install** button.
5. After the library has downloaded and installed, click the **Close** button to close the pop-up.

## Include RedBot Library in App

You must include a copy of the `RedBot.h` library in **each of your robot apps**.

### Arduino Create \(Web Editor\)

1. Create a new app, or open an existing app.
2. If necessary, click the **Libraries** menu in the left navigation to show its options in the middle panel.
3. Click the **Favorites** tab in the middle panel. Hover your mouse cursor over "SparkFun RedBot Library" and click the **Include** button that appears.

### Arduino IDE \(Desktop Editor\)

1. Create a new app, or open an existing app.
2. Under the **Sketch** menu, select "Include Library" and then select "SparkFun RedBot Library" in the sub-menu \(the library will be listed toward the bottom under **Contributed Libraries**\).

### Both Editors

The following `#include` statements will be **automatically** inserted at the beginning of your app code:

```cpp
#include <RedBot.h>
#include <RedBotSoftwareSerial.h>
```

The `#include` statements shown above actually add **two** RedBot libraries to your program:

* The first library \(`RedBot.h`\) is the main RedBot library, which is what you need.
* The second library is the RedBot Software Serial library, which you do **not** need.

You should **delete** the **second** `#include` statement for the RedBot Software Serial library. This library is only used for the XBee Wireless Antenna module \(which is **not** included in a standard RedBot kit – and will **not** be used for this project\).

Arduino has a built-in `Serial` class that can be used to send serial data from your robot's sensors to your computer for viewing in the serial monitor \(so you **don't** need the RedBot Software Serial library\).

