---
layout: notes
title: "[C++ Programming] Formatting Output with Manipulators"
meta: endl, fixed, scientific, left, right, setfw(), setfill(), setprecision()
reference: 
category: cpp-programming
---

## Manipulators in C++

Manipulators in C++ are operators and functions used to format the output.

Some commonly used manipulators in C++ are,
* endl
* fixed
* scientific
* left, right
* setw()
* setfill()
* setprecision()

endl, fixed, scientific are called 'manipulator operators' and set(),
setprecision() are called 'manipulator functions'.


### endl

*endl* feeds the whole line and then point the cursor to the beginning of the
next line.

*\n (escape sequence)* can be used instead of *endl* for the same purpose.

Header file *iostream* must be included.


### fixed

*fixed* is used to output floating-point numbers in a fixed decimal format.

Header file *iostream* must be included.


### scientific

*scientific* is used to output floating-point numbers in scientific format.

Header file *iostream* must be included.


### left, right

* left
    - the output is padded to the *field width* appending *fill characters* at
      the end.
* right
    - the output is padded to the *fleid width* by inserting *fill characters*
      at the beginning.

Once set, remains set until changed to something else.

Header file *iostream* must be included.


### setw()

*setw()* is used to set the minimum field width on the output (string or a 
number).
* If the width specified is less than the width required by the output, the
  output automatically expands to the required width; the output is NOT
  truncated.

Applies to the next output expression ONLY!

The output is right-justified.

Header file *iomanip* must be included. 


### setprecision()

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

Once set, remains set until a similar subsequent statement changes the 
precision.

Header file *iomanip* must be included. 


## RULES!!!

1. Default precision is 6.
2. setw() is the only manipulator active on the next output expression ONLY!
3. If field width is set to small, the number/string is still printed. set() is
   ignored.


## Examples

### Example 1

```cpp
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
### Example 2

```cpp
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
    // Dashes represent spaces on the screen.

    cout << fixed << setw(6) << setprecision(1);
    cout << 38.24591 << endl;
    // --38.2

    cout << fixed << setw(10) << setprecision(3);
    cout << 125.374 << endl;
    // ---125.374

    cout << fixed << setw(8) << setprecision(1);
    cout << 125.374 << endl;
    // ---125.4

    cout << fixed << setw(5) << setprecision(0);
    cout << 125.374 << endl;
    // --125

    cout << fixed << setprecision(2);
    cout << setw(5) << 909 << setw(9) << 347.25 << endl;
    // --909---347.25

    cout << fixed;
    cout << setw(5) << 909 << 213 << endl;
    // --909213

    cout << fixed << setprecision(2);
    cout << setw(6) << 78.913421 << setw(6) << 909 << endl;;
    // -78.91---909

    cout << scientific << setprecision(2) << setw(10) << 74832.511 << endl;
    // --7.48E+04

    return 0;
}
```
### Example 3

```cpp
//
// Program to input and output mixed data types.
// Types: string, char, integer, float, double
//
// Output format operations: left, setprecision(), setfill(), setw() and fixed.
//

#include <iostream>
#include <iomanip>
#include <fstream>
#include <string>

using namespace std;

int main(int argc, char *argv[])
{
    string firstname;
    string lastname;
    char initial;
    unsigned int employee_no;
    float wage, hours;
    double pay;

    cout << "Employee Record Database\n\n"; 
    //'\n' can be used instead of 'endl'

    cout << "enter the following information for each employee:\n\n";
    cout << "LastName FirstName MiddleInitial IDNumber Wage HoursWorked";
    cout << endl << endl;

    cin >> lastname >> firstname >> initial >> employee_no >> wage >> hours;

    cout << endl;
    cout << fixed << setprecision(2);
    cout << left; // Left justify in the field
    // Once 'left' has been used, everything is left-justified until reset to
    // 'right'
    cout << setfill('.'); // Set fill to dots
    // Once set, remains set until changed to something else. So be sure to
    // set it back to blank when done.

    cout << setw(20) << "Last Name:" << lastname << endl;
    cout << setw(20) << "Fist Name:" << firstname << endl;
    cout << setw(20) << "Initial:" << initial << endl;
    cout << setw(20) << "Employee Number:" << employee_no << endl;
    cout << setw(20) << "Wage:" << wage << endl;
    cout << setw(20) << "Hours Worked:" << hours << endl;
    // setw() has to be written every time because it is the only manipulator
    // that is active on the very next output expression ONLY!!!

    pay = wage * hours;

    cout << "Pay:" << '$' << pay << endl;

    cout << setfill(' '); // Restore fill char to space

    cout << setw(20) << endl << endl;
    system("pause"); // Windows only


    return 0;
}
```
```text
Employee Record Database

enter the following information for each employee:

LastName FirstName MiddleInitial IDNumber Wage HoursWorked

Lee Kyungjae M 2470 25.50 40

Last Name:..........Lee
Fist Name:..........Kyungjae
Initial:............M
Employee Number:....2470
Wage:...............25.50
Hours Worked:.......40.00
Pay:$1020.00
```
