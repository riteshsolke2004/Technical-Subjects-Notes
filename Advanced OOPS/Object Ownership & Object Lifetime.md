# 📘 Advanced OOP for LLD

# Lesson 5: Object Ownership & Object Lifetime

## 📌 Table of Contents

* Introduction
* What is Object Ownership?
* Why Do We Need Object Ownership?
* Types of Object Ownership
* Object Lifetime
* Stack vs Heap Objects
* Ownership Models
* Smart Pointers
* RAII (Resource Acquisition Is Initialization)
* Memory Management in LLD
* Best Practices
* Common Mistakes
* Interview Questions
* Practice Problems
* Summary

---

# 📖 Introduction

In Object-Oriented Programming (OOP), objects are constantly created, shared, and destroyed.

One of the biggest responsibilities of a software engineer is deciding:

* Who creates an object?
* Who owns the object?
* Who destroys the object?
* How long should the object remain alive?

These questions are answered by **Object Ownership** and **Object Lifetime**.

Incorrect ownership leads to:

* Memory leaks
* Dangling pointers
* Double deletion
* Crashes
* Undefined behavior

Understanding these concepts is fundamental for writing safe and maintainable C++ code and designing robust Low-Level Design (LLD) systems.

---

# ✅ What is Object Ownership?

## Definition

Object Ownership defines **which object or component is responsible for managing another object's lifetime**.

The owner is responsible for:

* Creating the object
* Managing the object
* Destroying the object

## Simple Definition

> Object Ownership determines **who is responsible for an object's lifecycle**.

---

# 🎯 Why Do We Need Object Ownership?

Imagine a company.

The company buys laptops for employees.

Who owns the laptops?

The company.

Employees only use them.

Similarly, in software:

If a class creates an object, it usually owns that object and is responsible for destroying it.

Without clear ownership, programs may leak memory or access invalid objects.

---

# ✨ Types of Object Ownership

## 1. Exclusive Ownership

Only one object owns another object.

When the owner is destroyed, the owned object is also destroyed.

Example:

```text
House
  ◆
  |
Room
```

Equivalent C++ concept:

```cpp
std::unique_ptr<Room>
```

---

## 2. Shared Ownership

Multiple objects share ownership.

The object is destroyed only when the last owner releases it.

Example:

```text
Project
   ▲
  / \
Employee Employee
```

Equivalent C++ concept:

```cpp
std::shared_ptr<Project>
```

---

## 3. Borrowed Reference (Non-Owning)

An object temporarily uses another object without owning it.

Example:

```cpp
void print(const Printer& printer);
```

The function borrows the object.

It does not destroy it.

---

## 4. Weak Reference

A weak reference observes an object without increasing its ownership count.

Equivalent C++ concept:

```cpp
std::weak_ptr<T>
```

Useful for avoiding circular references.

---

# ⏳ What is Object Lifetime?

## Definition

Object Lifetime is the period between an object's creation and its destruction.

Every object has a beginning and an end.

Understanding object lifetime helps prevent accessing invalid memory.

---

# 🧠 Lifetime Example

```cpp
{
    Student student;
}
```

Object is created at the opening brace.

Object is destroyed at the closing brace.

---

# 📦 Stack vs Heap Objects

## Stack Objects

```cpp
Student student;
```

Characteristics:

* Automatic memory management
* Fast allocation
* Fast deallocation
* Destroyed automatically when scope ends

Example:

```text
Stack

+----------------+
| Student        |
+----------------+
```

---

## Heap Objects

```cpp
Student* student = new Student();
```

Characteristics:

* Dynamically allocated
* Manual management (or smart pointers)
* Exists until explicitly destroyed

Example:

```text
Stack

+-------------------+
| student ---------+------+
+-------------------+      |
                           |
Heap                       |
+----------------------+   |
| Student Object       |<--+
+----------------------+
```

---

# ⚠️ Manual Memory Management

Using `new` requires a matching `delete`.

```cpp
Student* student = new Student();

delete student;
```

Forgetting `delete` causes memory leaks.

Deleting twice causes undefined behavior.

Modern C++ recommends avoiding raw owning pointers.

---

# 🔥 RAII (Resource Acquisition Is Initialization)

## Definition

RAII is a C++ programming technique where:

* Resources are acquired during object construction.
* Resources are released automatically during object destruction.

Resources include:

* Memory
* Files
* Database connections
* Network sockets
* Mutexes

RAII ensures exception-safe resource management.

---

# 💡 Smart Pointers

Modern C++ provides smart pointers to manage ownership automatically.

---

## std::unique_ptr

Exclusive ownership.

```cpp
std::unique_ptr<Car> car = std::make_unique<Car>();
```

Characteristics:

* Single owner
* Cannot be copied
* Can be moved
* Automatically deletes the object

Use when exactly one object owns another.

---

## std::shared_ptr

Shared ownership.

```cpp
std::shared_ptr<Book> book =
    std::make_shared<Book>();
```

Characteristics:

* Multiple owners
* Uses reference counting
* Object destroyed when count becomes zero

---

## std::weak_ptr

Non-owning observer.

