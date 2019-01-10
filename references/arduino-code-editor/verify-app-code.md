# Verify App Code

The Arduino code editor does **NOT** check your code syntax as you type, so be sure to periodically verify your code to check for errors. You can verify your code even if you're not done creating your entire app.

## Select Correct Board

In order to verify the code, the code editor first needs to know which type of Arduino board is being used. The RedBot circuit board is equivalent to an Arduino Uno circuit board.

Once you've selected the correct type of Arduino board, the code editor should remember this selection for the future.

#### Arduino Create \(Web Editor\)

1. Click "Select Other Board & Port" in the drop down menu at the top of the code editor panel.
2. In the pop-up, select "Arduino/Genuino Uno" and then click the **OK** button.

#### Arduino IDE \(Desktop Editor\)

Under the **Tools** menu, go to the **Board** sub-menu, and select "Arduino/Genuino Uno" in the **Board**.

## Verify App Code

Verify your app code by clicking the **Verify** icon \(looks like a checkmark\) at the top of the code editor panel. \(The Arduino code editor will first save your code before verifying it.\)

After the verification is done, a message will appear in a status bar at the bottom of the code editor panel:

* If your code compiled without any errors, the status bar will display a **success message**. \(In the web editor, the message will say "Success." In the desktop editor, the message will say "Done compiling."\)
* If your code contains an error, the status bar will display an **error message** with a description of the error, and the code editor will highlight the specific line number in your code where the error was detected \(though the root cause of the error usually occurs on a previous line\). You'll want to fix the error and then try verifying your code again.

{% hint style="warning" %}
**MULTIPLE ERRORS:** Sometimes your app code might contain multiple errors. However, the Arduino code editor will stop verifying the code at the first error that is detected. Once you fix that error and verify the code again, you might see a **new** error message for another error that occurs later in the code.
{% endhint %}

