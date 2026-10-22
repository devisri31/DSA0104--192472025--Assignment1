TASK 2 – USE TOKENS, KEYWORDS, IDENTIFIERS AND CONSTANTS CORRECTLY

2.1 Five Kinds of Tokens in C++

Tokens are the smallest meaningful units of a C++ program.

1. Keywords: Reserved words with predefined meanings. Examples: "int", "class", "if", "switch", "return", and "constexpr".

2. Identifiers: Names given to variables, functions and classes. Examples: "fare", "balance", "SmartCard", and "canTravel".

3. Constants: Fixed values that do not change during program execution. Examples: "1000", "2000", "3000", and "5000".

4. Operators: Symbols used to perform operations. Examples: "+", "-", "*", "/", "%", "==", "&&", and ">=".

5. Punctuators: Symbols used to organize program statements and structures. Examples: ";", "{}", "()", "[]", and ",".

These tokens work together to implement the metro fare-calculation system.

2.2 Difference Between #define, const and constexpr

1. #define: It is a preprocessor directive that replaces a name with a specified value before compilation.

Example:

#define MIN_BALANCE_PAISE 5000

It does not provide normal C++ type checking or scope rules.

2. const: It declares a variable whose value cannot be modified after initialization.

Example:

const int MIN_BALANCE_PAISE = 5000;

It provides type checking and follows C++ scope rules.

3. constexpr: It declares a value or function that can be evaluated at compile time when the required conditions are satisfied.

Example:

constexpr int INNER_FARE_PAISE = 1000;
constexpr int MIDDLE_FARE_PAISE = 2000;
constexpr int OUTER_FARE_PAISE = 3000;
constexpr int PEAK_SURCHARGE_PERCENT = 20;
constexpr long long MIN_BALANCE_PAISE = 5000;

"constexpr" is preferred for fixed fare values because it supports type checking, scope rules and compile-time evaluation. It also makes fare revisions easier because values can be updated in one place.

2.3 Use of enum and enum class for Zones

An enumeration represents a set of named values.

Example using "enum":

enum Zone { Inner, Middle, Outer };

Traditional "enum" values can be implicitly converted to integers, and their enumerator names can enter the surrounding scope.

Example using "enum class":

enum class Zone { Inner, Middle, Outer };

With "enum class", values are accessed using names such as "Zone::Inner" and are not implicitly converted to integers.

Therefore, "enum class" is safer because it provides stronger type checking and reduces naming conflicts.

2.4 Naming Rules and Conventions for Identifiers

The following rules should be followed:

1. An identifier must begin with a letter or underscore, not a digit.
2. It may contain letters, digits and underscores.
3. Spaces and special symbols are not allowed.
4. C++ keywords cannot be used as identifiers.
5. Identifiers are case-sensitive.
6. Meaningful names should be used for readability.

Examples:

- Valid: "fare", "cardBalance", "MIN_BALANCE_PAISE"
- Invalid: "2fare", "card balance", "class"

A consistent naming convention improves readability and maintainability.

2.5 Alternative Concept and Complexity Analysis

If "#define" macros were used instead of "constexpr" constants and "enum class", the program would perform textual substitution rather than using normal typed C++ constants.

Macros do not provide ordinary type checking or C++ scope control. In contrast, "constexpr" values have types and follow C++ scope rules. "enum class" also prevents accidental mixing of zone values with unrelated integers.

Both approaches have O(1) time complexity for accessing a fixed fare value. A macro itself occupies no storage, and a "constexpr" value may require no separate runtime storage when optimized or used as a compile-time constant.

Therefore, using "constexpr" and "enum class" provides better type safety and maintainability without changing the overall time complexity of fare calculation.

Conclusion

The metro fare system should use meaningful identifiers, appropriate C++ tokens, "constexpr" for fixed fare values and "enum class" for zones. These choices improve type safety, readability and maintainability. Centralizing fare constants also makes future fare revisions easier.
