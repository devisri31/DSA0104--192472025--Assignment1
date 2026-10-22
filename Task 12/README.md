TASK 12 – Re-evaluate and Adapt the Design

A. Impact Analysis (2 Marks)

The new requirements affect the original design as follows:

- Constants: Add "AIRPORT_FARE = 6000" paise and "WEEKEND_DISCOUNT_PERCENT = 10".
- Enum: Add "Airport" to the "Zone" enumeration.
- Fare expression: Add the weekend discount rule. The discount must not combine with the peak surcharge.
- Switch statement: Add a case for the Airport zone. Alternatively, use a fare table indexed by zone.
- Classes: Retain "SmartCard" for balance management and introduce a "Pass" class to store two selected zones and check pass validity.

B. Evaluation of the Original Design (2 Marks)

The original switch-based fare logic can be modified to support the Airport zone, but every new zone requires another case. A fare table is easier to maintain because fare values are stored in one place.

Worked examples:

Condition| Calculation| Fare
Airport, weekday off-peak| ₹60| ₹60
Airport, weekday peak| ₹60 + 20%| ₹72
Airport, weekend during peak hours| ₹60 − 10%| ₹54
Journey in a zone covered by a valid monthly pass| No fare deduction| ₹0

The weekend rule takes priority over the peak surcharge. The "SmartCard" class can still enforce the minimum balance of ₹50, while the "Pass" class handles unlimited journeys in its two selected zones.

C. Adaptation or Redesign (2 Marks)

I recommend modifying the existing design by using a fare table, a separate fare-calculation function, a "SmartCard" class and a "Pass" class.

C++ Program

#include <iostream>
#include <iomanip>
using namespace std;

enum class Zone { Inner, Middle, Outer, Airport };

constexpr long long BASE_FARE[] = {
    1000, 2000, 3000, 6000
};

constexpr int PEAK_SURCHARGE = 20;
constexpr int WEEKEND_DISCOUNT = 10;
constexpr long long MIN_BALANCE = 5000;

bool isPeak(int hour) {
    return (hour >= 8 && hour < 10) ||
           (hour >= 17 && hour < 20);
}

long long calculateFare(Zone zone, int hour, bool weekend) {
    int index = static_cast<int>(zone);

    if (index < 0 || index > 3 || hour < 0 || hour > 23)
        return -1;

    long long fare = BASE_FARE[index];

    if (weekend)
        fare -= fare * WEEKEND_DISCOUNT / 100;
    else if (isPeak(hour))
        fare += fare * PEAK_SURCHARGE / 100;

    return fare;
}

class SmartCard {
    long long balance;

public:
    SmartCard(long long amount) : balance(amount) {}

    bool deduct(long long fare) {
        if (fare < 0 || balance - fare < MIN_BALANCE)
            return false;

        balance -= fare;
        return true;
    }

    long long getBalance() const {
        return balance;
    }
};

class Pass {
    Zone first, second;
    bool active;

public:
    Pass(Zone a, Zone b, bool valid = true)
        : first(a), second(b), active(valid) {}

    bool covers(Zone zone) const {
        return active && (zone == first || zone == second);
    }
};

void showMoney(long long paise) {
    cout << "Rs " << paise / 100 << "."
         << setw(2) << setfill('0') << paise % 100
         << setfill(' ');
}

int main() {
    SmartCard card(20000); // Rs 200
    Pass monthlyPass(Zone::Inner, Zone::Middle);

    long long fare = calculateFare(Zone::Airport, 18, true);

    cout << "Airport weekend fare: ";
    showMoney(fare);
    cout << '\n';

    if (card.deduct(fare))
        cout << "Airport journey: Fare deducted\n";
    else
        cout << "Airport journey: Rejected\n";

    cout << "Remaining balance: ";
    showMoney(card.getBalance());
    cout << '\n';

    if (monthlyPass.covers(Zone::Inner))
        cout << "Inner-zone journey: Rs 0.00 (covered by pass)\n";

    return 0;
}

Expected Output

Airport weekend fare: Rs 54.00
Airport journey: Fare deducted
Remaining balance: Rs 146.00
Inner-zone journey: Rs 0.00 (covered by pass)

Note: These are expected results calculated from the code. Execute the program and capture your actual output screenshot for submission.

D. Evidence-Based Defence (2 Marks)

I choose to modify rather than completely replace the original design because the "SmartCard" class already protects the balance and enforces the minimum balance rule.

- The fare table makes fare revisions easier and avoids repeating fare values.
- Separate weekend and peak conditions prevent the two adjustments from being combined.
- The "Pass" class checks whether a journey belongs to either of the two selected zones.
- Fare lookup, pass-zone checking and balance deduction each take O(1) time.
- The design uses O(1) additional space for each card and pass.

The main limitation is that this simple "Pass" class does not yet check expiry dates or monthly renewal. These features would be required in a production system.

Conclusion: The modified object-oriented design supports the Airport zone, weekend discounts and monthly passes while maintaining exact paise-based calculations and the stored-value card's minimum balance rule.