```cpp
std::weak_ptr<Book> weakBook = sharedBook;
```

Characteristics:

* Does not increase reference count
* Prevents circular references
* Must be converted to `shared_ptr` before use

---

# 🔄 Ownership Models

| Ownership  | C++ Type                |
| ---------- | ----------------------- |
| Exclusive  | std::unique_ptr         |
| Shared     | std::shared_ptr         |
| Non-owning | Raw Pointer / Reference |
| Observer   | std::weak_ptr           |

---

# 🏗 Memory Management in LLD

Ownership is one of the most important design decisions.

Examples:

### Composition

```text
House
  ◆
Room
```

House owns Room.

---

### Aggregation

```text
Department
  ◇
Employee
```

Department uses Employee.

Employee manages its own lifetime.

---

### Dependency

```text
Order

-----> Payment Service
```

Temporary usage.

No ownership.

---

# 📊 Ownership Decision Flow

```text
Do you own the object?

        │
        ▼
      YES
        │
        ▼
Only one owner?

   │             │
  YES           NO
   │             │
   ▼             ▼
unique_ptr   shared_ptr

        ▲
        │
Need only to observe?

        │
        ▼
     weak_ptr

No ownership?

        │
        ▼
Reference / Raw Pointer
```

---

# ⭐ Best Practices

* Prefer stack allocation whenever possible.
* Use `std::unique_ptr` for exclusive ownership.
* Use `std::shared_ptr` only when ownership is genuinely shared.
* Use `std::weak_ptr` to break cyclic references.
* Avoid raw owning pointers.
* Clearly define ownership responsibilities.
* Follow the RAII principle.
* Prefer automatic lifetime management over manual memory management.

---

# 🚫 Common Mistakes

### ❌ Forgetting `delete`

```cpp
Student* s = new Student();
```

Memory leak.

---

### ❌ Double Delete

```cpp
delete student;
delete student;
```

Undefined behavior.

---

### ❌ Dangling Pointer

```cpp
delete student;

student->display();
```

Accessing destroyed memory.

---

### ❌ Circular Reference

```cpp
shared_ptr<A> → shared_ptr<B>

shared_ptr<B> → shared_ptr<A>
```

Objects are never destroyed.

Use `std::weak_ptr`.

---

### ❌ Overusing `shared_ptr`

Not every object needs shared ownership.

Prefer `std::unique_ptr` unless multiple owners are truly required.

---

# 🎤 Interview Questions

1. What is Object Ownership?
2. What is Object Lifetime?
3. Difference between Stack and Heap memory?
4. Explain RAII.
5. What is `std::unique_ptr`?
6. Difference between `unique_ptr` and `shared_ptr`?
7. Why do we need `std::weak_ptr`?
8. What is a dangling pointer?
9. What is a memory leak?
10. What is a circular reference?
11. When should you use stack allocation?
12. When should you use heap allocation?

---

# 📝 Practice Problems

## Beginner

Create a `Car` class using:

* Stack allocation
* Heap allocation

Observe object lifetime.

---

## Intermediate

Design:

* House
* Room

Use:

```cpp
std::unique_ptr<Room>
```

---

## Intermediate

Design:

* Library
* Book

Use:

```cpp
std::shared_ptr<Book>
```

---

## Advanced

Design a Social Media System.

Classes:

* User
* Profile
* Post

Requirements:

* A User exclusively owns a Profile.
* Multiple Users can share a Post.
* Comments observe Posts without owning them.

Choose appropriate ownership models (`unique_ptr`, `shared_ptr`, `weak_ptr`) and justify your decisions.

---

# 🧠 Key Takeaways

* Every object has an owner or clearly defined non-owner.
* Object Lifetime begins at creation and ends at destruction.
* Prefer stack allocation whenever practical.
* Use smart pointers instead of raw owning pointers.
* `std::unique_ptr` represents exclusive ownership.
* `std::shared_ptr` represents shared ownership.
* `std::weak_ptr` prevents circular references.
* RAII is the foundation of safe resource management in modern C++.
* Proper ownership design leads to safer, cleaner, and more maintainable LLD solutions.

---

# 📚 Revision Cheat Sheet

| Topic             | Key Point                        |
| ----------------- | -------------------------------- |
| Object Ownership  | Who manages an object's lifetime |
| Object Lifetime   | Creation → Destruction           |
| Stack Object      | Automatic lifetime               |
| Heap Object       | Dynamic lifetime                 |
| `std::unique_ptr` | Exclusive ownership              |
| `std::shared_ptr` | Shared ownership                 |
| `std::weak_ptr`   | Non-owning observer              |
| RAII              | Automatic resource management    |
| Memory Leak       | Memory not released              |
| Dangling Pointer  | Pointer to destroyed object      |

---

# 🚀 Next Lesson

**Lesson 6: Delegation**

Topics to be Covered:

* What is Delegation?
* Why Delegation?
* Delegation vs Inheritance
* Delegation vs Composition
* Forwarding Requests
* Real-World Examples
* UML Representation
* C++ Implementation
* Delegation Pattern
* LLD Use Cases
* Interview Questions
* Best Practices
