TASK 1 – UNDERSTAND THE PROBLEM AND IDENTIFY THE OBJECTS

1.1 Objects in the Metro Smart-Card System

The City Metro Smart-Card System can be designed using object-oriented programming (OOP). The main objects are:

1. SmartCard: Stores the card number and available balance. Its behaviours include checking the balance, checking travel eligibility and deducting the fare.

2. Passenger: Stores passenger details and passenger category, such as regular passenger, student or senior citizen. The passenger category can be used to determine concession eligibility.

3. Journey: Stores the source zone, destination zone, travel time and calculated fare. It determines whether the journey occurs during peak hours.

4. Zone: Represents the Inner, Middle and Outer zones. Each zone has a corresponding base fare of ₹10, ₹20 and ₹30, respectively.

5. FareTable: Stores the base fares, peak-hour surcharge and applicable concession rules. It calculates the final fare according to the journey details.

These objects help organize the program and make the system easier to maintain and modify.

1.2 Procedural Programming vs Object-Oriented Programming

In procedural programming, the system uses separate variables and functions to calculate fares, check balances and process journeys. Data and functions are maintained separately.

In object-oriented programming, related data and functions are grouped into classes such as "SmartCard", "Journey" and "FareTable". This improves organization, data protection and code reusability.

For example, a "SmartCard" class can keep the balance private and allow changes only through suitable member functions. This prevents other parts of the program from directly modifying the balance incorrectly.

1.3 Basic Principles of OOP

1. Encapsulation: Encapsulation combines data and functions within a class. The smart-card balance can be declared private and accessed through functions such as "getBalance()" and "deduct()".

2. Abstraction: Abstraction hides internal implementation details. The user can call a fare-calculation function without knowing all the calculations used internally.

3. Inheritance: Inheritance allows a new class to reuse the properties and functions of an existing class. For example, "StudentPassenger" and "SeniorPassenger" could inherit common passenger details from a "Passenger" class.

4. Polymorphism: Polymorphism allows the same function interface to produce different behaviour. For example, a virtual "calculateConcession()" function could be implemented differently for students and senior citizens.

These principles improve code organization, security, flexibility and maintainability.

1.4 Rules for a Correct Journey

The following rules must be satisfied:

1. The base fare must correspond to the farthest zone travelled.
2. A 20% surcharge must be applied during peak hours: 8:00–10:00 AM and 5:00–8:00 PM.
3. The system must calculate money accurately using integer paise.
4. A journey is permitted only if the remaining balance after deducting the fare is at least ₹50.
5. The card balance must never become negative.
6. Invalid zone values and invalid inputs must be rejected.
7. Student and senior citizen concessions must be applied according to the defined concession rules.

These rules ensure accurate fare calculation and prevent invalid journeys.

1.5 Alternative Concept and Complexity Analysis

If the system were implemented using procedural programming, global variables could store balances and fare values, while separate functions could calculate fares and check travel eligibility.

Both procedural and object-oriented implementations can process one journey in O(1) time because they perform a fixed number of calculations and comparisons.

The memory required for each card balance is also O(1) in both implementations.

However, when a fare rule changes, the procedural version may require changes in multiple functions. In the object-oriented version, the change can usually be made within the relevant class, such as "FareTable". Therefore, the object-oriented approach is easier to maintain and extend.

Conclusion

The object-oriented approach is suitable for the metro smart-card system because it organizes passengers, cards, journeys and fare rules into separate classes. Encapsulation protects the card balance, while abstraction, inheritance and polymorphism support a flexible design. Both approaches have similar basic time and space complexity, but OOP offers better maintainability as the system grows.
