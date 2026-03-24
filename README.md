# Assignment 02: Encapsulation and Inheritance (Banking System)

## 🎯 Objectives
* **Encapsulation**: Practice protecting internal data states using access modifiers.
* **Inheritance**: Create multiple specialized classes that share a common foundation.
* **Method Overriding**: Learn how to modify parent behavior in a subclass to meet specific requirements.

## 🏢 Scenario
You are developing a backend module for a digital banking application. While all accounts have a balance and an owner, different account types have different rules for how money is handled. You will implement a base account and two specific variations:
1.  **Savings Account**: Designed for long-term growth through interest.
2.  **Checking Account**: Designed for daily use with a small transaction fee on withdrawals.

---

## 🛠️ Step-by-Step Implementation Guide

### Step 1: The Foundation (`BankAccount.java`)
This class handles logic common to **all** accounts.
* **Fields**:
    * `private String accountHolder`
    * `protected double balance` (Note: `protected` allows child classes to see it).
* **Constructor**: 
    * Initialize both fields. 
    * **Rule**: If the provided `initialBalance` is negative, set the balance to `0.0`.
* **Methods**: 
    * `public void deposit(double amount)`: Increase balance if the amount is positive.
    * `public void withdraw(double amount)`: Decrease balance if the amount is positive and funds are sufficient (no overdrafts).
    * `public double getBalance()`: Returns the current balance.

### Step 2: The Interest Logic (`SavingsAccount.java`)
A specialized account that grows over time.
* **Inheritance**: Use the `extends` keyword to inherit from `BankAccount`.
* **Additional Field**: `private double interestRate` (e.g., `0.05` for 5%).
* **Constructor**: 
    * You **must** call `super(accountHolder, initialBalance)` as the first line.
* **New Method**: 
    * `public void applyInterest()`: Calculates interest ($Balance \times interestRate$) and adds that amount to the current balance.
    * **Pro-Tip**: Reuse `this.deposit()` or `super.deposit()` to add the interest amount.

### Step 3: The Overriding Logic (`CheckingAccount.java`)
A daily-use account that charges a fee for every withdrawal.
* **Inheritance**: Extends `BankAccount`.
* **Additional Field**: `private static final double TRANSACTION_FEE = 1.50;`
* **Method Overriding**: Override `public void withdraw(double amount)`.
    * **Logic**: The total deduction from the balance should be `amount + TRANSACTION_FEE`.
    * **Rule**: Only perform the withdrawal if the balance can cover **both** the amount and the fee.
    * **Pro-Tip**: Use `super.withdraw(...)` to reuse the logic already written in the parent class.

---

## ✅ Pre-Submission Checklist
*Before you `git push`, make sure you can answer **YES** to all the following:*

- [ ] **Encapsulation**: Is my `balance` field `protected`? (It should NOT be `public`).
- [ ] **Inheritance**: Do both `SavingsAccount` and `CheckingAccount` use the `extends` keyword?
- [ ] **Super Constructor**: Does my subclass constructor call `super(...)`?
- [ ] **Checking Logic**: Does my `CheckingAccount` charge the $1.50 fee *only* on withdrawals?
- [ ] **Overdraft Protection**: Does my code prevent the balance from ever dropping below zero?
- [ ] **Naming**: Do my method names match the instructions exactly? (Java is case-sensitive!)
- [ ] **Local Tests**: Did I run `mvn test` and see "BUILD SUCCESS"?

---

## 🚀 How to Submit
1.  **Local Testing**: Run the provided JUnit tests in your IDE or via terminal using `mvn test`.
2.  **Pushing to GitHub**:
    ```bash
    git add .
    git commit -m "Completed BankAccount assignment"
    git push origin main
    ```
3.  **View Results**: Check the **Actions** tab on your GitHub repository to see your automated grade.

---

## 📋 Evaluation Criteria
| Feature | Weight |
| :--- | :--- |
| **Encapsulation** (Correct access modifiers) | 20% |
| **Savings Logic** (Interest calculation) | 25% |
| **Checking Logic** (Fee implementation & Overriding) | 35% |
| **Code Quality** (Use of `super`, no negative balances) | 20% |

## 🔍 Troubleshooting Your Grade
If your score is **0/100**, check the following:

1. **❌ Build Failed**: Your code has a syntax error (missing semicolon, bracket, etc.). Check the "Build and Test" logs in the Actions tab.
2. **❌ Encapsulation**: You likely made the `balance` field `public`. It must be `protected`.
3. **❌ Checking/Savings Logic**: Ensure your math matches the formulas in the Step-by-Step guide.
4. **❌ No Tests Found**: Do not rename the test classes or delete the `src/test` folder. The grader needs those files to verify your work.
