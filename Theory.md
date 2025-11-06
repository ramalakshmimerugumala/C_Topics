## 1. Can a global variable be declared as auto?
```
No.
auto is used only for local variables inside functions.
Global variables have static storage duration by default, not automatic.
```
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
Feature	         Local Static	                    Global Static
Scope	         Within the function	            Within the file
Lifetime	     Entire program	                   Entire program
Usage	        Retains value between          function calls	Hides the global variable from other files
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
## 8.What is memory layout of a C program?
```
+---------------------------+
|   Command Line Arguments  |
|   & Environment Variables |
+---------------------------+
|          Stack            |  ← grows downward
+---------------------------+
|           Heap            |  ← grows upward
+---------------------------+
|   Uninitialized Data (BSS)|
+---------------------------+
|   Initialized Data (Data) |
+---------------------------+
|          Text (Code)      |
+---------------------------+
.text → machine code (functions)
.data → initialized global/static variables
.bss → uninitialized global/static variables
.rodata → read-only constants (like string literals and const variables
```
## 9.Where string literals are stored?
```
In Ro-Data
by using objdump or readelf, you can prove and see that string literals are stored in the .rodata section (read-only memory)
```
## 10.What if we declare a static variable inside a header file included by multiple .c files?
```
Each .c file that includes the header will get its own private copy of that static variable.
Because static gives internal linkage — it’s not shared across files.
✅ No linker error, but each file has a separate variable, not a common one.
```
## 11.What if a static local variable is declared but never used?
```
It will be allocated memory (in the data/bss segment), but unused.
The compiler may warn:
warning: unused variable ‘x’
It still exists for the program’s lifetime but is never accessed..
```
## 12.What happens if we define a global variable after main()?
```
✅ It’s perfectly valid.
In C, declarations and definitions can appear anywhere before they are used.
The compiler scans the whole file before linking, so the order doesn’t matter.
Example:
int main() { printf("%d", x); return 0; }
int x = 10; // works fine
(But better practice: declare globals before main())
```
## 13.Can we use extern inside a function?
```
✅ Yes, you can.
It means the variable is defined somewhere else (outside the function, maybe another file).
Example:
void func() {
    extern int x;
    printf("%d", x);
}
This tells the compiler not to allocate memory here — just reference the existing one.
```
## 14.What if an extern variable is declared but not defined anywhere?
```
❌ Linker error.
Example:
extern int x;
int main() { 
printf("%d", x); 
}
→ Compiler is fine, but the linker fails because x has no definition.
undefined reference to 'x'
```
## 15.What if you call a recursive function without a base condition?
```
💥 Infinite recursion → function keeps calling itself.
Eventually, stack overflow occurs because:
Each call stores return address + local variables on the stack.
Stack memory gets exhausted → program crashes.
```
## 16.What is the difference between declaring a static global variable vs a global variable without static?
```
Type	          Scope	                        Linkage	         Visible To
Global   variable	Entire program	            External	        All files (if declared extern)
Static   global variable	Only that file	    Internal	        Only within that .c file
```
## 17.Can we have two functions with same name if one is static and other is not?
```
✅ Yes, but only if they are in different files.
static functions have internal linkage — only visible in the same .c file.
The non-static version in another file is separate.
So, no conflict during linking..
```
## 18.How can you access a global variable inside a function if there’s a local variable with the same name?
```
The local variable shadows the global one.
To access the global explicitly, use the scope resolution trick:
int x = 10;   // global
void func() {
    int x = 20;   // local
    printf("%d", x);    // prints 20
    printf("%d", ::x);  // ❌ not valid in C (only in C++)
}
In C, you cannot directly access the shadowed global name.
To use it, rename one or use a different file without the local shadow.
```
## 19
