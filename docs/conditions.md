---
layout: default
title: Conditions
nav_order: 4
---

# Control Flow Statements in Mini Mouse Macro

Control flow statements in Mini Mouse Macro allow you to add decision-making capabilities to your macros, enabling them to evaluate the environment and control the flow of execution.

## IF

An **IF** condition checks whether a statement evaluates to **TRUE**.

**Example:**

```
1 | IF | FILE | C:\MMM\Skip.mmmacro | EXIST | CONTINUE
```

This reads: IF the file `C:\MMM\skip.mmmacro` exists, then CONTINUE the macro.

## IF NOT

An **IF NOT** condition checks whether a statement evaluates to **FALSE**.

**Example:**

```
1 | IF NOT | FILE SIZE | C:\MMM\Skip.mmmacro | IS | 2929 | STOP
```

This reads: IF the file size of `C:\MMM\skip.mmmacro` is not 2929 bytes, then STOP the macro.

## IF THEN ELSE

An **IF THEN ELSE** statement runs different sets of actions depending on whether an expression is **TRUE** or **FALSE**.

**Basic IF THEN Block:**

```
1 | IF | FILE | C:\Macro\File\output.txt | EXIST | THEN
2 | RUN ACTION | DEFINE INTEGER VARIABLE | COUNT::+1
3 | RUN ACTION | DEFINE STRING VARIABLE | %strFileOutput%::%count%: %date%-%TIME%
4 | RUN ACTION | OUTPUT TO FILE | C:\Macro\File\output.txt::APPEND_NEWLINE::%strFileOutput%
5 | IF | END IF
```

**IF THEN ELSE Block:**

```
1 | IF | BOOLEAN VARIABLE | %BOOLEAN% | IS TRUE | THEN
2 | RUN ACTION | MESSAGE PROMPT | TRUE
3 | IF | ELSE
4 | RUN ACTION | MESSAGE PROMPT | FALSE
5 | IF | END IF
```

Here is another example of a formed **IF THEN ELSE** block involving image detection:

```
1 | IF | DETECT IMAGE | image path C:\File\pics\capture.bmp::match quick::move mouse yes | IMAGE FOUND | THEN
2 | RUN ACTION | MOUSE CLICK | Left click at %mouse_x% %mouse_y% 10 times with 10 ms delay and lock the mouse
3 | RUN ACTION | DEFINE BOOLEAN VARIABLE | %boolImageFound%::TRUE
4 | IF | ELSE
5 | RUN ACTION | DEFINE PIXEL RANGE VARIABLE | %PIXEL_RANGE%::At location [X:89 Y:124 W:100 H:100]::Save image to C:\File\pics\capture.bmp
6 | RUN ACTION | DEFINE BOOLEAN VARIABLE | %boolImageFound%::FALSE
7 | RUN ACTION | WAIT SECONDS | 5
8 | IF | END IF
9 | IF | BOOLEAN VARIABLE | %boolImageFound% | IS FALSE | GOTO MACRO LINE | 1
```

## Nested IF Blocks

**IF** blocks can be nested within each other. Here is an example:

```
1 | IF | FOLDER | C:\Macro\File\pics\ | EXIST | THEN
2 | IF | DETECT IMAGE | image path C:\File\pics\capture.bmp::match quick::move mouse yes | IMAGE FOUND | THEN
3 | RUN ACTION | MOUSE CLICK | Left click at %mouse_x% %mouse_y% 10 times with 10 ms delay and lock the mouse
4 | RUN ACTION | DEFINE BOOLEAN VARIABLE | %boolImageFound%::TRUE
5 | IF | ELSE
6 | RUN ACTION | DEFINE PIXEL RANGE VARIABLE | %PIXEL_RANGE%::At location [X:89 Y:124 W:100 H:100]::Save image to C:\File\pics\capture.bmp
7 | RUN ACTION | DEFINE BOOLEAN VARIABLE | %boolImageFound%::FALSE
8 | RUN ACTION | WAIT SECONDS | 5
9 | IF | END IF
10 | IF | ELSE
11 | RUN ACTION | FILE CREATE | C:\File\pics\capture.bmp::B::1
12 | RUN ACTION | DEFINE PIXEL RANGE VARIABLE | %PIXEL_RANGE%::At location [X:89 Y:124 W:100 H:100]::Save image to C:\File\pics\capture.bmp
13 | RUN ACTION | DEFINE BOOLEAN VARIABLE | %boolImageFound%::FALSE
14 | IF | END IF
15 | IF | BOOLEAN VARIABLE | %boolImageFound% | IS FALSE | GOTO MACRO LINE | 1
```

## Notes on IF THEN Blocks

- All **IF THEN** blocks must have a closing **END IF**.
- Once within an **IF THEN** block, it is not possible to escape out using **GOTO** prior to closing the block.
- Classic **IF ELSEIF** statements are not yet supported.
- Statements within **IF THEN** blocks do not need to be indented and will work as expected without indentation.

