---
layout: default
title: Conditions
nav_order: 4
---

# Conditions in Mini Mouse Macro

Conditions in Mini Mouse Macro allow you to make decisions and execute actions based on certain criteria. They work by comparing a variable or a system state against a specified value or condition.

---

## Basic Syntax

The syntax for a condition in Mini Mouse Macro is as follows:

<Condition>:<Comparison>:<Value>

markdown
Copy code

- <Condition>: Specifies what to check (e.g., a variable or system property).
- <Comparison>: Defines the comparison operator (e.g., ==, >, <, !=).
- <Value>: The value to compare against.

---

## Available Conditions

### Variable Comparison
You can compare the value of a variable using conditions.

VARIABLE:<VariableName>:<Comparison>:<Value>

makefile
Copy code

**Example:**
VARIABLE:counter:==:10

yaml
Copy code
This condition checks if the variable counter equals 10.

---

### Window State
Conditions can be used to check the state of a window.

WINDOW:<WindowTitle>:<Comparison>:<Value>

makefile
Copy code

**Example:**
WINDOW:Notepad:EXISTS

yaml
Copy code
This condition checks if a window titled "Notepad" exists.

---

### File State
You can check if a file exists or its properties.

FILE:<FilePath>:<Comparison>:<Value>

makefile
Copy code

**Example:**
FILE:C:\example.txt:EXISTS

yaml
Copy code
This condition checks if the file C:\example.txt exists.

---

### Pixel Color
Check the color of a specific screen pixel.

PIXEL:<X>:<Y>:<Comparison>:<ColorValue>

makefile
Copy code

**Example:**
PIXEL:100:200:==:#FFFFFF

yaml
Copy code
This condition checks if the pixel at (100, 200) is white (#FFFFFF).

---

### Delay and Wait Conditions
Conditions can be used with delays or waits to pause macro execution until the condition is met.

**Example:**
WAIT:VARIABLE:counter:==:20

yaml
Copy code
This waits until the variable counter equals 20.

---

## Comparison Operators

| Operator  | Description              |
|-----------|--------------------------|
| ==      | Equals                   |
| !=      | Not equals               |
| >       | Greater than             |
| <       | Less than                |
| >=      | Greater than or equal to |
| <=      | Less than or equal to    |

---

## Examples

### Example 1: Variable-Based Condition
VARIABLE:count:>=:5

yaml
Copy code
Checks if the variable count is greater than or equal to 5.

---

### Example 2: Conditional Execution
IF VARIABLE:counter:==:10 MESSAGE:Counter reached 10! ENDIF

yaml
Copy code
Displays a message box if the variable counter equals 10.

---

### Example 3: Pixel Color Check with Wait
WAIT PIXEL:300:400:==:#FF0000 MESSAGE:Red pixel detected!

yaml
Copy code
Waits until the pixel at (300, 400) is red (#FF0000), then shows a message.

---

## Tips and Tricks

1. **Combining Conditions**: Use nested conditions for complex logic.
2. **Debugging**: Add log messages to troubleshoot your conditions.
3. **Performance**: Be cautious when checking pixel colors or file states frequently, as they can impact macro speed.
