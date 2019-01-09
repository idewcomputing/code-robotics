# Verify App Code

in progress

how to verify app code \(and troubleshoot errors\)

## Verify Your App Code

The Arduino code editor does **NOT** check your code syntax as you type, so be sure to periodically verify your code to check for errors.

Verify your app code by clicking the **Verify** icon \(looks like a checkmark\) at the top of the code editor panel. \(The Arduino code editor will first save your code before verifying it.\)

After the verification is done, a message will appear in a status bar at the bottom of the code editor panel:

* If your code compiled without any errors, the status bar will display a **success message**. \(In the web editor, the message will say "Success." In the desktop editor, the message will say "Done compiling."\)
* If your code contains an error, the status bar will display an **error message** with a description of the error, and the code editor will highlight the specific line number in your code where the error was detected \(though the root cause of the error usually occurs on a previous line\). You'll want to fix the error and then try verifying your code again.

{% hint style="warning" %}
**MULTIPLE ERRORS:** Sometimes your app code might contain multiple errors. However, the Arduino code editor will stop verifying the code at the first error that is detected. Once you fix that error and verify the code again, you might see a **new** error message for another error that occurs later in the code.
{% endhint %}

