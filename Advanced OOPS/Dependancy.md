# 📘 Advanced OOP for LLD

# Lesson 4: Dependency

## 📌 Table of Contents

* Introduction
* What is Dependency?
* Why Do We Need Dependency?
* Characteristics
* Real-World Examples
* Types of Dependency
* UML Representation
* Dependency vs Association
* Dependency vs Aggregation
* Dependency vs Composition
* C++ Implementation
* Dependency in Low-Level Design (LLD)
* Advantages
* Disadvantages
* Best Practices
* Common Mistakes
* Interview Questions
* Practice Problems
* Summary

---

# 📖 Introduction

In Object-Oriented Programming (OOP), objects interact with each other in different ways.

Sometimes an object **owns** another object.

Sometimes it simply **knows** another object.

Sometimes it **temporarily uses** another object to complete a task.

This temporary relationship is called **Dependency**.

Dependency is one of the most important concepts in **Low-Level Design (LLD)** because it forms the foundation for **Dependency Injection**, **SOLID Principles**, and **loosely coupled software**.

---

# ✅ What is Dependency?

## Definition

Dependency is a relationship in which one class **temporarily uses another class** to perform a specific task.

The dependent class does **not own** the other object.

It simply uses it whenever required.

## Simple Definition

> Dependency means **one object temporarily depends on another object to perform a task.**

---

# 🎯 Why Do We Need Dependency?

Imagine a customer placing an order.

The customer needs a payment service.

The customer **uses** the payment service only while making a payment.

The payment service is not stored permanently inside the customer object.

This is Dependency.

---

# ✨ Characteristics

* Temporary relationship
* Weakest object relationship
* No ownership
* No object lifetime dependency
* Usually exists inside methods or constructors
* Promotes loose coupling
* Easy to replace dependent objects

---

# 🌍 Real-World Examples

| Class            | Depends On           |
| ---------------- | -------------------- |
| Customer         | Payment Service      |
| Student          | Printer              |
| Employee         | Email Service        |
| User             | Notification Service |
| Order            | Payment Gateway      |
| Application      | Logger               |
| Report Generator | PDF Generator        |

---

# 📚 Types of Dependency

## 1. Method Dependency

An object is passed as a parameter to a method.

```cpp
class Printer
{
public:
    void print()
    {
        cout << "Printing...\n";
    }
};

class Student
{
public:
    void submitAssignment(Printer& printer)
    {
        printer.print();
    }
};
```

The Student only uses the Printer temporarily.

---

## 2. Constructor Dependency

A dependency is provided through the constructor.

```cpp
class Logger
{
public:
    void log()
    {
        cout << "Logging...\n";
    }
};

class Application
{
private:
    Logger& logger;

public:
    Application(Logger& logger)
        : logger(logger)
    {
    }

    void run()
    {
        logger.log();
    }
};
```

---

## 3. Local Object Dependency

The dependent object is created inside a function.

```cpp
class EmailService
{
public:
    void sendEmail()
    {
        cout << "Email Sent\n";
    }
};

class User
{
public:
    void registerUser()
    {
        EmailService service;

        service.sendEmail();
    }
};
```

Although valid, this creates **tight coupling** because the User decides which EmailService to create.

---

# 📊 UML Representation

Dependency is represented using a **dashed arrow**.

```text
+---------+      - - - - - - - - - >
| Student |----------------------->| Printer |
+---------+                        +---------+
```

Dashed line = Dependency

Arrow points towards the class being used.

---

# 🧠 Memory Representation

```text
Stack Memory

+----------------+
| Student        |
+----------------+

+----------------+
| Printer        |
+----------------+

Student temporarily calls Printer.
```

Neither object owns the other.

---

# 💻 C++ Example

```cpp
#include <iostream>

using namespace std;

class Printer
{
public:
    void print()
    {
        cout << "Printing Assignment..." << endl;
    }
};

class Student
{
public:
    void submitAssignment(Printer& printer)
    {
        printer.print();
    }
};

int main()
{
    Printer printer;

    Student student;

    student.submitAssignment(printer);

    return 0;
}
```

### Output

```text
Printing Assignment...
```

Notice:

* Student does not store Printer.
* Student does not create Printer.
* Student simply uses Printer.

---

# 🏗 Dependency in LLD

Dependency appears almost everywhere.

## E-commerce

```text
Order
    |
    |-----> Payment Service
```

The Order uses the Payment Service to process payment.

---

## Banking

```text
Account
    |
    |-----> SMS Service
```

The Account uses an SMS Service to send notifications.

---

## Hospital

```text
Doctor
    |
    |-----> Printer
```

Doctor prints prescriptions.

---

## Food Delivery

```text
Order
    |
    |-----> Notification Service
```

The Order temporarily uses a notification service.

