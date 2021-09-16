---
layout: notes
title: "[C++ Programming] Case Study: Processing a Large Climate Data File
    (Using Buffer Operations)"
meta: fstream, iomanip, file open, file read, file close, getline, eof, 
reference: 
category: cpp-programming
---

## Case Study: Processing a Large Climate Data File (Using Buffer Operations)

### Implementation

```cpp
//
// Program to read and process weather station data
// Data is read from the input buffer
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
    string station_name = "";
    string date = "";
    string space = " ";
    float mdpr = 0.0, dapr = 0.0, prcp = 0.0, snwd = 0.0, snow = 0.0;
    float tmax = 0.0, tmin = 0.0, awnd = 0.0;
    int i = 0;
    char letter;
    ifstream infile;
    ofstream outfile;

    cout << "WEATHER STATION DATA" << endl << endl;

    cout << "Open the files." << endl << endl;

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

    // Set the output formatting
    outfile << fixed;

    // Read the first line (column headers)
    getline(infile, dataline);
    outfile << dataline << endl;

    // Read the second line (dashes) from the file
    getline(infile, dataline);
    outfile << dataline << endl;

    while (!infile.eof())
    {
        // Read a line of data from the buffer
        infile >> station;

        // Ignore the space after Station ID
        infile.ignore(1);
            // Can't use getline as it will read everything in the line
            // Can't use the string variable because it won't read the spaces
            // The only way to do it is to read it char by char and concatenate

        // Read the station name letter by letter
        for (i = 0; i < 50; i++)
        {
            infile.get(letter); // infile >> letter;
            station_name += letter;
        }

        // Now it is easy to read the remaining data
        infile >> date;
        infile >> mdpr >> dapr >> prcp >> snwd >> snow >> tmax >> tmin >> awnd;

        // Write the data to the outfile
        if (tmax != -9999 && tmin != -9999)
        {
            outfile << station << space << station_name << space
                << date << space
                << left // All remaninig fields are left justified
                << setw(8) << setprecision(0) << mdpr << space
                << setw(8) << setprecision(0) << dapr << space
                << setw(8) << setprecision(2) << prcp << space
                << setw(8) << setprecision(1) << snwd << space
                << setw(8) << setprecision(0) << snow << space
                << setw(8) << setprecision(0) << tmax << space
                << setw(8) << setprecision(0) << tmin << space
                << setw(8) << setprecision(0) << awnd << space
                << endl;
        }
        station_name = "";
    }

    // Close the files
    infile.close();
    outfile.close();
    cout << "Closed the files." << endl;

    cout << "\n";

    system("pause");

    return 0;
}
```
![buf-climate-data-console]({{site.baseurl}}/img/cpp-programming/buf-climate-data-console.png){:.inline-img-w900}

![climate-data-txt]({{site.baseurl}}/img/cpp-programming/climate-data-txt.png){:.inline-img-w900}

![filtered-climate-data-txt.png]({{site.baseurl}}/img/cpp-programming/filtered-climate-data-txt.png){:.inline-img-w900}
