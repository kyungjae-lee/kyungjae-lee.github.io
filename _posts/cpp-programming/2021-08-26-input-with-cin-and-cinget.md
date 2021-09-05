---
layout: notes
title: "[C++ Programming] Input with cin and cin.get()"
meta: cin, cin.get()
reference: 
category: cpp-programming
---

## Examples

### Example 1
Program to read compressed data in with *cin*

```cpp
//
// Program to read compressed data in with 'cin'
// Types: unsigned int and char
//

#include <iostream>
#include <iomanip>
#include <fstream>
#include <string>

using namespace std;

int main(int argc, char *argv[])
{
    // Variables for packed data YYYY.MM.DDPLXDC
    // setprecision() pertains to 'float' and 'double' types so we don't need
    // to deal with it in this example.

    unsigned int year;          // YYYY : Year
    unsigned int month;         // MM   : Month 
    unsigned int day;           // DD   : Day 
    char product_id;            // P    : Product
    unsigned int factory_loc;   // L    : Factory Location (integer)
    char quality_flag;          // X    : Quality Flag
    char inspector;             // D    : Inspector
    char package_type;          // C    : Package Type
    char dot;
    
    cout << "PRODUCT CODE" << endl << endl;
    cout << "Enter the product code as YYYY.MM.DDPLXDC" << endl;

    cin >> year >> dot >> month >> dot >> day >> product_id >> factory_loc 
        >> quality_flag >> inspector >> package_type;
        // cin continues to read in the data as long as the type of the data 
        // in the input buffer matches what it's expecting.
        // cin also stops reading in the data when it encounters white space.
        // skips over the white spaces to look for the next legitimate input.
        // (following input would still make the program work.)
        // 2021   . 08  . 26 . B
        // 9 G
        // DL

    cout << "Product code contains:" << endl;
    cout << left;
    cout << "Date:" << month << dot << day << dot << year << endl;
    cout << setw(15) << "Product ID: " << setw(2) << product_id << endl
        << setw(15) << "Location Code" << setw(2) << factory_loc << endl
        << setw(15) << "Quality Flag: " << setw(2) << quality_flag << endl
        << setw(15) << "Inspector: " << setw(2) << inspector << endl
        << setw(15) << "Package Type: " << setw(2) << package_type << endl
        << endl;

    cout << endl << endl;
    system("pause"); // Windows only
    
    return 0;
}
```
```text
PRODUCT CODE

Enter the product code as YYYY.MM.DDPLXDC
2021.08.27R123GYL
Product code contains:
Date:8.27.2021
Product ID:    R
Location Code  123
Quality Flag:  G
Inspector:     Y
Package Type:  L



```
### Example 2

Program to read a complete sentence (containing white space) in with 
*cin.get()*

[!] Note: *cin* cannot be used because it will stop reading data in as soon as
it encounters the white space (space, tab, end of line characters) unless there
come extra variales to read the rest into.

[!] Note: When the input data contains numbers, be aware that they will be read
in in ASCII encoded forms.

```cpp
//
// Program to read a complete sentence (containing white space) in with 
// cin.get() 
//

#include <iostream>
#include <iomanip>
#include <fstream>
#include <string>

using namespace std;

int main(int argc, char *argv[])
{
    string sentence;

    cout << "Please enter a complete sentence." << endl;
    getline(cin, sentence); 
    // Read everything up until it encounters the 'end of line' character (\n)
    // 2nd argument must be of type 'string'. Be careful!

    cout << "You entered: " << sentence << endl;

    return 0;
}
```
```
Please enter a complete sentence.
Hi, my name is Kyungjae. I like to write computer programs in C++.
You entered: Hi, my name is Kyungjae. I like to write computer programs in C++.

```

### Example 3

Program to show the difference between *cin* and *cin.get()* for input

```cpp
//
// Program to show the difference between 'cin' and 'cin.get()' for input
// 

#include <iostream>
#include <fstream>
#include <iomanip>
#include <string>

using namespace std;

int main(int argc, char *argv[])
{
    string remainder;
    char ch1 = ' ', ch2 = ' ', ch3 = ' ', ch4 = ' ';

  // Case 1: Use cin to read in a series of characters with no spaces
    cout << "Case 1: Enter at least 4 characters with no spaces in between." 
        << endl;

    cin >> ch1 >> ch2 >> ch3 >> ch4;

    cout << "You entered " << ch1 << ch2 << ch3 << ch4 << endl;

    // Get any remaining characters with getline()
    getline(cin, remainder);
    cout << "The remainder of the input buffer contained: " << remainder 
        << endl << endl;


  // Case 2: Use cin to read in a series of characters with white space 
    cout << "Case 2: enter at least 4 characters with spaces in between." 
        << endl;

    cin >> ch1 >> ch2 >> ch3 >> ch4;

    cout << "You entered " << ch1 << ch2 << ch3 << ch4 << endl;

    // Get any remaining characters with getline()
    getline(cin, remainder);
    cout << "The remainder of the input buffer contained: " << remainder 
        << endl << endl;

    
  // Case 3: Use cin.get() to input a series of characters with no spaces
    cout << "Case 3: Enter at least 4 characters with no spaces in between." 
        << endl;

    cin.get(ch1); 
    // Read exactly one character from the input buffer including spaces.
    cin.get(ch2); 
    cin.get(ch3); 
    cin.get(ch4); 

    cout << "You entered " << ch1 << ch2 << ch3 << ch4 << endl;

    // Get any remaining characters with getline()
    getline(cin, remainder);
    cout << "The remainder of the input buffer contained: " << remainder 
        << endl << endl;


  // Case 4: Use cin.get() to input a series of characters with white space
    cout << "Case 4: Enter at least 4 characters with no spaces in between." 
        << endl;

    cin.get(ch1); 
    cin.get(ch2); 
    cin.get(ch3); 
    cin.get(ch4); 

    cout << "You entered " << ch1 << ch2 << ch3 << ch4 << endl;

    // Get any remaining characters with getline()
    getline(cin, remainder);
    cout << "The remainder of the input buffer contained: " << remainder 
        << endl;

    return 0;
}
```
```
Case 1: Enter at least 4 characters with no spaces in between.
ABCD
You entered ABCD
The remainder of the input buffer contained:

Case 2: enter at least 4 characters with spaces in between.
A B     C   D
You entered ABCD
The remainder of the input buffer contained:

Case 3: Enter at least 4 characters with no spaces in between.
ABCD
You entered ABCD
The remainder of the input buffer contained:

Case 4: Enter at least 4 characters with spaces in between.
A B C D
You entered A B
The remainder of the input buffer contained: C D

```
```
Case 1: Enter at least 4 characters with no spaces in between.
ABCDEFG
You entered ABCD
The remainder of the input buffer contained: EFG

Case 2: enter at least 4 characters with spaces in between.
A B C D E       F   G
You entered ABCD
The remainder of the input buffer contained:  E F   G

Case 3: Enter at least 4 characters with no spaces in between.
ABCDEFG
You entered ABCD
The remainder of the input buffer contained: EFG

Case 4: Enter at least 4 characters with spaces in between.
A_B_C_D_  E_F_G
You entered A_B_
The remainder of the input buffer contained: C_D_  E_F_G
```
