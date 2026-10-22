TASK 6 – DESIGN THE CONTROL STRUCTURES

6.1 Decision-Making Statements

The metro fare system uses decision-making statements to calculate fares and decide whether a passenger can travel.

1. if–else statement: It is used to check whether the journey occurs during peak hours and whether the passenger has sufficient balance.

2. switch statement: It is used to select the base fare according to the travel zone.

3. Conditional operator: The "?:" operator can be used to select the final fare based on the peak-hour condition.

These statements make the fare calculation simple and organized.

6.2 Looping Statements

1. for loop: It is suitable when the number of journeys is known in advance.

2. Range-based for loop: It is suitable for processing every journey in an array or collection.

3. while loop: It is suitable when journeys are processed until a condition becomes false, such as when no more input is available.

For the given program, a range-based for loop is appropriate because the journeys are stored in an array.

6.3 Use of break and continue

The "break" statement terminates a loop or exits a switch statement.

The "continue" statement skips the current loop iteration and moves to the next iteration.

For example, "continue" can skip an invalid journey without processing its fare. A "break" statement can be used to exit a switch case after selecting the appropriate base fare.

If no case matches a switch expression, the default block executes if one is provided. Otherwise, control moves to the statement following the switch.

6.4 Pseudocode for Fare Computation

Algorithm: Calculate Metro Fare

Input: Zone, travel hour, card balance

Output: Final fare and remaining balance, or travel denial

1. Start.
2. Read the travel zone, travel hour and card balance.
3. Check whether the hour is between 8 and 10 AM or between 5 and 8 PM, using the specified boundary rules.
4. Use a switch statement to select the base fare:
   - Inner zone: 1000 paise.
   - Middle zone: 2000 paise.
   - Outer zone: 3000 paise.
5. If the journey occurs during peak hours, calculate the 20% surcharge using integer arithmetic.
6. Otherwise, retain the base fare.
7. Calculate the remaining balance after deducting the fare.
8. If the remaining balance is at least 5000 paise, approve the journey and deduct the fare.
9. Otherwise, deny the journey and retain the original balance.
10. Display the fare and remaining balance or the denial message.
11. Stop.

6.5 Completed C++ Program

The following program completes TODO 1 and TODO 2 using a switch statement and integer paise, as required.

#include <iomanip>
#include <iostream>
using namespace std;

enum class Zone { Inner, Middle, Outer };

constexpr int BASE_PAISE[] = {1000, 2000, 3000};
constexpr int PEAK_SURCHARGE_PERCENT = 20;
constexpr long long MIN_BALANCE_PAISE = 5000;

long long fare(Zone z, bool peak) {
    long long base = 0;

    switch (z) {
        case Zone::Inner:
            base = BASE_PAISE[0];
            break;

        case Zone::Middle:
            base = BASE_PAISE[1];
            break;

        case Zone::Outer:
            base = BASE_PAISE[2];
            break;

        default:
            return 0;
    }

    if (peak) {
        base += base * PEAK_SURCHARGE_PERCENT / 100;
    }

    return base;
}

bool canTravel(long long balance, long long f) {
    return f > 0 && balance - f >= MIN_BALANCE_PAISE;
}

int main() {
    long long balance = 10000;

    struct Trip {
        Zone zone;
        bool peak;
    };

    Trip trips[] = {
        {Zone::Inner, false},
        {Zone::Outer, true},
        {Zone::Middle, false}
    };

    for (const Trip& t : trips) {
        long long f = fare(t.zone, t.peak);

        if (canTravel(balance, f)) {
            balance -= f;

            cout << "Fare Rs " << f / 100 << '.'
                 << setw(2) << setfill('0') << f % 100
                 << setfill(' ');
        } else {
            cout << "Denied (low balance)";
        }

        cout << " balance Rs " << balance / 100 << '\n';
    }

    return 0;
}

6.6 Expected Output

Fare Rs 10.00 balance Rs 90
Fare Rs 36.00 balance Rs 54
Denied (low balance) balance Rs 54

6.7 Peak-Hour Boundary Testing

The peak-hour condition must be:

bool peak = (hour >= 8 && hour < 10) ||
            (hour >= 17 && hour < 20);

Time| Peak hour?
8:00 AM| Yes
10:00 AM| No
5:00 PM| Yes
8:00 PM| No

The given program receives a Boolean "peak" value directly, so the time-boundary test requires adding an hour-checking function or testing the condition separately.

6.8 Alternative Concept and Complexity Analysis

An alternative to the switch statement is to use a fare array indexed by the zone:

constexpr long long FARE[] = {1000, 2000, 3000};

The fare can be selected using an appropriate zone index. Both switch-based selection and array lookup have O(1) time complexity for a fixed number of zones.

The array requires storage proportional to the number of zones, or O(z), where z is the number of zones. A switch statement does not require a separate fare array, although the compiler may implement it using a jump table.

When a fourth zone is added, both designs must be updated. The array-based design requires a new fare entry and a reliable mapping between each zone and its index. The switch-based design requires an additional enum value and switch case.

Conclusion

The metro fare system uses switch statements for zone-based fare selection, if–else statements for travel eligibility, and a range-based for loop to process journeys. Integer paise ensures accurate monetary calculations, while the minimum-balance check prevents journeys that would leave less than ₹50 on the card.
