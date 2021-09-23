---
layout: notes
title: "[C++ Programming] User Defined Functions"
meta: User defined functions
reference: 
category: cpp-programming
---

## Examples

### Example 1

```cpp
//
// Program to validate a date input as MM DD YYYY
//
// The program uses three functions:
//
// 1. days - Returns the number of days in month
// 2. leap - Returns 1 if the year is a leap year, 0 otherwise
// 3. valiDATE - Returns FALSE if any of the three values is out of range.
//

#include <iostream>
#include <fstream>
#include <iomanip>
#include <string>

using namespace std;

// Function Prototypes
unsigned int leap(unsigned int year);
unsigned int datys_in_month(unsigned int, unsigned int);
    // Names of the parameters can be dropped
bool valiDATE(unsigned int smonth, unsigned int DOM, unsigned int year);
bool valiDATE(unsigned int month, unsigned int DOM, unsigned int year);


void main(int argc, char* argv[])
{
    unsigned int mm = 0, dd = 0, yyyy = 0;
    unsigned int i = 0;
    char answer = 'Y';

    do {
        cout << "Please enter the month, day, and year as MM DD YYYY: ";
        cin >> mm >> dd >> yyyy;

        //
        // The following WHILE LOOP is used to make sure that the data
        // entered are correct.
        //

        while (!valiDATE(mm, dd, yyyy))
        {
            cout << "Please enter the month, day and year like MM DD YYYY."
                << endl;
            cin >> mm >> dd >> yyyy;
        }

        cout << "The date has been validated." << endl << endl;

        cout << "Do you want to continue (Y/N)? ";
        cin >> answer;

    } while (answer == 'Y' || answer == 'y');

    cout << endl << endl << endl;
    system("pause");
}

// ------------------------------------------------------------------------- //
//                                                                           //
//                              LIST OF FUNCTIONS                            //
//                                                                           //
// ------------------------------------------------------------------------- //

//
// Function days_in_month
//
// Inputs:
// 1. month - Type unsigned int - Numeric value for month (1 - 12)
// 2. year  - Type unsgined int - Numeric value for year (2000 - 2025)
//
// External functions referrenced: leap
//
// Returns: number of days in the month
//

unsigned int days_in_month(unsigned int month, unsigned int year)
{
    unsigned int days = 0;

    if (month == 2)
    {
            days = 28 + leap(year);
    }
    else if (month == 4 || month == 6 || month == 9 || month == 11)
    {
        days = 30;
    }
    else
    {
        days = 31;
    }

    return days;
}



//
// Function leap
//
// Inputs:
// 1. year - Type unsigned int - Numeric value for year (2000 - 2025)
//
// Returns: 1 if the year is a leap year, 0 otherwise
//

unsigned int leap(unsigned int year)
{
    if (year % 400 == 0)
        return 1;
    else if (year % 100 != 0 && year % 4 == 0)
        return 1;
    else
        return 0;
}


//
// Function valiDATE
//
// Inputs:
// 1. month         - Type unsigned int - Numeric value for month (1 - 12)
// 2. day_of_month  - Type unsigned int - Numeric value for day of the month
// 3. year          - Type unsigned int - Numeric value for year (2000 - 2025)
//
// Returns: TRUE if month day and year are within range, FALSE othersie
//

bool valiDATE(unsigned int month, unsigned int DOM, unsigned int year)
{
    unsigned int days = 0;

    // Validate the month first
    if (month < 1 || month > 12)
    {
        cout << "Value for month (MM) is out of range." << endl << endl;
        return false;
    }

    // Validate the day of month
    days = days_in_month(month, year);
    if (DOM < 1 || DOM > days)
    {
        cout << "Value for day (DD) is out of range." << endl << endl;
        return false;
    }

    // Validate the year
    if (year < 2000 || year > 2025)
    {
        cout << "Value for year (YYYY) is out of range." << endl << endl;
        return false;
    }

    return true;
}
```
