---
layout: notes
title: "[C++ Programming] Input Buffer Operations"
meta: getline(), cin.get(), cin.ignore(), cin.peek(), cin.putback()
reference: 
category: cpp-programming
---

## Examples

### Example 1

Program to illustrate functions on the input stream.

```cpp
//
// Program to illustrate functions on the input stream - cin
// Functions: getline, get, ignore, peek, putback
//

#include <iostream>
#include <fstream>
#include <iomanip>
#include <string>

using namespace std;

int main(int argc, char* argv[])
{
	// Variables

	string indata = "";
	string remainder = "";
	char ch1 = ' ', ch2 = ' ', ch3 = ' ', ch4 = ' ', ch5 = ' ';
	unsigned int hrs, mins, seconds;
	float value;

	cout << "PROCESSING DATA FROM the INPUT BUFFER" << endl << endl;

	cout << "CASE 1. Read all the data one character at a time with cin.get()" << endl;
	cout << "Enter this data exactly as shown" << endl;
	cout << "QXR03:30:15U150.33" << endl;

	// cin.get() pulls off one character at a time
	cin.get(ch1);	// ch1 = Q,	Input Buffer: XR03:30:15U150.33
	cin.get(ch2);	// ch1 = X,	Input Buffer: R03:30:15U150.33
	cin.get(ch3);	// ch1 = R,	Input Buffer: 03:30:15U150.33
	cin.get(ch4);	// ch1 = 0,	Input Buffer: 3:30:15U150.33
	cout << ch1 << ch2 << ch3 << ch4 << endl;

	while (ch5 != '\n')
	{
		cin.get(ch5);
		cout << ch5;
	}

	cout << endl;


	cout << "CASE 2. Read all the data at once with getline(cin, indata)." << endl;
	cout << "Enter this data exactly as shown" << endl;
	cout << "QXR03:30:15U150.33" << endl;

	getline(cin, indata);
	cout << "You entered " << indata << endl;

	cout << endl;


	cout << "CASE 3. Ignore the first 3 characters then read the time." << endl;
	cout << "Enter this data exactly as shown" << endl;
	cout << "QXR03:30:15U150.33" << endl;

	// Ignore and delete from the input buffer, can't get them back
	cin.ignore(3);	// The input buffer contains 03:30:15U150.33

	while (ch1 != 'U')
	{
		cin.get(ch1);
		cout << ch1;
	}

	cout << endl;

	getline(cin, remainder);
	cout << "The input buffer contains " << remainder << endl;

	cout << endl;


	cout << "CASE 4. Ignore the first 3 characters peek at each one until U is reached. Read the time again. " << endl;
	cout << "Enter this data exactly as shown" << endl;
	cout << "QXR03:30:15U150.33" << endl;

	cin.ignore(3);	// The input buffer contains 03:30:15U150.33
	ch2 = cin.peek();	// Inspect the next character in the input buffer
						// but DO NOT READ it.
	while (ch2 != 'U')
	{
		cin.get(ch2);	// Reads a character from the input buffer
		cout << ch2;
		ch2 = cin.peek();
	}

	cout << endl;

	getline(cin, remainder);
	cout << "Theinput buffer contains " << remainder << endl;

	cout << endl;


	cout << "CASE 5-1. cin.putback(ch) Extract the time leaving the rest of the data in the input buffer. " << endl;
	cout << "Enter this data exactly as shown" << endl;
	cout << "QXR03:30:15U150.33" << endl;

	cin.get(ch1);	// Get the letter Q
	cin.get(ch2);	// Get the letter X
	cin.get(ch3);	// Get the letter R

	ch4 = cin.peek();
	while (ch4 != 'U')
	{
		cin.get(ch4);
		cout << ch4;
		ch4 = cin.peek();
	}
	// The input buffer contains U150.33
	cout << endl;

	cin.putback(ch3);	// The input buffer contains RU150.33
	cin.putback(ch2);	// The input buffer contains XRU150.33
	cin.putback(ch1);	// The input buffer contains QXRU150.33

	getline(cin, remainder);
	cout << "The input buffer contains " << remainder << endl;

	cout << endl;


	cout << "CASE 5-2. cin.putback(ch) Insert characters to the input buffer. " << endl;
	cout << "Enter this data exactly as shown" << endl;
	cout << "QXR03:30:15U150.33" << endl;

	cin.putback('G');	// Insert G into input buffer
	cin.putback('M');	// insert M into input buffer
	// The input buffer contains MGQXR03:30:15U150.33
	getline(cin, remainder);
	cout << "The input buffer contains " << remainder << endl;

	cout << endl;


	cout << "CASE 6. Read the mixed input with cin." << endl;
	cout << "Enter this data exactly as shown" << endl;
	cout << "QXR03:30:15U150.33" << endl;

	cin.ignore(3);	// Removes QXR from the input buffer
	cin >> hrs		// Input buffer now contains :30:15U150.33
		>> ch1		// Input buffer now contains 30:15U150.33
					// ch1 is used to read in and discard ':'
		>> mins		// Input buffer now contains :15U150.33
		>> ch1		// Input buffer now contains 15U150.33
		>> seconds;	// Input buffer now contains U150.33
	cin >> remainder;	// Input buffer is empty.

	cout << hrs << setw(3) << mins << setw(3) << seconds << endl;
	cout << remainder << endl;

	cout << endl;


	cout << "CASE 7. Count all zeros" << endl;
	cout << "Enter this data exactly as shown" << endl;
	cout << "QXR03:30:15U150.33" << endl;

	cin.get(ch1);	// ch1 = Q
	cin.get(ch2);	// ch2 = X
	cin.get(ch3);	// ch3 = R

	// Count all zeros
	int count = 0;
	while (ch4 != '\n')
	{
		cin.get(ch4);
		if (ch4 == '0')
			count++;
	}

	cout << count << endl;

	cout << endl;


	cout << "CASE 8. Count the numbers in a sentence." << endl;
	cout << "Enter this data exactly as shown" << endl;
	cout << "QXR03:30:15U150.33" << endl;

	ch1 = ' ';
	count = 0;
	while (ch1 != '\n')
	{
		cin.get(ch1);
		if (ch1 >= '0' && ch1 <= '9')
			count++;
	}

	cout << count << endl;

	cout << endl;


	cout << "CASE 9. Count the numbers in a sentence using isdigit() function." << endl;
	cout << "Enter this data exactly as shown" << endl;
	cout << "QXR03:30:15U150.33" << endl;

	ch1 = ' ';
	count = 0;
	while (ch1 != '\n')
	{
		cin.get(ch1);
		if (isdigit(ch1))
			count++;
	}

	cout << count << endl;

	cout << endl;

	// isdigit(ch) returns true if ch is 0-9
	// isalpha(ch) returns true if ch is a-z or A-Z
	// ispunct(ch) returns true if ch is puctuation
	// isspace(ch) returns true if ch is a space

	system("pause");
	return 0;
}
```
```text
PROCESSING DATA FROM the INPUT BUFFER

CASE 1. Read all the data one character at a time with cin.get()
Enter this data exactly as shown
QXR03:30:15U150.33
QXR03:30:15U150.33
QXR0
3:30:15U150.33

CASE 2. Read all the data at once with getline(cin, indata).
Enter this data exactly as shown
QXR03:30:15U150.33
QXR03:30:15U150.33
You entered QXR03:30:15U150.33

CASE 3. Ignore the first 3 characters then read the time.
Enter this data exactly as shown
QXR03:30:15U150.33
QXR03:30:15U150.33
03:30:15U
The input buffer contains 150.33

CASE 4. Ignore the first 3 characters peek at each one until U is reached. Read the time again.
Enter this data exactly as shown
QXR03:30:15U150.33
QXR03:30:15U150.33
03:30:15
Theinput buffer contains U150.33

CASE 5-1. cin.putback(ch) Extract the time leaving the rest of the data in the input buffer.
Enter this data exactly as shown
QXR03:30:15U150.33
QXR03:30:15U150.33
03:30:15
The input buffer contains QXRU150.33

CASE 5-2. cin.putback(ch) Insert characters to the input buffer.
Enter this data exactly as shown
QXR03:30:15U150.33
QXR03:30:15U150.33
The input buffer contains MGQXR03:30:15U150.33

CASE 6. Read the mixed input with cin.
Enter this data exactly as shown
QXR03:30:15U150.33
QXR03:30:15U150.33
3 30 15
U150.33

CASE 7. Count all zeros
Enter this data exactly as shown
QXR03:30:15U150.33
QXR03:30:15U150.33
3

CASE 8. Count the numbers in a sentence.
Enter this data exactly as shown
QXR03:30:15U150.33
QXR03:30:15U150.33
11

CASE 9. Count the numbers in a sentence using isdigit() function.
Enter this data exactly as shown
QXR03:30:15U150.33
QXR03:30:15U150.33
11

```
