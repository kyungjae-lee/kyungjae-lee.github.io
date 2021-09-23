---
layout: notes
title: "[C++ Programming] Scope and Lifetime of a Variable"
meta: Scope and lifetime of a variable
reference: 
category: cpp-programming
---

## Scope and Lifetime of a Variable

![scope-and-lifetime]({{site.baseurl}}/img/cpp-programming/scope-and-lifetime.png){:.inline-img-w800}


## Examples

### Example 1

```cpp
//
// Program that illustrates scope rules, static variables
// passing arguments by reference and by value
//


#include <iostream>
#include <fstream>
#include <iomanip>
#include <string>

using namespace std;

void function_one(void);
void function_two(void);
void function_three(void);
void function_four(int, int);
void function_five(int&, int&);

// Global variables (Visible to all functions)
int x = 4;
int y = 3;



int main(int argc, char* argv[])
{
    // Variables
    int x = 1;
    int a = 10, b = 20;

    //
    // Scope Rules
    //
    // - Local variables are visible only within the block of code
    //   where they are defined.
    // - Global variables are visible to all functions in the program.
    //   If there is a local variable with the same identifier as a global
    //   variable, the local variable takes precedence.


    cout << "In main program local x = " << x << endl;
    function_one();
    cout << "Back in main program local x = " << x << endl;

    cout << "In main program global y = " << y << endl;
    function_one();

    function_two();
    cout << endl << endl << endl;

    // Illustrate static variables
    function_three();
    function_three();
    cout << endl << endl << endl;

    //
    // Call by value: A copy of a and b are passed to function four.
    // Function four cannot alter the variables a and b in main.
    //
    cout << "In main a = " << a << " b = " << b << endl;
    cout << "Calling function four by value." << endl;
    function_four(a, b);
    cout << "Back in main a = " << a << " b = " << b << endl;
    cout << endl << endl << endl;

    //
    // Call by reference: The addresses of a and b are passed to function five.
    // Any changes made by function five are retained by variables a and b.
    //
    cout << "In main a = " << a << " b = " << b << endl;
    cout << "Calling function five by reference." << endl;
    function_five(a, b);
    cout << "Back in main a = " << a << " b = " << b << endl;
    cout << endl << endl << endl;




    system("pause");

    return 0;
}

void function_one(void)
{
    // Variable x local to this function. Not the same as x in main.
    int x = 2;

    cout << "In function one local x = " << x << endl;
    cout << "In function one global y = " << y << endl;

    return;
}

void function_two(void)
{
    cout << "In function one local x = " << x << endl;
    cout << "In function one global y = " << y << endl;

    return;
}

void function_three(void)
{
    static int number = 3;
    cout << "Entering function three number = " << number << endl;

    number += 3;

    cout << "Leaving function three number = " << number << endl;

    return;
}

void function_four(int value_one, int value_two)
{
    cout << "Entering function four value_one = " << value_one
        << " value_two = " << value_two << endl;

    value_one = 50;
    value_two = 70;

    cout << "Leaving function four value_one = " << value_one
        << " value_two = " << value_two << endl;

    return;
}

void function_five(int &value_one, int &value_two)
{
    cout << "Entering function five value_one = " << value_one
        << " value_two = " << value_two << endl;

    value_one = 50;
    value_two = 70;

    cout << "Leaving function five value_one = " << value_one
        << " value_two = " << value_two << endl;

    return;
}
```
```text
In main program local x = 1
In function one local x = 2
In function one global y = 3
Back in main program local x = 1
In main program global y = 3
In function one local x = 2
In function one global y = 3
In function one local x = 4
In function one global y = 3



Entering function three number = 3
Leaving function three number = 6
Entering function three number = 6
Leaving function three number = 9



In main a = 10 b = 20
Calling function four by value.
Entering function four value_one = 10 value_two = 20
Leaving function four value_one = 50 value_two = 70
Back in main a = 10 b = 20



In main a = 10 b = 20
Calling function five by reference.
Entering function five value_one = 10 value_two = 20
Leaving function five value_one = 50 value_two = 70
Back in main a = 50 b = 70



Press any key to continue . . .
```
