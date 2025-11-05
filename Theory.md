## 1. Can a global variable be declared as auto?
No.
auto is used only for local variables inside functions.
Global variables have static storage duration by default, not automatic.
## 2Can you declare a global variable as register? Why or why not?
No.
register variables are stored in CPU registers, not in memory.
Global variables must have a fixed memory address, so they cannot be declared as register
## 3 What is the lifetime and scope of a static variable?
```
Lifetime: Entire program execution (it exists from start to end).
Scope:
If declared inside a function → visible only within that function.
If declared outside all functions → visible only within that file
```
## 4.Difference between global static and local static variables:
```
Feature	Local Static	Global Static
Scope	Within the function	Within the file
Lifetime	Entire program	Entire program
Usage	Retains value between function calls	Hides the global variable from other files
```
## 5.What is the default value of static and extern variables?
```
Both have default value = 0 (if not initialized explicitly)
```
## 6 Can we initialize an extern variable?
```
No, not at the point of extern declaration.
You can only declare it with extern, and initialize it where it is defined.
// file1.c
int x = 10;  // definition and initialization

// file2.c
extern int x;  // declaration only, no initialization
```
## 7.Difference between declaration and definition of variables:
```
Term	                   Meaning	                                                  Example
Declaration	   Tells the compiler that a variable exists (no memory allocated).	    extern int a;
Definition	     Actually creates the variable and allocates memory.	               int a = 5;
```
## 8.
