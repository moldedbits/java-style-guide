# The Official MoldedBits Java Style Guide

This style guide is different from other you may see, because the focus is
centered on readability for print and the web. We created this style guide to
keep the code in our tutorials consistent.

Our overarching goals are __conciseness__, __readability__ and __simplicity__.

You should also check out out [Swift](https://github.com/raywenderlich/swift-style-guide)
and [Objective-C](https://github.com/raywenderlich/objective-c-style-guide)
style guides too.

## Inspiration

This style-guide is somewhat of a mash-up between the existing Java language
style guides, and a tutorial-readability focused Swift style-guide. The language
guidance is drawn from the
[Android contributors style guide](https://source.android.com/source/code-style.html)
and the
[Google Java Style Guide](https://google-styleguide.googlecode.com/svn/trunk/javaguide.html).
Alterations to support additional readability in tutorials were inspired by the
[raywenderlich.com Swift style guide](https://github.com/raywenderlich/swift-style-guide).

## Android Studio Coding Style

It is possible to get Android Studio to adhere to these style guidelines, via
a rather complex sequence of menus. To make it easier, we've provided a coding
style that can be imported into Android Studio.

First, clone this repository and run `install.sh`.

Then, open Android Studio. To set this codestyle as the default, select
__File > Other Settings > Default Settings...__:

![Default Settings](resources/default_settings.png)

In __Editor > Code Style__, choose the __Scheme__ to be __raywenderlich.com__:

![Setting the Scheme](resources/setting_scheme.png)

From now on, projects you create _should_ follow the correct style guidelines.


## Table of Contents

- [Nomenclature](#nomenclature)
  + [Packages](#packages)
  + [Classes & Interfaces](#classes--interfaces)
  + [Methods](#methods)
  + [Fields](#fields)
  + [Variables & Parameters](#variables--parameters)
  + [Misc](#misc)
- [Declarations](#declarations)
  + [Access Level Modifiers](#access-level-modifiers)
  + [Fields & Variables](#fields--variables)
  + [Classes](#classes)
  + [Enum Classes](#enum-classes)
- [Spacing](#spacing)
  + [Indentation](#indentation)
  + [Line Length](#line-length)
  + [Vertical Spacing](#vertical-spacing)
- [Getters & Setters](#getters--setters)
- [Brace Style](#brace-style)
- [Switch Statements](#switch-statements)
- [Annotations](#annotations)
- [XML Guidance](#xml-guidance)
  + [XML File Names](#xml-file-names)
  + [Indentation](#indentation-1)
  + [Use Context-Specific XML Files](#use-context-specific-xml-files)
  + [XML Attribute Ordering](#xml-attribute-ordering)
- [Language](#language)
- [Copyright Statement](#copyright-statement)
- [Smiley Face](#smiley-face)
- [Credit](#credits)


## Nomenclature

On the whole, naming should follow Java standards.

### Packages

Package names are all lowercase, with consecutive words simply concatenated together (no underscores, no hyphens).

__BAD__:

```java
com.example.deepSpace
com.example.deep_space
```

__GOOD__:

```java
com.example.deepspace
```

### Classes & Interfaces

Written in __UpperCamelCase__. For example `RadialSlider`. 

### Methods

Written in __lowerCamelCase__. For example `setValue`.

### Fields

Written in __lowerCamelCase__.

Static fields should be written in __uppercase__, with an underscore separating
words:

```java
public static final int THE_ANSWER = 42;
```

As distasteful as it is, field naming should follow the Android source code
naming conventions:

- Non-public, non-static field names start with an `m`.
- Static field names start with an `s`.

For example:

```java
public class MyClass {
  public static final int SOME_CONSTANT = 42;
  public int mPublicField;
  private static MyClass sSingleton;
  int mPackagePrivate;
  private int mPrivate;
  protected int mProtected;
}
```

> __Note:__ You can set Android Studio to follow this convention. See this SO
> link for details http://stackoverflow.com/questions/22732722/intellij-android-studio-member-variable-prefix

### Variables & Parameters

Written in __lowerCamelCase__.

Single character values to be avoided except for temporary looping variables.

### Misc

In code, acronyms should be treated as words. For example:

__BAD:__

```java
XMLHTTPRequest
String URL
findPostByID
```
__GOOD:__

```java
XmlHttpRequest
String url
findPostById
```

## Declarations

### Access Level Modifiers

Access level modifiers should be explicitly defined for classes, methods and
member variables.

### Fields & Variables

Prefer single declaration per line.

__BAD:__

```java
String username, twitterHandle;
```

__GOOD:__

```java
String username;
String twitterHandle;
```

### Classes

Exactly one class per source file, although inner classes are encouraged where
scoping appropriate.


### Enum Classes

Enum classes should be avoided where possible, due to a large memory overhead.
Static constants are preferred. See http://developer.android.com/training/articles/memory.html#Overhead
for further details.

Enum classes without methods may be formatted without line-breaks, as follows:

```java
private enum CompassDirection { EAST, NORTH, WEST, SOUTH }
```

## Spacing

Spacing is especially important in MoldedBits code, as code needs to be
easily readable as part of the tutorial. Java does not lend itself well to this.

### Indentation

Indentation is using spaces - never tabs.

#### Blocks

Each time a new block or block-like construct is opened, the indent increases by two spaces. When the block ends, the indent returns to the previous indent level. The indent level applies to both code and comments throughout the block. 

__BAD:__

```java
for (int i = 0; i < 10; i++) {
    Log.i(TAG, "index=" + i);
}
```

__GOOD:__

```java
for (int i = 0; i < 10; i++) {
  Log.i(TAG, "index=" + i);
}
```

#### Line Wraps

Terminology Note: When code that might otherwise legally occupy a single line is divided into multiple lines, typically to avoid overflowing the column limit, this activity is called line-wrapping.

Indentation for line wraps should use 4 spaces (not the default 8):

__BAD:__

```java
CoolUiWidget widget =
        someIncrediblyLongExpression(that, reallyWouldNotFit, on, aSingle, line);
```

__GOOD:__

```java
CoolUiWidget widget =
    someIncrediblyLongExpression(that, reallyWouldNotFit, on, aSingle, line);
```
The prime directive of line-wrapping is: prefer to break at a higher syntactic level. Also:

When a line is broken at a non-assignment operator the break comes before the symbol.
This also applies to the following "operator-like" symbols: the dot separator (.), the ampersand in type bounds (<T extends Foo & Bar>), and the pipe in catch blocks (catch (FooException | BarException e)).
When a line is broken at an assignment operator the break typically comes after the symbol, but either way is acceptable.
This also applies to the "assignment-operator-like" colon in an enhanced for ("foreach") statement.
A method or constructor name stays attached to the open parenthesis (() that follows it.
A comma (,) stays attached to the token that precedes it.

__BAD:__
```
Counter.getInstance().
    getCount();
    
if (value != null && 
    value.equals(value2)
```

__GOOD:__
```
Counter.getInstance()
    .getCount();
    
if (value != null
    && value.equals(value2)
```
  
When there are multiple continuation lines, indentation may be varied beyond +4 as desired. In general, two continuation lines use the same indentation level if and only if they begin with syntactically parallel elements.

### Line Length

Lines should be no longer than 100 characters long.


### Vertical Spacing

There should be exactly one blank line between methods to aid in visual clarity 
and organization. Whitespace within methods should separate functionality, but 
having too many sections in a method often means you should refactor into
several methods.

## Getters & Setters

For external access to fields in classes, getters and setters are preferred to
direct access of the fields. Fields should rarely be `public`.

However, it is encouraged to use the field directly when accessing internally
(i.e. from inside the class). This is a performance optimization recommended
by Google: http://developer.android.com/training/articles/perf-tips.html#GettersSetters

Prefer Lombok @Getter and @Setter annotations.

## Brace Style

Only trailing closing-braces are awarded their own line. All others appear the
same line as preceding code:

__BAD:__

```java
class MyClass
{
  void doSomething()
  {
    if (someTest)
    {
      // ...
    }
    else
    {
      // ...
    }
  }
}
```

__GOOD:__

```java
class MyClass {
  void doSomething() {
    if (someTest) {
      // ...
    } else {
      // ...
    }
  }
}
```

Conditional statements are always required to be enclosed with braces,
irrespective of the number of lines required.

__BAD:__

```java
if (someTest)
  doSomething();
if (someTest) doSomethingElse();
```

__GOOD:__

```java
if (someTest) {
  doSomething();
}
if (someTest) { doSomethingElse(); }
```


## Switch Statements

Switch statements fall-through by default, but this can be unintuitive. If you
require this behavior, comment it.

Alway include the `default` case.

__BAD:__

```java
switch (anInput) {
  case 1:
    doSomethingForCaseOne();
  case 2:
    doSomethingForCaseOneOrTwo();
    break;
  case 3:
    doSomethingForCaseOneOrThree();
    break;
}
```

__GOOD:__

```java
switch (anInput) {
  case 1:
    doSomethingForCaseOne();
    // fall through
  case 2:
    doSomethingForCaseOneOrTwo();
    break;
  case 3:
    doSomethingForCaseOneOrThree();
    break;
  default:
    break;
}
```

## Annotations

Standard annotations should be used - in particular `@Override`. This should
appear the line before the function declaration.

__BAD:__

```java
protected void onCreate(Bundle savedInstanceState) {
  super.onCreate(savedInstanceState);
}
```

__GOOD:__

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
  super.onCreate(savedInstanceState);
}
```


## XML Guidance

Since Android uses XML extensively in addition to Java, we have some rules
specific to XML.

### XML File Names

View-based XML files should be prefixed with the type of view that they
represent.

__BAD:__

- `login.xml`
- `main_screen.xml`
- `rounded_edges_button.xml`

__GOOD:__

- `activity_login.xml`
- `fragment_main_screen.xml`
- `button_rounded_edges.xml`

### Indentation

Similarly to Java, indentation should be __two characters__.

### Use Context-Specific XML Files

Wherever possible XML resource files should be used:

- Strings => `res/values/strings.xml`
- Styles => `res/values/styles.xml`
- Colors => `res/color/colors.xml`
- Animations => `res/anim/`
- Drawable => `res/drawable`


### XML Attribute Ordering

Where appropriate, XML attributes should appear in the following order:

- `id` attribute
- `layout_*` attributes
- style attributes such as `gravity` or `textColor`
- value attributes such as `text` or `src`

Within each of these groups, the attributes should be ordered alphabetically.


## Language

Use US English spelling.

__BAD:__

```java
String colour = "red";
```

__GOOD:__

```java
String color = "red";
```

## Copyright Statement

The following copyright statement should be included at the top of every source
file:

    /*
     * Copyright (c) 2016 Razeware LLC
     * 
     * Permission is hereby granted, free of charge, to any person obtaining a copy
     * of this software and associated documentation files (the "Software"), to deal
     * in the Software without restriction, including without limitation the rights
     * to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
     * copies of the Software, and to permit persons to whom the Software is
     * furnished to do so, subject to the following conditions:
     * 
     * The above copyright notice and this permission notice shall be included in
     * all copies or substantial portions of the Software.
     * 
     * THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
     * IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
     * FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
     * AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
     * LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
     * OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
     * THE SOFTWARE.
     */

## Credits


