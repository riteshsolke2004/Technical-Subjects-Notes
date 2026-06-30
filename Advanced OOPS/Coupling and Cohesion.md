# 📘 Advanced OOP for LLD

# Module 3 – Part 2: Coupling & Cohesion

## 📌 Table of Contents

* Introduction
* What is Coupling?
* Why Do We Need Loose Coupling?
* Types of Coupling
* Tight Coupling vs Loose Coupling
* Advantages & Disadvantages of Coupling
* What is Cohesion?
* Why Do We Need High Cohesion?
* Types of Cohesion
* High Cohesion vs Low Cohesion
* Coupling vs Cohesion
* Coupling & Cohesion in LLD
* Best Practices
* Common Mistakes
* Interview Questions
* Practice Problems
* Summary

---

# 📖 Introduction

Writing good software is not only about making it work.

It should also be:

* Easy to maintain
* Easy to extend
* Easy to test
* Easy to reuse

Two of the most important concepts that help achieve these goals are:

* **Coupling**
* **Cohesion**

These concepts are fundamental in **Low-Level Design (LLD)** and are closely related to the **SOLID Principles**.

---

# 🔗 What is Coupling?

## Definition

Coupling is the degree of dependency between two classes or modules.

It tells us **how much one class depends on another class**.

## Simple Definition

> Coupling measures how strongly two classes are connected.

---

# 🎯 Why Do We Need Loose Coupling?

Imagine two rooms connected by a wall.

If you change one room and the other also needs modification, they are tightly connected.

Similarly, if changing one class forces changes in another class, they are tightly coupled.

Loose coupling allows classes to change independently.

---

# ✨ Characteristics of Loose Coupling

* Independent modules
* Easy maintenance
* Better scalability
* Better testing
* High reusability
* Easy replacement of components

---

# ❌ Tight Coupling

In Tight Coupling:

* One class directly creates or depends on another concrete class.
* Changes in one class often require changes in the other.

Example:

```cpp
class Engine
{
public:
    void start() {}
};

class Car
{
private:
    Engine engine;

public:
    void drive()
    {
        engine.start();
    }
};
```

Problems:

* Difficult to replace `Engine`.
* Hard to unit test.
* Less flexible.

---

# ✅ Loose Coupling

In Loose Coupling:

Classes depend on **abstractions** instead of concrete implementations.

Example:

```cpp
class IEngine
{
public:
    virtual void start() = 0;
    virtual ~IEngine() = default;
};

class PetrolEngine : public IEngine
{
public:
    void start() override {}
};

class Car
{
private:
    IEngine& engine;

public:
    Car(IEngine& engine) : engine(engine) {}

    void drive()
    {
        engine.start();
    }
};
```

Now the engine can easily be replaced.

---

# 📚 Types of Coupling

From worst to best:

---

## 1. Content Coupling (Worst)

One module directly accesses another module's internal data.

Avoid this completely.

---

## 2. Common Coupling

Multiple modules share global variables.

Example:

```cpp
int count = 0;
```

Many classes modify the same variable.

---

## 3. External Coupling

Modules depend on external systems.

Examples:

* Database
* Operating System
* Hardware
* External APIs

---

## 4. Control Coupling

One module controls another using flags.

Example:

```cpp
process(true);
```

The boolean flag changes the behavior.

---

## 5. Stamp Coupling

Passing an entire object when only part of it is needed.

Example:

```cpp
void display(Student student);
```

Only `student.name` is used.

Better:

```cpp
void display(string name);
```

---

## 6. Data Coupling (Best Practical)

Only required data is passed.

Example:

```cpp
void printName(string name);
```

Highly recommended.

---

# 📊 Coupling Comparison

| Coupling Type | Quality  |
| ------------- | -------- |
| Content       | Worst    |
| Common        | Poor     |
| External      | Moderate |
| Control       | Moderate |
| Stamp         | Good     |
| Data          | Best     |

---

# 🎯 What is Cohesion?

## Definition

Cohesion measures **how closely related the responsibilities of a class are**.

A highly cohesive class performs **one well-defined responsibility**.

## Simple Definition

> Cohesion measures how focused a class is on a single task.

---

# 🎯 Why Do We Need High Cohesion?

Imagine a calculator.

It should perform mathematical operations.

If it also:

* Sends emails
* Plays music
* Stores files

Then it has multiple responsibilities.

This makes the design poor.

---

# ✨ Characteristics of High Cohesion

* One responsibility
* Easy maintenance
* Better readability
* Easy testing
* Better reuse
* Simpler debugging

---

# 📚 Types of Cohesion

From worst to best:

---

## 1. Coincidental Cohesion (Worst)

Unrelated tasks are grouped together.

---

## 2. Logical Cohesion

Tasks are grouped logically.

Example:

Input functions.

---

## 3. Temporal Cohesion

Tasks executed at the same time.

Example:

Application startup.

---

## 4. Procedural Cohesion

Tasks follow the same procedure.

---

## 5. Communicational Cohesion

Tasks work on the same data.

---

## 6. Sequential Cohesion

Output of one function becomes input of another.

---

## 7. Functional Cohesion (Best)

The class performs exactly one responsibility.

Example:

```cpp
class EmailService
{
public:
    void sendEmail() {}
};
```

