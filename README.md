#include <iostream>
}
}


return 0;
}


// ------------------------------------------------------------
// Function Definitions
// ------------------------------------------------------------


double checkBalance(double balance) {
return balance; // pass-by-value per assignment spec
}


bool deposit(double &balance, double amount, vector<string>& history) {
if (amount <= 0.0) return false;
balance += amount;
// History entry
ostringstream oss;
oss << nowString() << " | Deposit +$" << fixed << setprecision(2) << amount
<< " | Balance $" << balance;
history.push_back(oss.str());
return true;
}


bool withdraw(double &balance, double amount, vector<string>& history,
double &withdrawnToday, const double dailyLimit) {
if (amount <= 0.0) return false;
if (amount > balance) return false;
if (withdrawnToday + amount > dailyLimit) return false; // daily cap


balance -= amount;
withdrawnToday += amount;


// History entry
ostringstream oss;
oss << nowString() << " | Withdraw -$" << fixed << setprecision(2) << amount
<< " | Balance $" << balance;
history.push_back(oss.str());
return true;
}


string nowString() {
using clock = chrono::system_clock;
auto now = clock::now();
std::time_t t = clock::to_time_t(now);
char buf[64];
#if defined(_MSC_VER)
ctime_s(buf, sizeof(buf), &t);
#else
ctime_r(&t, buf);
#endif
// ctime appends a newline; strip it
string s(buf);
if (!s.empty() && s.back() == '\n') s.pop_back();
return s;
}


bool authenticate(const string& correctPin, int maxAttempts) {
for (int attempt = 1; attempt <= maxAttempts; ++attempt) {
string entered;
cout << "\nEnter PIN: ";
cin >> entered;
if (entered == correctPin) {
cout << "Authentication successful.\n\n";
return true;
}
cout << "Incorrect PIN (" << attempt << "/" << maxAttempts << ")." << '\n';
}
return false;
}


void printMenu() {
cout << "==============================\n";
cout << " ATM MAIN MENU\n";
cout << "==============================\n";
cout << "1. Check Balance\n";
cout << "2. Deposit Money\n";
cout << "3. Withdraw Money\n";
cout << "4. Exit\n";
cout << "==============================\n";
}
