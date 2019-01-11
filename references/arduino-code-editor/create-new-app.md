# Create New App

An Arduino program \(or app\) is also referred to as a "sketch" because the Arduino language is designed to allow you to quickly create a program — just like a sketch is a quick drawing.

This guidebook will primarily use the term "app" but just keep in mind that **program**, **app**, and **sketch** all mean the same thing:  a set of coded software instructions to control the operation of a computing device \(which is your robot, in this case\).

## Create New App

### Arduino Create \(Web Editor\)

1. If necessary, click the **Sketchbook** menu link in the left navigation panel to display the Sketchbook menu options in the middle panel.
2. Click the **New Sketch** button at the top of the middle panel.

### Arduino IDE \(Desktop Editor\)

Under the **File** menu, select "New" – or you can click the **New** icon \(looks like a document\) at the top of an existing code editor window.

### Starter Code in New App

If you're using the **Arduino Create web editor**, your new app template will probably look like this:

```cpp
/*

*/

void setup() {
    
}

void loop() {
    
}

```

If you're using the **Arduino IDE desktop editor**, your new app template will probably look like this:

```cpp
void setup() {
  // put your setup code here, to run once:

}

void loop() {
  // put your main code here, to run repeatedly:

}
```

## Add Comment Block to Identify App

It is recommended to add a comment block at the very top of your code to list a title for your app and any other information that might be helpful to you or to anyone else reviewing the program code.

A blank comment block is created with slashes and asterisks like this:

```cpp
/*

*/
```

In between the asterisks, you can list as many lines of comments as you want or need. This would be a good place to list your app's name and perhaps describe its purpose. You could also include other information, such as your team information, your teacher's name and class period, etc.

Ask your teacher if there is specific information that should be listed in this block comment.

For example, your block comment might look like this:

```cpp
/*
Hello World App
Team 3 - Destiny, Katya, Lucas, Miguel
Ms. Hopper - Period 2
*/
```