Perfect cohesion.

---

# 📊 Cohesion Comparison

| Cohesion Type   | Quality   |
| --------------- | --------- |
| Coincidental    | Worst     |
| Logical         | Poor      |
| Temporal        | Average   |
| Procedural      | Good      |
| Communicational | Better    |
| Sequential      | Very Good |
| Functional      | Best      |

---

# ⚖️ Tight Coupling vs Loose Coupling

| Feature     | Tight Coupling | Loose Coupling |
| ----------- | -------------- | -------------- |
| Flexibility | Low            | High           |
| Testing     | Difficult      | Easy           |
| Reusability | Low            | High           |
| Maintenance | Difficult      | Easy           |
| Scalability | Poor           | Excellent      |

---

# ⚖️ High Cohesion vs Low Cohesion

| Feature        | High Cohesion | Low Cohesion |
| -------------- | ------------- | ------------ |
| Responsibility | Single        | Multiple     |
| Readability    | High          | Low          |
| Maintenance    | Easy          | Difficult    |
| Reusability    | High          | Low          |
| Testing        | Easy          | Difficult    |

---

# 🔄 Coupling vs Cohesion

| Feature     | Coupling                   | Cohesion                   |
| ----------- | -------------------------- | -------------------------- |
| Measures    | Dependency between classes | Relatedness within a class |
| Goal        | Minimize                   | Maximize                   |
| Good Design | Loose Coupling             | High Cohesion              |

---

# 🏗 Coupling & Cohesion in LLD

## Example 1

### Bad Design

```text
UserService

- Login
- Register
- Payment
- Email
- SMS
- PDF
- Reports
```

Low Cohesion.

---

### Better Design

```text
UserService

↓

AuthenticationService

↓

EmailService

↓

PaymentService

↓

NotificationService
```

High Cohesion.

---

## Example 2

Instead of:

```cpp
class Order
{
    PayPal payment;
};
```

Use:

```cpp
class Order
{
    IPaymentService& payment;
};
```

This reduces coupling.

---

# ✅ Advantages of Loose Coupling & High Cohesion

* Better architecture
* Easy maintenance
* Easy extension
* Better scalability
* Better testing
* Better code reuse
* Easier debugging

---

# ❌ Disadvantages of Tight Coupling & Low Cohesion

* Difficult to maintain
* Difficult to test
* Hard to replace modules
* Reduced flexibility
* Increased bugs
* Poor scalability

---

# ⭐ Best Practices

* One class should have one responsibility.
* Prefer interfaces over concrete classes.
* Use Dependency Injection.
* Follow SOLID Principles.
* Keep methods small and focused.
* Avoid unnecessary dependencies.
* Design independent modules.

---

# 🚫 Common Mistakes

### ❌ God Class

One class doing everything.

---

### ❌ Too Many Dependencies

A class depending on many other classes.

---

### ❌ Global Variables

They create unnecessary coupling.

---

### ❌ Mixing Responsibilities

Authentication, payment, logging, and reporting should not be in the same class.

---

# 🎤 Interview Questions

1. What is Coupling?
2. What is Cohesion?
3. Difference between Coupling and Cohesion?
4. Explain Tight Coupling with an example.
5. Explain Loose Coupling with an example.
6. Explain High Cohesion.
7. Which is better: High Cohesion or Low Cohesion?
8. Which is better: Tight Coupling or Loose Coupling?
9. How does Dependency Injection reduce coupling?
10. How are SOLID Principles related to Coupling and Cohesion?

---

# 📝 Practice Problems

## Beginner

Design:

* Calculator
* Email Service

Ensure each class has one responsibility.

---

## Intermediate

Design:

* User Service
* Authentication Service
* Notification Service

Keep coupling low.

---

## Advanced

Design an E-commerce System with:

* Order Service
* Payment Service
* Inventory Service
* Email Service
* Shipping Service

Requirements:

* High Cohesion
* Loose Coupling
* Easy to extend
* Easy to test

---

# 🧠 Key Takeaways

* Coupling measures dependency **between classes**.
* Cohesion measures relatedness **within a class**.
* Good software aims for **Loose Coupling**.
* Good software aims for **High Cohesion**.
* Loose Coupling improves flexibility and maintainability.
* High Cohesion keeps classes focused and easier to understand.
* These concepts are the foundation of SOLID Principles and modern software architecture.

---

# 📚 Revision Cheat Sheet

| Topic          | Best Practice                  |
| -------------- | ------------------------------ |
| Coupling       | Keep it Loose                  |
| Cohesion       | Keep it High                   |
| Loose Coupling | Classes depend on abstractions |
| High Cohesion  | One class, one responsibility  |
| Tight Coupling | Avoid                          |
| Low Cohesion   | Avoid                          |
| LLD Goal       | Loose Coupling + High Cohesion |

---

# 🚀 Next Module

**Module 4: SOLID Principles**

Topics to be Covered:

* Single Responsibility Principle (SRP)
* Open/Closed Principle (OCP)
* Liskov Substitution Principle (LSP)
* Interface Segregation Principle (ISP)
* Dependency Inversion Principle (DIP)

These five principles build directly on the concepts of **Coupling**, **Cohesion**, **Object Relationships**, and **Dependency**, making them the next logical step in mastering Low-Level Design.