---

# ⚖️ Comparison

## Dependency vs Association

| Feature      | Dependency        | Association       |
| ------------ | ----------------- | ----------------- |
| Relationship | Uses              | Knows / Uses      |
| Duration     | Temporary         | Long-term         |
| Ownership    | None              | None              |
| UML          | Dashed Arrow      | Straight Line     |
| Example      | Student → Printer | Student ↔ Teacher |

---

## Dependency vs Aggregation

| Feature       | Dependency   | Aggregation    |
| ------------- | ------------ | -------------- |
| Ownership     | None         | Weak           |
| Lifetime      | Temporary    | Independent    |
| Stores Object | Usually No   | Yes            |
| UML           | Dashed Arrow | Hollow Diamond |

---

## Dependency vs Composition

| Feature               | Dependency   | Composition    |
| --------------------- | ------------ | -------------- |
| Ownership             | None         | Strong         |
| Lifetime              | Temporary    | Dependent      |
| Parent Controls Child | No           | Yes            |
| UML                   | Dashed Arrow | Filled Diamond |

---

# 🔥 Dependency Injection (Introduction)

Instead of creating dependent objects inside a class,

```cpp
EmailService service;
```

provide them from outside.

```cpp
User user(emailService);
```

This is called **Dependency Injection (DI)**.

Benefits:

* Loose coupling
* Better testing
* Easy replacement
* Better scalability

We will study Dependency Injection in detail later.

---

# ✅ Advantages

* Loose coupling
* Better flexibility
* Easy testing
* Easy mocking
* Better code reuse
* Improved maintainability
* Supports SOLID Principles

---

# ❌ Disadvantages

* Too many dependencies may increase complexity.
* Poor dependency management can make debugging harder.
* Incorrect design can create unnecessary coupling.

---

# ⭐ Best Practices

* Depend on abstractions rather than concrete classes.
* Pass dependencies through constructors whenever possible.
* Avoid creating dependencies inside business logic.
* Keep dependencies minimal.
* Prefer Dependency Injection for large applications.

---

# 🚫 Common Mistakes

### ❌ Creating objects inside business methods

```cpp
PaymentService payment;
```

This tightly couples your code.

---

### ❌ Depending on concrete implementations

Instead of:

```cpp
PayPalService payment;
```

Prefer:

```cpp
PaymentService& payment;
```

where `PaymentService` is an abstract interface.

---

### ❌ Confusing Dependency with Association

Dependency is **temporary**.

Association is generally a **long-term relationship**.

---

# 🎤 Interview Questions

1. What is Dependency?
2. Difference between Dependency and Association?
3. Difference between Dependency and Aggregation?
4. Difference between Dependency and Composition?
5. Explain Dependency using a real-world example.
6. Draw UML notation for Dependency.
7. What is Constructor Dependency?
8. What is Method Dependency?
9. What is Dependency Injection?
10. Why is Dependency important in LLD?

---

# 📝 Practice Problems

## Beginner

Design:

* Student
* Printer

Use Dependency.

---

## Intermediate

Design:

* User
* Email Service

Use Constructor Dependency.

---

## Intermediate

Design:

* Order
* Payment Service

Use Method Dependency.

---

## Advanced

Design a Food Delivery Application.

Classes:

* Customer
* Order
* Payment Service
* Notification Service

Requirements:

* Customer places an order.
* Order uses Payment Service.
* Order uses Notification Service.
* No object should own either service.

Use Dependency.

---

# 🧠 Key Takeaways

* Dependency is the weakest object relationship.
* One class temporarily uses another class.
* There is no ownership.
* Objects remain completely independent.
* UML uses a **dashed arrow**.
* Dependency forms the foundation of **Dependency Injection**.
* Dependency helps create loosely coupled and maintainable software.

---

# 📚 Revision Cheat Sheet

| Topic                | Key Point                                                  |
| -------------------- | ---------------------------------------------------------- |
| Relationship         | Uses                                                       |
| Ownership            | None                                                       |
| Lifetime             | Temporary                                                  |
| UML Symbol           | Dashed Arrow                                               |
| Object Sharing       | Yes                                                        |
| Parent Deletes Child | No                                                         |
| Common Examples      | Student–Printer, Order–Payment Service, User–Email Service |

---

# 🚀 Next Lesson

**Lesson 5: Object Ownership & Object Lifetime**

Topics to be Covered:

* What is Object Ownership?
* Types of Ownership
* Exclusive Ownership
* Shared Ownership
* Borrowed References
* Object Lifetime
* Stack vs Heap Objects
* RAII in Depth
* Smart Pointers (`std::unique_ptr`, `std::shared_ptr`, `std::weak_ptr`)
* Memory Management in LLD
* Interview Questions
* Best Practices
