TASK 8 – READ AND PRINT DATA SAFELY

8.1 Aim

To read metro journey details safely, handle invalid user input, and display the fare report using formatted output in C++.

8.2 C++ Program

#include <iostream>
#include <iomanip>
#include <limits>
using namespace std;

int main() {
    int zone, hour;
    double balance, fare;

    cout << "Enter zone (1-Inner, 2-Middle, 3-Outer): ";
    if (!(cin >> zone)) {
        cout << "Invalid zone input\n";
        return 1;
    }

    if (zone < 1 || zone > 3) {
        cout << "Invalid zone\n";
        return 1;
    }

    cout << "Enter hour (0-23): ";
    if (!(cin >> hour)) {
        cout << "Invalid hour input\n";
        return 1;
    }

    if (hour < 0 || hour > 23) {
        cout << "Invalid hour\n";
        return 1;
    }

    cout << "Enter card balance in rupees: ";
    if (!(cin >> balance) || balance < 0) {
        cout << "Invalid balance\n";
        return 1;
    }

    if (zone == 1)
        fare = 10;
    else if (zone == 2)
        fare = 20;
    else
        fare = 30;

    bool peak = (hour >= 8 && hour < 10) ||
                (hour >= 17 && hour < 20);

    if (peak)
        fare += fare * 0.20;

    cout << fixed << setprecision(2);
    cout << "\n--- Metro Journey Report ---\n";
    cout << left << setw(20) << "Zone:"
         << zone << '\n';
    cout << left << setw(20) << "Travel hour:"
         << hour << '\n';
    cout << left << setw(20) << "Peak period:"
         << (peak ? "Yes" : "No") << '\n';
    cout << left << setw(20) << "Fare (Rs):"
         << fare << '\n';
    cout << left << setw(20) << "Balance (Rs):"
         << balance << '\n';

    if (balance - fare >= 50)
        cout << "Journey status: Approved\n";
    else
        cout << "Journey status: Denied - low balance\n";

    return 0;
}

8.3 Explanation

- "cin.fail()" / input validation: Checking "cin" after reading detects input failures, such as entering letters instead of a number.
- "cin.clear()" and "cin.ignore()": These can be used to reset the input stream and discard invalid input so the program can ask again. This program instead displays an error and exits.
- "setw()" and "left": Align the report into neat columns.
- "fixed" and "setprecision(2)": Display money with two decimal places.
- "setfill()": Can fill unused field positions with a chosen character when needed.

8.4 Sample Test

Input:

Enter zone (1-Inner, 2-Middle, 3-Outer): 3
Enter hour (0-23): 18
Enter card balance in rupees: 100

Expected output:

--- Metro Journey Report ---
Zone:               3
Travel hour:        18
Peak period:        Yes
Fare (Rs):          36.00
Balance (Rs):       100.00
Journey status: Approved

8.5 Alternative Concept and Complexity Analysis

An alternative is to read the entire input using "getline()" and convert it with "stoi()" inside a "try-catch" block. This allows the program to handle conversion errors and request valid input again.

For input containing (L) characters, reading and processing the input takes O(L) time. The input buffer requires O(L) space. For a fixed number of journey fields, the overall fare calculation and report generation take O(1) time and O(1) additional space.

Conclusion

Safe input validation prevents invalid values from being used in fare calculations. Formatted output improves readability and helps passengers and operators understand the journey details clearly.
