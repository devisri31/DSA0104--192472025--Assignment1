TASK 9 – IMPLEMENT AND TEST FARE LOGIC

9.1 Aim

To implement the metro fare calculation logic and test normal journeys, peak hours, minimum balance requirements, and invalid inputs.

9.2 C++ Program

#include <iostream>
using namespace std;

int main() {
    int zone, hour;
    double balance, fare;

    cout << "Enter zone (1-Inner, 2-Middle, 3-Outer): ";
    if (!(cin >> zone) || zone < 1 || zone > 3) {
        cout << "Invalid zone\n";
        return 1;
    }

    cout << "Enter hour (0-23): ";
    if (!(cin >> hour) || hour < 0 || hour > 23) {
        cout << "Invalid hour\n";
        return 1;
    }

    cout << "Enter balance in rupees: ";
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

    cout << "Fare: Rs " << fare << '\n';

    if (balance - fare >= 50)
        cout << "Journey approved\n";
    else
        cout << "Journey denied - minimum balance rule\n";

    return 0;
}

9.3 Test Cases

Test| Input / Condition| Expected Result
1| Inner zone, 11 AM, balance ₹100| Fare ₹10; approved
2| Middle zone, 8 AM, balance ₹100| Fare ₹24; approved
3| Outer zone, 6 PM, balance ₹100| Fare ₹36; approved
4| 10 AM| Off-peak fare
5| 8 PM| Off-peak fare
6| Inner zone, balance ₹60| Approved; remaining balance ₹50
7| Inner zone, balance ₹59.99| Denied
8| Zone 4| Invalid zone
9| Negative balance| Invalid balance
10| Letters entered for hour| Invalid hour input

9.4 Verification

The fare is calculated using the base fare for the selected zone. During peak hours, a 20% surcharge is applied. The journey is approved only when the remaining balance is at least ₹50.

For example, an Inner-zone journey costs ₹10 off-peak. With a starting balance of ₹60, the remaining balance is exactly ₹50, so the journey is approved.

The peak-hour boundaries are important: 8 AM and 5 PM are peak times, while 10 AM and 8 PM are off-peak times.

9.5 Alternative Concept and Complexity Analysis

An alternative is to store test cases in an array or table and use a loop to execute each test automatically. This makes testing easier when many journeys and boundary conditions must be checked.

For (t) test cases, the testing process takes O(t) time. Each individual fare calculation takes O(1) time, and the program uses O(1) additional space when tests are processed one at a time.

Conclusion

The test cases check normal fares, peak-hour surcharges, minimum balance conditions, boundary times, and invalid inputs. The program should be compiled and executed for each test, and actual output screenshots should be saved as evidence.
