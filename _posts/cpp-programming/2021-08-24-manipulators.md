---
layout: notes
title: "[C++ Programming] Manipulators in C++"
meta: Important facts about the manipulators in C++
reference: 
category: cpp-programming
---

## Manipulators in C++

Manipulators in C++ are operators and functions used to format the output.

Some commonly used manipulators in C++ are,
* endl
* fixed
* scientific
* setw()
* setprecision()

endl, fixed, scientific are called 'manipulator operators' and set(),
setprecision() are called 'manipulator functions'.

## endl

*endl* feeds the whole line and then point the cursor to the beginning of the
next line.

*\n (escape sequence)* can be used instead of *endl* for the same purpose.

Header file *iostream* must be included.

## fixed

*fixed* is used to output floating-point numbers in a fixed decimal format.

Header file *iostream* must be included.

## scientific

*scientific* is used to output floating-point numbers in scientific format.

Header file *iostream* must be included.

## setw()

*setw()* is used to set the minimum field width on the output (string or a 
number).
* If the width specified is less than the width required by the output, the
  output automatically expands to the required width; the output is NOT
  truncated.

The output is right-justified.

Header file *iomanip* must be included. 

## setprecision()

*setprecision()* is used with floating point numbers.

Used to set the number of digits printed to the right of the decimal
point.

May be used in two forms:
* fixed
    - The keyword *fixed* before the *setprecision()* prints the floating-point
      number in fixed notation.
* scientific
    - The keyword *scientific* before the *setprecision()* prints the
      floating-point number in scientific notation.

Header file *iomanip* must be included. 

## Examples

RULES!!!
1. Default precision is 6.
2. setw() applies to the next expression ONLY!
3. If field width is set to small, the number/string is still printed. set() is
   ignored.

```c
//
// Program to show the usage of manipulators in C++
//

#include <iostream>
#include <iomanip>
#include <fstream>
#include <string>

using namespace std;

int main(int argc, char *argv[])
{
    double PI = 3.14159256;
    double big_number = 34876.237892;

    cout << "OUTPUT OPTIONS" << endl;

    cout << "Scientific Format" << endl;
    cout << scientific; /* Set the output of floating-point numbers in a 
        scientific format on the stnadard output device. */
    cout << PI << endl;
    cout << big_number << endl;

    cout << "Fixed Format" << endl; 
    cout << fixed << PI << endl << big_number << endl; /* Set the output of
        floating-point numbers in a fixed decimal format on the standard output
        device. */

    cout << "Precision and Width" << endl;
    cout << "set precision to 4" << endl; 
    cout << setprecision(4); /* Format the output of decimal numbers to 4
        decimal places until a similar subsequent statement changes the
        precision. */
    cout << PI << endl;
    cout << "set field width" << endl;
    cout << setw(10); /* Right-justify and set the minimum field width to 10.
        ----3.1416 (precision 4, width 10) */
    cout << PI << endl;
    cout << setprecision(2) << setw(6) << PI << endl; /* --3.14 (precision 2,
        width 6) */
    cout << setw(10) << PI << big_number << endl; /* ------3.1434876.23 (setw()
        only applies to the very next expression.) */

    return 0;
}
```
