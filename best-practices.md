# Programming Best Practices
[FIRST Robotics Competition Team 3476: Code Orange](http://www.teamcodeorange.com/)<br>
Authors: [@jackw01](https://github.com/jackw01), [@AraknosDe](https://github.com/AraknosDe)

## Naming

### Consistency
Avoid inconsistent vocabulary in naming. Never give different classes, methods, or variables different names with similar meanings. Keep names that refer to the same value or functionality consistent between classes.

```java
// Bad
public void print() {...}
public void display() {...}
public void showToUser() {...}
```

Keep capitalization of ambiguous words consistent throughout your code. For example, don't use `filename` in one place and `fileName` in another.

### Choosing Names
Avoid using generic words for names:<br> `amount`, `constant`, `data`, `do`, `execute`, `factor`, `handle`, `input`, `it`, `key`, `new`, `number`, `old`, `output`, `parameter`, `perform`, `previous`, `run`, `task`, `type`, `value`, `variable`

Avoid using names with connotations or multiple meanings as they will confuse readers.

Never start variable names with articles (*a*, *an*, *the*) or possessives (*my*).

### Standard Names
Use `i` as the variable name in a `for` loop iterating over a one-dimensional array. Use `x`, `y`, and `z` when indices represent coordinates in a two-or-three-dimensional space or `i`, `j`, and `k` for other two-or-three-dimensional data.

### Code Names and Screen Names
Names in code should always match their respective user-facing text in a user interface.

## Documentation

### Updating
Keep comments up to date with code.

### Useless Comments
More comments are better up to a point, but don't write comments for code that is already self-explanatory. Use comments to explain less obvious algorithms or logic.
```java
// Good
public void addPoint(Translation2d point, double speed) {
	addPoint(point.getX(), point.getY(), speed);
	isEmpty = false;
}

// Bad
public void addPoint(Translation2d point, double speed) {
	addPoint(point.getX(), point.getY(), speed); // Add the point and speed
	isEmpty = false; // Path is not empty
}
```
Likewise, try to write code that is self-explanatory. Avoid writing long conditional statements, squeezing long math operations onto one line, or using the ternary operator.

If you have to step through code to understand it, it probably needs to be commented.

### Measurement Units
Always document the unit of measure for values passed to and returned from functions. Use SI (Metric) units for calculations since SI unit conversions are generally self-explanatory.

If converting imperial units in your code, define conversion factors as constants.

### TODOs
Leave TODO comments whenever it makes sense.
```java
// TODO: message here
```

## Defensive Programming

### Function Input and Output
Functions should check their inputs when necessary to ensure that out-of-range values will not cause other code to throw errors. For example, if dividing by an unknown number, check that the number is not zero.

Perform precondition checks using `if` statements instead of `assert`. Precondition checks should not fail silently.

Make sure that your own functions do not return unusual values like `NaN` that could cause errors in other code.

### User Input
Always sanitize strings or numbers received as user input.

### Logging
Log useful data in a format that can be easily accessed and searched later. Logs are only useful for debugging if a human can understand them.

### Globals
Never use global variables (this is generally not an issue in Java). Creating a class to hold global **constants** is usually acceptable.

### Testing
Test your code. Fix all bugs, even if they are unlikely to happen or difficult to reproduce.

### Potential Bugs
Be proactive about potential bugs and prevent them from happening before they become an issue. If you don't fix them right away, then leave a TODO comment.

### Trial and Error
Never use the [shotgun debugging](https://en.wikipedia.org/wiki/Shotgun_debugging) technique as it can introduce further bugs or unintended changes. Any other forms of trial-and-error programming are bad for the same reasons.

### Libraries and Frameworks
Use widely used and well tested libraries instead of attempting to solve complex problems yourself.

### Copy and Paste Programming
Avoid [copy and paste programming](https://en.wikipedia.org/wiki/Copy_and_paste_programming) by always reading and understanding code snippets you found online before copying them. Instead of copying and pasting, type the code out yourself and improve it in the process. Never trust other people's code to handle unusual inputs or work perfectly 100% of the time.

### Try/Catch
Try/catch should be used, but only when necessary. Never use try/catch to "fix" issues caused by your
own broken code. Exceptions that represent an actual error should always be reported (the catch block should usually not be left empty).

### Control Flow
Minimize the possible number of paths through your program and avoid nested `if` statements that are more than a few levels deep.

### Strings
Never use strings to store values that could be represented as a number or enum class.

### Initialization
Avoid leaving object properties and variables uninitialized or null. Initialize number variables to a default value when defining them.

### Recursion
Avoid using recursion as it can be difficult to debug and potentially result in infinite loops if not properly written.

## Code Quality

### Code Reuse
Always refactor repetitive code into separate functions or simplify it with loops. If the same code is used by multiple classes, move it into a package that the other classes can use.

```java
// Good
public void addPoint(double x, double y, double speed) {
	segments.add(new PathSegment(lastPoint.getX(), lastPoint.getY(), x, y, speed));
	lastPoint = new Translation2d(x, y);
}

public void addPoint(Translation2d point, double speed) {
	addPoint(point.getX(), point.getY(), speed);
}

// Bad
public void addPoint(double x, double y, double speed) {
	segments.add(new PathSegment(lastPoint.getX(), lastPoint.getY(), x, y, speed));
	lastPoint = new Translation2d(x, y);
}

public void addPoint(Translation2d point, double speed) {
	segments.add(new PathSegment(lastPoint.getX(), lastPoint.getY(), point.getX(), point.getY(), speed));
	lastPoint = new Translation2d(x, y);
}
```

### Constants
Never use "magic numbers" in your code. Always define constant numeric values as constants, even if you only use them once.

### Disambiguate
Write code in the most concise, easiest to understand, and least ambiguous way possible.

### Unused Code
Remove unused code instead of commenting it out. Getting back things you deleted shouldn't be an issue if you are using Git properly.

### Code Size
Keep functions short for readability. If a functions is over 100 lines long, consider splitting it up into smaller logical blocks.

### General Types
Try to use the most general type possible (example: `Iterable` instead of `ArrayList` or `List` when a function only needs to iterate through a set of data).

### Unnecessary Variables
Don't create unnecessary temporary variables.
```java
// Good
return getValues();

// Bad
List<int> values = getValues();
return values;
```

### Exceptions
Throw specific exceptions instead of the generic `Exception`.
