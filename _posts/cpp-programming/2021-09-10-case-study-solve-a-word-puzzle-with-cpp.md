---
layout: notes
title: "[C++ Programming] Case Study: Solve a Word Puzzle with C++"
meta: Find words in a Jumble
reference: 
category: cpp-programming
---

## Case Study: Find words in a Jumble

### Written Algorithm

Set position to 0

Loop 1
* Extract four characters from the scramble
* Call this substring test_word.
    - Loop 2
        - Read a word from the dictionary
        - Compare word with test_word
            - Word == test_word?
            - Yes: Print word and exit Loop 2
    - End of Loop 2
* Are there more letters in the scramble?
* No: Exit the Loop 1
* Yes: Reset Dictionary
* Increment position by 1

End of Loop 1

### Analysis

Sample input: axbirdatewtlakexxz

Get substring **axbi**rdatewtlakexxa

* NOT in dictionary

* Position = 1

Get substring a**xbir**datewtlakexxa

* NOT in dictionary

* Position = 2

Get substring ax**bird**atewtlakexxa

* bird found: print bird to screen

* Position = 3

...

Keep going until last group of 4 is encountered

axbirdatewtlak**exxa**


### Implementation

```cpp
//
// This program uses string processing operations to locate words hidden in a
// sequence of characters.
// The program requires the file dictionary_four_letter_words
//

#include <iostream>
#include <fstream>
#include <iomanip>
#include <string>

using namespace std;

int main(int argc, char* argv[])
{
    ifstream dictionary;
    string scramble = "";
    string word = "", test_word = "";
    int position;
    bool found = false;

    dictionary.open("dictionary_four_letter_words.txt");
    if (!dictionary)
    {
        cout << "ERROR: Could not open the file." << endl;
        system("pause");
        return 1;
    }
    cout << "File is open for read." << endl;

    // Using the dictionary find any four letter words in the scramble.

    // Enter the scramble
    cout << "Enter the word scramble in lowercase letters. " << endl;
    cin >> scramble;

    // Loop oever all 4-letter group in the scramble
    // Begin by getting 4 characters from the scramble
    position = 0;

    while (position <= scramble.length() - 4)
    {
        test_word = scramble.substr(position, 4);
        //cout << "Is " << test_word << " a word? " << endl;

        // Loop through dictionary comparing each word.
        while (!dictionary.eof())
        {:q
            // Get a word from the dictionary
            dictionary >> word;
            if (word == test_word)
            {
                cout << "The word " << test_word
                    << " was found in the scramble. " << endl;
                found = true;

                // Exit the nearest loop (while)
                // Program doesn't have to search through all the way to the
                // end.
                break;
            }
        } // End of inner while loop

        //if (!found)
        //  cout << "The string " << test_word << " is not a word." << endl;

        // Reset everything for the next substring from the scramble.
        dictionary.seekg(0, ios::beg);
        dictionary.clear();

        position++;
        found = false;
    } // End of outer while loop

    // Loop through the dictionary

    dictionary.close();
    cout << endl << endl;

    system("pause");

    return 0;
}

```
