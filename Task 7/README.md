TASK 7 – FROM PROCEDURAL TO OBJECT-ORIENTED

7.1 Procedural Programming Approach

In procedural programming, the card balance is stored in a variable, and separate functions are used to check travel eligibility and deduct the fare.

#include <iostream>
using namespace std;

const long long MIN_BALANCE = 5000;

bool canTravel(long long balance, long long fare) {
    return fare > 0 && balance - fare >= MIN_BALANCE;
}

void deduct(long long& balance, long long fare) {
    if (canTravel(balance, fare)) {
        balance -= fare;
    }
}

int main() {
    long long balance = 10000;
    long long fare = 3000;

    if (canTravel(balance, fare)) {
        deduct(balance, fare);
        cout << "Journey approved\n";
    } else {
        cout << "Journey denied\n";
    }

    cout << "Remaining balance: " << balance << " paise\n";
    return 0;
}

In this approach, data and functions are separate. The balance is passed to functions, and the program uses a reference to update it.

7.2 Object-Oriented Programming Approach

In object-oriented programming, the card balance and its related functions are grouped into a "SmartCard" class. The balance is declared private and can be changed only through controlled member functions.

#include <iostream>
using namespace std;

class SmartCard {
private:
    long long balance;
    static constexpr long long MIN_BALANCE = 5000;

public:
    SmartCard(long long initialBalance) {
        balance = initialBalance;
    }

    bool canTravel(long long fare) const {
        return fare > 0 &&
               balance - fare >= MIN_BALANCE;
    }

    bool deduct(long long fare) {
        if (canTravel(fare)) {
            balance -= fare;
            return true;
        }
        return false;
    }

    long long getBalance() const {
        return balance;
    }
};

int main() {
    SmartCard card(10000);
    long long fare = 3000;

    if (card.deduct(fare)) {
        cout << "Journey approved\n";
    } else {
        cout << "Journey denied\n";
    }

    cout << "Remaining balance: "
         << card.getBalance() << " paise\n";

    return 0;
}

7.3 How the SmartCard Class Prevents a Negative Balance

The "balance" data member is private, so it cannot be modified directly from outside the class. The "deduct()" function first calls "canTravel()" to check whether the fare can be paid while maintaining the minimum balance of 5000 paise.

The fare is deducted only when the condition is satisfied. Otherwise, the balance remains unchanged. This protects the card balance from invalid deductions through the class interface.

7.4 Which Approach Is Easier to Modify?

If the minimum balance changes from ₹50 to another amount, the procedural program requires the corresponding constant or rule to be updated. In the object-oriented program, the "MIN_BALANCE" constant inside the "SmartCard" class can be updated in one place.

The object-oriented approach is easier to maintain because the balance rules are grouped within the class.

7.5 Alternative Concept and Complexity Analysis

If the balance were declared public instead of private, any part of the program could directly change it.

For example:

card.balance = -1000;

This would bypass the travel eligibility check if the balance were publicly accessible. It could violate the rule that the balance must never fall below the required minimum.

Both procedural and object-oriented approaches have O(1) time complexity for checking eligibility and deducting one fare. The memory required to store one balance is O(1) in both approaches.

Making the balance private does not change the basic time or space complexity. It improves data protection and ensures that changes to the balance go through the class's validation rules.

Conclusion

Both procedural and object-oriented programming can implement the metro fare system. However, the "SmartCard" class provides better encapsulation by protecting the balance and controlling deductions. Therefore, the object-oriented approach is more suitable for maintaining and extending the metro smart-card system.
