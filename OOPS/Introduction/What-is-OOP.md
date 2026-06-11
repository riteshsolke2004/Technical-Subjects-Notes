# What is Object-Oriented Programming (OOP)?

## Definition

Object-Oriented Programming (OOP) is a programming paradigm that organizes programs into objects. These objects contain:

- Data (Variables)
- Methods (Functions)

OOP models real-world entities and their behavior.

---

## Simple Meaning

In OOP, everything is treated as an object.

Examples:

- Student
- Car
- Mobile Phone
- Bank Account
- Employee

---

## Components of an Object

An object contains:

### 1. State (Properties)

Examples:

- Name
- Age
- Color
- Salary

### 2. Behavior (Functions)

Examples:

- Walk()
- Eat()
- Deposit()
- Withdraw()

---

## Example

Car:

Properties:

- Brand
- Color
- Speed

Behaviors:

- Start()
- Stop()
- Accelerate()

---

## Basic C++ Example

```cpp
#include<iostream>
using namespace std;

class Car {
public:
    string brand;

    void start() {
        cout << "Car Started";
    }
};

int main() {

    Car c1;

    c1.brand = "BMW";

    c1.start();

    return 0;
}
```

---

## Output

```

Car Started

```

---

## Advantages of OOP

- Code Reusability
- Security
- Modularity
- Easy Maintenance
- Better Scalability

---

## Real World Examples

1. ATM Machine
2. Banking System
3. Hospital Management System
4. Student Management System
5. E-Commerce Websites

---

## Interview Questions

### Q1. What is OOP?

Object-Oriented Programming is a programming paradigm based on objects containing data and methods.

### Q2. What are the four pillars of OOP?

1. Encapsulation
2. Abstraction
3. Inheritance
4. Polymorphism

### Q3. Name some OOP languages.

- C++
- Java
- Python
- C#
- Kotlin

---

## Summary

OOP represents real-world entities using objects and provides better code organization, security, and reusability.

