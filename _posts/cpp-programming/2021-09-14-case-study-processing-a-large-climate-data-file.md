---
layout: notes
title: "[C++ Programming] Case Study: Processing a Large Climate Data File"
meta: fstream, iomanip, file open, file read, file close, getline, eof, substr,
    at, length and find
reference: 
category: cpp-programming
---

## Case Study: Processing a Large Climate Data File

### Implementation

```cpp
//
// Program to read and process weather station data
// Data is input one full line at a time and then processed with
// string manipulation functions
//
// It demonstrates fstream, iomanip, file open, file read, file close,
// getline, eof, substr, at, length and find.
//
// Actual weather station data is employed
//

#include <iostream>
#include <fstream>
#include <iomanip>
#include <string>

using namespace std;

int main(int argc, char* argv[])
{
    // Variables
    string dataline = "";
    string station = "";
    string tmax_s, tmin_s;
    unsigned int pos_satation_name = 0;
    unsigned int pos_date = 0;
    unsigned int pos_tmax = 0;
    unsigned int pos_tmin = 0;
    int bad_records = 0;
    float tmax = 0, tmin = 0;
    ifstream infile;
    ofstream outfile;

    cout << "WEATHER STATION DATA" << endl << endl;
    cout << "Open the data file." << endl << endl;
    infile.open("AL_Weather_Station.txt");

    if (!infile)
    {
        cout << "Unable to open the input file." << endl;
        system("pause");
        return 1;
    }
    else
    {
        cout << "Data file opened." << endl;
    }

    outfile.open("Filtered_AL_Weather_Station.txt");
    if (!outfile)
    {
        cout << "Unable to open the output file." << endl;
        system("pause");
        return 2;
    }
    else
    {
        cout << "Output file opened." << endl;
    }

    cout << endl;

    cout << "Use the first line of the file to find the column positions."
        << endl;
    getline(infile, dataline);      // First line
    outfile << dataline << endl;    // Write to output file
    cout << "Line 1: " << dataline << endl;

    // Use headers to find max and min temp columns
    pos_tmax = dataline.find("TMAX");
    if (pos_tmax <= dataline.length())
    {
        cout << "TMAX begins at column: " << pos_tmax << endl;
    }
    else
    {
        cout << "TMAX not found." << endl;
        return 2;
    }

    pos_tmin = dataline.find("TMIN");
    if (pos_tmin <= dataline.length())
    {
        cout << "TMIN begins at column: " << pos_tmin << endl;
    }
    else
    {
        cout << "TMIN not found." << endl;
        return 2;
    }

    // If you want to pull out data from any other columns, just add
    // the same template of the code shown above.

    cout << "Read the second line from the file." << endl;

    getline(infile, dataline);
    outfile << dataline << endl;
    cout << "Line 2: " << dataline << endl;

    while (!infile.eof())
    {
        // Read the lines with data
        getline(infile, dataline);

        // Extract tmax and tmin from dataline
        tmax_s = dataline.substr(pos_tmax, 5);
        tmin_s = dataline.substr(pos_tmin, 5);

        // if (tmax_s = "-9999")    // This also works!

        // Conver the string types to float
        tmax = stof(tmax_s);    // Convert string tmax_s to float tmax
        tmin = stof(tmin_s);    // Convert string tmax_s to float tmin

        // stoi: to convert string to int
        // stod: to convert string to double

        // Test for bad data flag. If good data then write to new file.
        if (tmax != -9999 && tmin != -9999)
            outfile << dataline << endl;
        else
            bad_records++;
    } // end while

    // Close the files
    infile.close();
    outfile.close();

    cout << "New file created with bad records filtered out." << endl;
    cout << "There were " << bad_records << " filtered out." << endl;

    cout << "\n\n";

    system("pause");

    return 0;
}
```
![climate-data-console]({{site.baseurl}}/img/cpp-programming/climate-data-console.png){:.inline-img-w900}

![climate-data-txt]({{site.baseurl}}/img/cpp-programming/climate-data-txt.png){:.inline-img-w900}

![filtered-climate-data-txt.png]({{site.baseurl}}/img/cpp-programming/filtered-climate-data-txt.png){:.inline-img-w900}
