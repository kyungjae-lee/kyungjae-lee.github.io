---
layout: notes
title: "[C++ Programming] String Processing" 
meta: length(), size(), find(), sutstr(), at(), erase(), insert(), replace(), append(), reversit()
reference: 
category: cpp-programming
---

[!] Note: string data means ASCII encoded data

[!] Note: Be careful about the type mismatch!

## Examples

### Example 1

Program to illustrate functions on a string constant.

```cpp
//
// Program to illustrate functions on a string constant
// Functions: length, size, find, substr, at, erase, insert, replace, append
//

#include <iostream>
#include <fstream>
#include <iomanip>
#include <string>

using namespace std;

int main(int argc, char *argv[])
{
    // Variables

    string sentence = "CS 121 meets from 11:10 to 12:30 on Monday and Wednesday.";
    string ecnetnes = ""; // To be robust, initialize the string to a null string.
    string part = "";
    char letter;
    unsigned int len = 0, position = 0, i = 0;

    cout << "STRING PROCESSING FUNCTIONS" << endl << endl;
    cout << "The sentence is: ";
    cout << sentence << endl << endl;


    // length
    // Calculates how many characters there are in a given sentence.
    // Returns an integer value.
    cout << "length()" << endl;
    len = sentence.length();
    cout << "The length of the sentence is: " << len << endl;

    cout << endl;


    // size
    cout << "size()" << endl;
    cout << "The size of the sentence is: " << sentence.size() << endl;
    // Embedding the function works as well.

    cout << endl;


    // find
    // Finds the position of a substring within a larger string
    // Returns an integer value representing the position of the string we are
    // looking for. (position counts from 0)
    // If 'find' didn't find the substring, it will return a number representing
    // failure. (4294967295, which is a very big number, this number may vary
    // in differenc computer environment so use 'string::npos' instead)
    cout << "find()" << endl;
    position = sentence.find("121");
    cout << "The substring '121' starts at position: " << position << endl;

    // Always do the test after calling the 'find' function
    position = sentence.find("1234");
    //if (position == string::npos)   // did not work in my environment
    if (position <= sentence.length())
        cout << "The substring '1234' starts at position: " << position << endl;
    else
        cout << "The substring '1234' was not found." << endl;

    position = sentence.find("12");
    if (position <= sentence.length())
        cout << "The substring '12' starts at position: " << position << endl;
    else
        cout << "The substring 12 was not found." << position << endl;

    // If you use the find function with only one argument, which is the
    // stubstring you want to find, it will always start finding it from the
    // begining of the string each time it's called.
    position = sentence.find("12");
    if (position <= sentence.length())
        cout << "The substring '12' starts at position: " << position << endl;
    else
        cout << "The substring 12 was not found." << position << endl;

    // To find the next occurence of '12',
    position = sentence.find("12", position + 1);
    if (position <= sentence.length())
        cout << "The substring '12' starts at position: " << position << endl;
    else
        cout << "The substring 12 was not found." << position << endl;

    cout << endl;


    // substr
    // Extracts a substring within a larger string.
    // First argument: The position within a larger string that you want to begin.
    // Second argument: How many characters do you want from that position
    // onward.
    // [!] Note: 'substr' does not delete the substring from the original
    // string.
    cout << "substr()" << endl;
    cout << "The substring of 10 characters at position 7 is: "
        << sentence.substr(7, 10) << endl;

    part = sentence.substr(7, 10);
    cout << "The substring of 10 characters at position 7 is: "
        << part << endl;

    cout << endl;


    // at
    // Extracts a letter from a string.
    cout << "at()" << endl;
    letter = sentence.at(10);
    // letter = sentence[10]; // Same! It's just that it's treating 'sentence'
    // as an array of character instead of as string.
    cout << "The character at position 10 is: " << letter << endl;

    cout << endl;


    // erase
    // First argument: The position in a given string where you want to begin
    // erasing characters.
    // Second argument: The number of characters you want to erase.
    // First, you need to 'find' what you want to erase.
    cout << "erase()" << endl;
    position = sentence.find("11:10");
    if (position <= sentence.length())
    {
        cout << "Erase the time '11:10' from the sentence." << endl;
        sentence.erase(position, 5); // Erase 5 characters beginning at position.
        cout << sentence << endl;
    }
    else
        cout << "The substring was not found." << endl;

    cout << endl;


    // insert
    cout << "insert()" << endl;
    cout << "Insert '12:45' as the new start time." << endl;
    sentence.insert(position, "12:45");
    cout << sentence << endl;

    cout << endl;


    // replace
    // Combination of 'erase' and 'insert'
    // First argument: The position where you want to replace something
    // Second argument: The number of characters you want to replace
    cout << "replace()" << endl;
    position = sentence.find("12:30");
    if (position <= sentence.length())
    {
        cout << "Replace the time '12:30' with '2:05'." << endl;
        sentence.replace(position, 5, "2:05");
    }
    else
        cout << "The substring was not found." << endl;
    cout << sentence << endl;

    cout << endl;


    // append
    // Appends a string to the end of an existing string.
    cout << "append()" << endl;
    sentence.append(" in classroom 307.");

    // Erase the first dot to make the sentence cleaner.
    position = sentence.find(".");
    // [!] Note: Remember that the 'find' function takes STRING as its
    // argument. Cannot do find('.').
    if (position <= sentence.length())
    {
        cout << "Erase the first dot to make the sentence cleaner" << endl;
        sentence.erase(position, 1);
        cout << sentence << endl;
    }
    else
        cout << "The substring was not found." << endl;

    cout << endl;

    system("pause");

    return 0;
}
```
```text
STRING PROCESSING FUNCTIONS

The sentence is: CS 121 meets from 11:10 to 12:30 on Monday and Wednesday.

length()
The length of the sentence is: 57

size()
The size of the sentence is: 57

find()
The substring '121' starts at position: 3
The substring '1234' was not found.
The substring '12' starts at position: 3
The substring '12' starts at position: 3
The substring '12' starts at position: 27

substr()
The substring of 10 characters at position 7 is: meets from
The substring of 10 characters at position 7 is: meets from

at()
The character at position 10 is: t

erase()
Erase the time '11:10' from the sentence.
CS 121 meets from  to 12:30 on Monday and Wednesday.

insert()
Insert '12:45' as the new start time.
CS 121 meets from 12:45 to 12:30 on Monday and Wednesday.

replace()
Replace the time '12:30' with '2:05'.
CS 121 meets from 12:45 to 2:05 on Monday and Wednesday.

append()
Erase the first dot to make the sentence cleaner
CS 121 meets from 12:45 to 2:05 on Monday and Wednesday in classroom 307.

```

