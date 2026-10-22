TASK 3 – CHOOSE DATA TYPES AND CHECK TYPE COMPATIBILITY

3.1 Data Types Used in the Metro Fare System

Appropriate data types are necessary to ensure accurate fare calculation, prevent overflow and store information efficiently.

Value| Data Type| Reason
Fare in paise| "long long"| Stores monetary values accurately as integers
Card balance in paise| "long long"| Prevents negative balance and supports large values
Peak-hour status| "bool"| Stores true or false
Zone| "enum class Zone"| Represents Inner, Middle and Outer zones safely
Hour of travel| "int"| Stores the hour from 0 to 23
Passenger category| "char" or "enum class"| Represents passenger categories
Journey count| "long long"| Supports large numbers of journeys
Surcharge percentage| "constexpr int"| Stores the fixed surcharge value
Fare calculation result| "long long"| Maintains integer precision
Displayed fare in rupees| "double" or formatted integer paise| Used for presentation; integer paise is preferred for exactness

3.2 Size and Range of Data Types

The following table shows common sizes and ranges on a typical modern system. Actual sizes should be verified on the compiler used for the assignment.

Data Type| Typical Size| Approximate Range
"bool"| 1 byte| "false" or "true"
"char"| 1 byte| −128 to 127 or 0 to 255
"int"| 4 bytes| −2,147,483,648 to 2,147,483,647
"unsigned int"| 4 bytes| 0 to 4,294,967,295
"long long"| 8 bytes| −9.22 × 10¹⁸ to 9.22 × 10¹⁸
"float"| 4 bytes| Approximately 6–7 decimal digits of precision
"double"| 8 bytes| Approximately 15–16 decimal digits of precision

The actual sizes can be checked using the "sizeof" operator.

#include <iostream>
#include <climits>
using namespace std;

int main() {
    cout << "Size of bool: " << sizeof(bool) << " bytes\n";
    cout << "Size of char: " << sizeof(char) << " bytes\n";
    cout << "Size of int: " << sizeof(int) << " bytes\n";
    cout << "Size of unsigned int: " << sizeof(unsigned int) << " bytes\n";
    cout << "Size of long long: " << sizeof(long long) << " bytes\n";
    cout << "Size of float: " << sizeof(float) << " bytes\n";
    cout << "Size of double: " << sizeof(double) << " bytes\n";

    cout << "INT_MAX: " << INT_MAX << '\n';
    cout << "LLONG_MAX: " << LLONG_MAX << '\n';

    return 0;
}

3.3 Why Money Should Be Stored in Integer Paise

Money should be stored as integer paise instead of "double" rupees because floating-point numbers may introduce rounding errors.

For example, ₹10.50 is stored as 1050 paise. This representation allows exact addition and subtraction of monetary amounts expressed in whole paise.

The 20% peak surcharge can be calculated using integer arithmetic:

long long fare = 3000;  // Rs 30.00
long long finalFare = fare + fare * 20 / 100;

The result is 3600 paise, equivalent to ₹36.00.

This method avoids floating-point representation errors in monetary calculations.

3.4 Type Compatibility in C++

C++ automatically converts values when different data types are used in an expression. These conversions can affect the result.

Example 1: Integer division

int a = 7, b = 2;
double result = a / b;

The result is "3.0", not "3.5", because integer division occurs before the result is assigned to "double".

Correct method:

double result = static_cast<double>(a) / b;

The result is "3.5".

Example 2: Integer to Boolean

bool status = 5;

The value of "status" becomes "true" because a nonzero value converts to "true".

Example 3: Character to Integer

char ch = 'A';
cout << ch + 1;

The character is promoted to an integer during addition. With the usual ASCII-compatible character encoding, the output is "66".

These examples show why conversions must be understood and controlled.

3.5 Is int Enough for the Daily Network Collection?

The metro network processes up to 3,000,000 journeys per day.

Assuming the maximum base fare is ₹30 per journey and ignoring surcharges and concessions:

Total collection = 3,000,000 × ₹30

Total collection = ₹90,000,000.

In paise, this is:

90,000,000 × 100 = 9,000,000,000 paise.

A typical 32-bit signed "int" has a maximum value of 2,147,483,647. Therefore, "int" is not sufficient to store the total in paise.

A "long long" is appropriate because its range is much larger. If the total is stored in rupees as an integer, ₹90,000,000 fits within a typical 32-bit signed "int", but paise is preferred for exact monetary calculations.

3.6 Alternative Concept and Complexity Analysis

If the system stored money using "double" rupees instead of "long long" paise, the program could represent values such as ₹10.50 directly. However, many decimal fractions cannot be represented exactly in binary floating-point format, so small rounding errors may occur.

Both integer addition and floating-point addition have O(1) time complexity per operation. On a typical system, both "long long" and "double" occupy 8 bytes per value.

To investigate rounding errors, the following program can be executed:

#include <iostream>
#include <iomanip>
using namespace std;

int main() {
    double totalRupees = 0.0;
    long long totalPaise = 0;

    for (int i = 0; i < 100000; i++) {
        totalRupees += 0.10;
        totalPaise += 10;
    }

    cout << fixed << setprecision(10);
    cout << "Double total: " << totalRupees << '\n';
    cout << "Paise total: " << totalPaise / 100.0 << '\n';

    return 0;
}

The program compares the two totals. Its actual output should be recorded after execution rather than assumed in advance.

Conclusion

The metro fare system should use "long long" for monetary values stored in paise, "bool" for logical conditions, "int" for hours and "enum class" for zones. The "sizeof" operator and limits from "<climits>" help verify storage requirements. Integer paise avoids floating-point rounding issues, while "long long" safely handles the total collection in paise for the expected network size.
