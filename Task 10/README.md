TASK 10 – COMPARE EXPECTATIONS WITH EXECUTION

10.1 Aim

To compare floating-point and integer-paise fare totals, identify possible integer overflow, and examine compiler warnings using "-Wall -Wextra".

10.2 C++ Program

The following program assumes every journey costs ₹30. This provides a consistent example for comparing totals at three network sizes.

#include <iostream>
#include <iomanip>
using namespace std;

int main() {
    const int farePaise = 3000;
    const double fareRupees = 30.00;
    const int counts[] = {20000, 500000, 3000000};

    cout << fixed << setprecision(2);

    for (int n : counts) {
        double doubleTotal = 0.0;
        long long paiseTotal = 0;

        for (int i = 0; i < n; ++i) {
            doubleTotal += fareRupees;
            paiseTotal += farePaise;
        }

        cout << "Journeys: " << n << '\n';
        cout << "Double total: Rs "
             << doubleTotal << '\n';
        cout << "Integer-paise total: Rs "
             << paiseTotal / 100.0 << '\n';
        cout << "Difference: Rs "
             << doubleTotal - paiseTotal / 100.0
             << "\n\n";
    }

    int networkTotal = 3000000 * farePaise;
    cout << "Int total in paise: "
         << networkTotal << '\n';

    return 0;
}

10.3 Expected Mathematical Totals

Journeys per day| Total at ₹30 per journey| Total in paise
20,000| ₹6,00,000| 60,000,000
500,000| ₹1,50,00,000| 1,500,000,000
3,000,000| ₹9,00,00,000| 9,000,000,000

The mathematical totals agree when the same fare is added. However, floating-point calculations may introduce small representation errors. The displayed difference may still be ₹0.00 because the output is rounded to two decimal places.

Important: These totals assume a fixed ₹30 fare for every journey; actual metro revenue will vary according to zone and peak-hour usage.

10.4 Does "int" Overflow?

On a typical system with a 32-bit signed "int", the maximum value is 2,147,483,647.

- At 20,000 journeys, 60,000,000 paise fits.
- At 500,000 journeys, 1,500,000,000 paise fits.
- At 3,000,000 journeys, 9,000,000,000 paise exceeds the limit.

Therefore, a 32-bit "int" cannot safely store the whole-network total in paise. The multiplication in the program can overflow, producing undefined behaviour in C++.

The correct declaration is:

long long networkTotal =
    3000000LL * 3000;

Using "3000000LL" ensures the multiplication is performed using "long long".

10.5 Compiler Warnings

Compile the program using:

g++ -std=c++17 -Wall -Wextra task10.cpp -o task10

- "-Wall" enables many common compiler warnings.
- "-Wextra" enables additional warnings.
- Warnings can reveal suspicious conversions, unused variables, or other potential problems.

The exact warnings depend on the compiler version and code. Record the warnings actually produced by your compiler; do not claim that a warning appeared if it did not.

10.6 Alternative Concept and Complexity Analysis

Data type| Advantage| Limitation
"int"| Uses less memory| Can overflow for the network total in paise
"long long"| Stores large integer totals safely for this example| Has a finite maximum value
"double"| Supports fractional values| Cannot represent every decimal amount exactly

Each addition takes O(1) time. For (n) journeys, the total calculation takes O(n) time. When processing journeys one at a time, the additional space is O(1).

Integer paise is recommended for exact money calculations, while "long long" is suitable for accumulating large totals.

Conclusion

The comparison shows that a 32-bit "int" is insufficient for the whole-network total in paise when every journey costs ₹30. Integer paise avoids floating-point representation issues, and "long long" prevents overflow for the totals in this example. Actual compiler output and measurements must be recorded after execution.
