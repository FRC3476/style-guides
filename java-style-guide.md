# Java Style Guide
[FIRST Robotics Competition Team 3476: Code Orange](http://www.teamcodeorange.com/)<br>
Authors: [@jackw01](https://github.com/jackw01), [@AraknosDe](https://github.com/AraknosDe)

## Editor Settings

### Indentation
Use tabs for indentation with Java. Know how to use auto indentation in your text editor. Turn on your editor's option to show indentation guides if it isn't already.

### Line Endings
Use Unix (LF) line endings instead of Windows (CRLF).

### Preferred Line Length
Set the preferred line length in your editor to 120 columns.

### Soft Wrap
Use soft wrap if your editor has it. This wraps lines longer than your preferred length, making it easier to edit long strings and to see when lines are too long.

### Text
Use a monospaced font where l, 1, and I can be easily distinguished. The default font in your text editor is good but [Input Mono](http://input.fontbureau.com/download/) or [Fira Code](https://github.com/tonsky/FiraCode) are probably better.

If your editor has an option to show invisibles, consider using it.

## Formatting

### Brace Style
Use the [K&R style](https://en.wikipedia.org/wiki/Indentation_style#K&R_style).

```java
// Acceptable in all cases
public void method() {
    doSomething();
}

// Acceptable for concise single line if statements only
if (condition) method1(value);
else method2(value);

// Not good
public void method()
{
    doSomething();
}

// Bad - can be unclear and possibly misleading
if (condition)
    method1(value);
else
    method2(value);
```

### Line Length
Keep lines other than long strings, plain text, HTML, or Markdown at a 120-column maximum.

### Line Breaks
One statement per line. Use whitespace to separate logical blocks of code.

#### Code blocks

```java
// Recommended for short blocks of code
public void method() {
    doSomething();
    doAnotherThing();
}

// Recommended for longer blocks of code:
// Once whitespace is added to the body of a code block, a blank line
// or comment should be added before the first line in the block
public void method() {

    doSomething();
    doAnotherThing();

    doADifferentThing();
}
```

#### Long method declarations

```java
// Good
public int method(
    int a,
    double b,
    String c) {

    doSomething();
}

// Also good
public int method(int a,
                  float b,
                  String c) {

    doSomething();
}

// Bad
public int method(   int a,
                   float b,
                  String c) {

    doSomething();
}
```

#### Chained method calls

```java
// Good
object.call1(value1)
      .call2(value2)
      .call3(value3);

// Bad - difficult to read
object.call1(value1).call2(value2).call3(value3);
```

### Spacing

Always pad operators, code blocks, and comma-separated lists with spaces.

```java
// Good
public int method(int a, int b) {
    int c = 0;
    if (a >= (b + 1)) {
        c = (a - b) * 2;
    }
    return c;
}

// Bad
public int method(int a,int b){
    int c=0;
    if(a>=(b+1)){
        c=(a-b)*2;
    }
    return c;
}
```

#### Horizontal alignment
Do not use spaces for horizontally aligning variable declarations.
```java
// Good
private int a;
private String b;

// Not recommended - difficult to edit later
private int    a;
private String b;
```

### Parentheses
Be explicit about operator precedence.
```java
// Good
if ((values != null) && (10 > values.size())) {}
return (a << (8 * n) + 1) | 0xFF;

// Not recommended
if (values != null && 10 > values.size()) {}

// Bad
return a << 8 * n + 1 | 0xFF;
```

### Specific Constructs

#### Arrays
```java
// Recommended for short initializers
new int[] {0, 1, 2, 3};

// Recommended for longer initializers
new int[] {
  0, 1, 2, 3
};                 
```

#### Enums
Line breaks are only necessary if `enum` constants are too long to fit on one line.
```java
// Good
private enum State { ON, OFF }
```

### Modifier Order
Follow the Java specification for modifier ordering:<br>
`public protected private abstract default static final transient volatile synchronized native strictfp`

### Imports
Imports should be grouped by top-level package. Do not use wildcard imports.

### Format Specifiers
Format specifiers should always be capitalized for readability.
```java
// Good
10000000000L

// Bad - lowercase L looks like a 1
10000000000l
```

### String Formatting
Do not use tab characters in strings. Use Unicode characters in strings instead of Unicode escapes, and if this is not possible add a comment to explain the Unicode escapes used.

## Naming

Use `lowerCamelCase` only for variable and method names. Use `UpperCamelCase` only for class names. Use `lowercase` only for package names. Use `UPPER_SNAKE_CASE` only for constant names. Never use non-English Alphabet characters in names (symbols, Unicode, emoji, accented letters, etc.).

### Acronyms and Abbreviations
Do not use acronyms in names unless they are commonly understood (HTTP, CAN, PID, I2C). Acronyms should always be capitalized.

Do not abbreviate words in names unless the abbreviation is commonly understood. **Abbreviations (like "Id" for identification) are not acronyms and should have only the first letter capitalized.**

### Spelling
Always use American English spellings.

### Variable Naming
```java
// Good
int longVariableName;

// Bad
int longvariablename;
int long_variable_name;
int LongVariableName;
int LONG_VARIABLE_NAME;
```

#### Short variable names
Do not use single letter variable names unless they are loop indices.

#### Units in variable names
Include units of measurement in variable names.
```java
// Good
float distanceInMeters;

// Bad
float distance;
```

#### Name Reuse
Do not reuse the same variable names in different scopes in the same method.

#### Metadata in variable names
Do not add information about the type of a variable to its name.

#### Names with underscores
Variable names should not start with underscores.

## Documentation

Class documentation should summarize the function of a class. Method documentation should tell what the method does and the input/output format.

Use [Javadoc](https://en.wikipedia.org/wiki/Javadoc) style with only `@param` and `@return` tags.

**Only use Javadoc comments for entire classes and methods. Use single-line or block comments inside of methods.**

```java
// Good

/**
 * Splits a string.
 *
 * @param s ...
 * @return ...
 */
List<String> split(String s);

// Bad

// Splits a string
List<String> split(String s);
```

Do not document override methods if they do not add any new functionality.

### Writing Style
```java
// Good

/**
 * A volatile storage for objects based on a key, which may be
 * invalidated and discarded.
 */
class Cache {}

/**
 * Splits a string on whitespace.
 *
 * @param s The string to split. An {@code null} string is treated as an
 *          empty string.
 * @return A list of the whitespace-delimited parts of the input.
 */
List<String> split(String s);

// Bad

/**
 * This is a class that implements a cache.
 */
class Cache {}

/**
 * Splits a string.
 *
 * @param s A string.
 * @return A list of strings.
 */
List<String> split(String s);
```
