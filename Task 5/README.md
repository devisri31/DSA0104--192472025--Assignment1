TASK 5 – WRITE CORRECT EXPRESSIONS WITH THE RIGHT PRECEDENCE

5.1 Expressions for Peak Hours, Surcharge and Concession

1. Peak-hour check

The peak hours are 8:00–10:00 AM and 5:00–8:00 PM.

bool peak = (hour >= 8 && hour < 10) ||
            (hour >= 17 && hour < 20);

The conditions use "&&" to check each time interval and "||" to combine the two intervals. The end times are excluded, so 10 AM and 8 PM are not peak hours.

2. Peak surcharge

A 20% surcharge is added to the base fare during peak hours.

long long finalFare = peak
    ? baseFare + baseFare * 20 / 100
    : baseFare;

The conditional operator "?:" selects the fare calculation based on whether "peak" is true or false. Integer arithmetic is used when the fare is stored in paise.

3. Concession

The assignment states that students and senior citizens receive a concession but does not specify the percentage. Assuming a concession percentage has been defined:

long long discountedFare =
    baseFare - baseFare * concessionPercent / 100;

The value of "concessionPercent" must be set according to the concession rule approved for the system.

5.2 Operator Precedence and Associativity

Operator precedence determines which operation is performed first. Associativity determines the order of evaluation when operators have the same precedence.

- Multiplication "*", division "/" and remainder "%" have higher precedence than addition "+" and subtraction "-".
- Relational operators such as "<" and ">=" are evaluated before logical "&&".
- Logical "&&" has higher precedence than logical "||".
- The conditional operator "?:" has lower precedence than arithmetic and logical operators.
- Compound assignment operators such as "+=" update a variable using the result of an operation.

Parentheses improve readability and make the intended order clear.

5.3 Difference Between x++ and ++x

The postfix increment operator "x++" returns the original value and then increments the variable.

The prefix increment operator "++x" increments the variable first and returns the new value.

Example:

int x = 5;
int a = x++;
int b = ++x;

After these statements, "a = 5", "b = 7" and "x = 7".

The expression "i = i++" should be avoided because it is confusing and does not express a clear intended update. In modern C++, this particular expression is not undefined behaviour, but it assigns the old value back to "i", so it does not reliably achieve the expected increment.

5.4 Division and Remainder with Negative Operands

In C++, integer division truncates the result toward zero, and the remainder has the sign of the dividend.

Examples:

- "10 / 3" gives "3".
- "10 % 3" gives "1".
- "-10 / 3" gives "-3".
- "-10 % 3" gives "-1".

These rules are important when performing integer calculations and checking monetary values.

5.5 Predicted Output of the Given Program

The predicted output is written before execution, as required by the assignment.

Predicted output:

11 16
7 6 4
6 4
3 1 -3 -1
18

5.6 Explanation of Each Output Line

Line 1:

11 16

The expression "x + y * 2" evaluates multiplication first: "5 + (3 × 2) = 11".

The expression "(x + y) * 2" evaluates the addition first because of parentheses: "(5 + 3) × 2 = 16".

Line 2:

7 6 4

The expression "x++ + ++y" uses postfix and prefix increment.

- "x++" contributes the original value "5", then "x" becomes "6".
- "++y" increments "y" from "3" to "4" and contributes "4".
- Therefore, "z = 5 + 4 = 9".

Correction to the predicted output: The correct second line is:

9 6 4

Line 3:

6 4

The conditional expression "(x > y ? x : y)" returns "x", which is "6", because "6 > 4".

The expression "x % 4 * 2" evaluates "%" and "*" from left to right: "(6 % 4) × 2 = 4".

Line 4:

3 1 -3 -1

Integer division truncates toward zero, while the remainder follows the sign of the dividend.

Line 5:

18

The loop uses "i = 0, 3, 6, 9". Their sum is "0 + 3 + 6 + 9 = 18".

5.7 Alternative Concept and Complexity Analysis

An alternative is to use a lookup table "bool peak[24]" instead of a combined logical expression.

Example:

bool peak[24] = {};

for (int h = 8; h < 10; h++)
    peak[h] = true;

for (int h = 17; h < 20; h++)
    peak[h] = true;

The peak status can then be checked using:

bool isPeak = peak[hour];

Both the logical expression and the lookup-table approach have O(1) time complexity per check. The lookup table requires approximately 24 Boolean elements of storage, while the logical expression requires no additional table.

The lookup-table approach can simplify repeated checks and makes changes to peak hours easier, while the logical expression uses less additional memory.

Conclusion

Correct operator precedence, associativity and increment behaviour are essential for accurate fare calculations. Parentheses improve readability, and a lookup table provides an alternative way to check peak hours. Both approaches have constant-time complexity, but the best choice depends on readability, maintainability and memory requirements.
