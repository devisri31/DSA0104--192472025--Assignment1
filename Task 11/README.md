TASK 11 – RECOMMEND AND DEFEND THE FINAL DESIGN

11.1 Aim

To recommend a reliable and maintainable design for the metro smart-card fare system based on data types, constants, object-oriented programming, and testing.

11.2 Recommended Design

I recommend an object-oriented design using a "SmartCard" class, an "enum class" for zones, named constants for fare rules, and integer paise for all money calculations.

Component| Recommended choice| Reason
Zone| "enum class Zone"| Represents valid zones clearly
Fare| Integer paise| Avoids floating-point rounding issues
Balance| "long long"| Supports large balances and totals
Peak status| "bool"| Represents peak or off-peak conditions
Fare rules| "constexpr" constants| Keeps rules in one place
Smart card| "SmartCard" class| Protects the balance through controlled functions
Fare calculation| Separate function| Makes fare rules easier to test and maintain

11.3 How a Fare Revision Is Carried Out

The base fares and surcharge should be declared in one place.

constexpr int BASE_PAISE[] = {
    1000, 2000, 3000
};

constexpr int PEAK_SURCHARGE_PERCENT = 20;
constexpr long long MIN_BALANCE_PAISE = 5000;

If the fare changes, the corresponding constant can be updated and the program recompiled. Centralising the values prevents inconsistent fares across different parts of the program.

11.4 Evidence from Testing

The following mathematical checks support the design:

Test| Expected result
Inner-zone off-peak journey| ₹10
Middle-zone peak journey| ₹24
Outer-zone peak journey| ₹36
Balance ₹60, fare ₹10| Approved; ₹50 remains
Balance ₹59.99, fare ₹10| Denied
Whole-network total at ₹30 × 3,000,000 journeys| ₹9,00,00,000

The whole-network total is ₹9,00,00,000, or 9,000,000,000 paise. A 32-bit signed "int" cannot safely store this paise total, so "long long" is recommended.

These are calculated expected results. Actual execution results and compiler warnings should be recorded separately after running the program.

11.5 Limitations of the Design

1. The current design supports only three zones.
2. The student and senior-citizen concession percentage is not specified in the assignment, so it must be confirmed before implementation.
3. Compiled-in fare constants require recompilation when fares change.
4. The design needs further modification to support weekend discounts and monthly passes.
5. A production system would also need persistent transaction records and suitable error handling.

11.6 Will the Design Work for the Whole Network?

The design can process journeys using the same fare and balance rules at a larger scale because each fare calculation and balance check takes O(1) time.

Processing (n) journeys takes O(n) time. Processing one journey at a time requires O(1) additional working space, excluding stored transaction records.

Using "long long" for accumulated money totals avoids the 32-bit "int" overflow demonstrated by the whole-network calculation.

11.7 Alternative Concept and Complexity Analysis

Instead of compiling fare values into the program, the fare table could be loaded from a configuration file when the system starts.

- Startup time: O(z), where (z) is the number of zones read.
- Fare-table storage: O(z).
- Fare lookup: O(1) when using a directly indexed table.
- Advantage: Fare revisions can be made through configuration rather than recompiling the program.
- Limitation: The program must validate the file and handle missing or incorrect values.

Conclusion

An object-oriented design with private card balances, centralised fare constants, integer-paise calculations, and "long long" totals is suitable for the current metro system. A configuration-based fare table would improve maintainability when fares change frequently. The final design should be validated using actual test results before deployment.
