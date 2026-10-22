TASK 4 – CONTROL IMPLICIT CONVERSIONS

4.1 Integer Division and Integer-to-Double Conversion

Implicit conversion occurs when C++ automatically converts a value from one data type to another.

Example:

int a = 7, b = 2;
double c = a / b;

Here, "a / b" performs integer division because both operands are integers. The result is "3", which is then converted to "3.0" when assigned to "double".

To obtain the correct decimal result, an explicit conversion can be used:

double d = static_cast<double>(a) / b;

The result is "3.5" because one operand is converted to "double" before division.

4.2 Comparison of Signed and Unsigned Values

Consider the following code:

unsigned int u = 1;
int s = -1;

cout << (s < u ? "s < u" : "s >= u");

When a negative signed integer is compared with an unsigned integer of the same rank, the signed value is converted to unsigned under the usual arithmetic conversions on typical systems where "int" and "unsigned int" have the same rank.

Therefore, "-1" converts to a large unsigned value, and the comparison is false. The output is:

s >= u

Compiler warnings can help identify potentially unsafe signed and unsigned comparisons. Using appropriate types and explicit checks prevents unexpected behaviour.

4.3 Narrowing Conversions and Brace Initialisation

A narrowing conversion may lose information when a value is converted to a type with a smaller range or precision.

Example:

int x = 3.7;

The fractional part is discarded, so "x" becomes "3".

Brace initialisation helps prevent unintended narrowing:

int x{3.7};  // Compilation error

The compiler rejects this initialisation because converting "3.7" to "int" would lose information.

4.4 Use of static_cast

"static_cast" explicitly converts a value to another compatible type.

Example:

int a = 7, b = 2;
double result = static_cast<double>(a) / b;

Output:

3.5

It makes the conversion clear and helps avoid errors caused by unintended integer arithmetic.

4.5 Predicted Output of the Given Program

The prediction below is written before execution, as required by the assignment.

Predicted output:

3 3.5
C 68
1 true
s >= u

4.6 Explanation of Each Output Line

Line 1:

3 3.5

"a / b" performs integer division, producing "3". The result is converted to "double", giving "3". In the second expression, "static_cast<double>(a) / b" performs floating-point division, producing "3.5".

Line 2:

C 68

The expression "'A' + 2" produces the character "C" on an ASCII-compatible system. When "ch + 1" is evaluated, "ch" is promoted to "int", producing "68" on that system.

Line 3:

1 true

The integer value "5" is converted to "bool", producing "true". By default, a Boolean value is printed as "1". After applying "std::boolalpha", the same value is printed as "true".

Line 4:

s >= u

The signed value "-1" is converted to an unsigned value during comparison with "u". On a typical system, the converted value is greater than "1", so the condition "s < u" is false.

4.7 Alternative Concept and Complexity Analysis

If every conversion were written explicitly using "static_cast" and brace initialisation were used where appropriate, the code would make type conversions easier to identify.

For example:

double result = static_cast<double>(a) / b;
int value{3}; 

Explicit conversions improve readability, while brace initialisation rejects certain narrowing conversions at compile time.

Both implicit and explicit conversions generally have O(1) time complexity per operation. They also use the same basic storage for the resulting data types. The main advantage of explicit conversion is improved clarity and the prevention of certain programming mistakes, rather than reduced execution time or memory usage.

Conclusion

Implicit conversions can cause unexpected results through integer division, character promotion, integer-to-Boolean conversion and signed-to-unsigned comparison. Using "static_cast", brace initialisation and suitable data types makes the program safer and easier to understand.