### Example 2

Program to reverse a sentence with string processing functions.

```cpp
//
// Program to revese a sentence with string processing functions
// Functions: + reversit()
// 

#include <iostream>
#include <fstream>
#include <iomanip>
#include <string>

using namespace std;

string reversit(string line);

int main(int argc, char *argv[])
{
    // Variables
    
    string sentence = "";
    string ecnetnes = ""; // To be robust, initialize the string to a null string.
    string part = "";
    char letter;
    unsigned int len = 0, i = 0;
    int position = 0; // to make it able to be negative


    cout << "Enter a sentence: ";
    getline(cin, sentence); // 'cin' cannot be used! Becareful!!!

    // Reverse the sentence
    cout << "Reverse the sentence." << endl << endl;

    position = sentence.length() - 1;

    for (i = 0; position >= 0; position--)
    {
        letter = sentence.at(position);
        ecnetnes += letter; // Concatenate the letter
    }

    cout << "The reversed sentence is: " << ecnetnes << endl;

    // Call function to reverse the sentence

    ecnetnes = reversit(sentence);
    cout << "The reversed sentence from function reversit is: " << ecnetnes 
        << endl;

    return 0;
}


//
// Function reversit()
// 

string reversit(string line)
{
    string invert_line = "";
    int position = 0;


    for (position = line.length() - 1; position >= 0; position--)
        invert_line += line.at(position);

    return invert_line;
}
```
```text
Enter a sentence: Hi my name is Kyungjae Lee.
Reverse the sentence.

The reversed sentence is: .eeL eajgnuyK si eman ym iH
The reversed sentence from function reversit is: .eeL eajgnuyK si eman ym iH

```
