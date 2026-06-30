# 📘 Advanced OOP for LLD

# Lesson 3: Composition

## 📌 Table of Contents

* Introduction
* What is Composition?
* Why Do We Need Composition?
* Characteristics
* Real-World Examples
* UML Representation
* Ownership
* Object Lifetime
* Memory Representation
* Constructor & Destructor Order
* C++ Implementation
* Composition in Low-Level Design (LLD)
* RAII (Introduction)
* Comparison
* Advantages
* Disadvantages
* Best Practices
* Common Mistakes
* Interview Questions
* Practice Problems
* Summary

---

# 📖 Introduction

In Object-Oriented Programming (OOP), objects often work together through relationships.

Among all object relationships, **Composition** is the **strongest**.

Composition represents a relationship where one object **owns** another object. The child object cannot exist independently and its lifetime is completely controlled by the parent object.

Composition is widely used in **Low-Level Design (LLD)** because it accurately models ownership and lifecycle in real-world software systems.

---

# ✅ What is Composition?

## Definition

Composition is a **strong Has-A relationship** in which one object completely owns another object.

The child object **cannot exist independently**.

If the parent object is destroyed, the child object is also destroyed automatically.

## Simple Definition

> Composition is a **Has-A relationship with strong ownership**.

---

# 🎯 Why Do We Need Composition?

Consider a **House**.

A house has rooms.

If the house is demolished, the rooms disappear as well.

Rooms have no meaning without the house.

This is exactly what Composition models.

Another example:

A book contains pages.

Delete the book.

The pages are deleted too.

---

# ✨ Characteristics

* Has-A relationship
* Strong ownership
* Dependent object lifetime
* Parent creates child
* Parent destroys child
* Child belongs to one parent
* Child cannot exist independently

---

# 🌍 Real-World Examples

| Parent Object | Child Object |
| ------------- | ------------ |
| House         | Room         |
| Book          | Page         |
| Human         | Heart        |
| Order         | Order Item   |
| Computer      | CPU          |
| Car           | Engine*      |

> **Note:** Whether **Car → Engine** is Composition or Aggregation depends on business rules. If the engine is permanently owned by one car, Composition is appropriate. If it can be detached and reused elsewhere, Aggregation may be a better choice.

---

# 📊 UML Representation

Composition is represented using a **Filled Diamond (◆)**.

```text
+---------+      +--------+
| House   |◆-----| Room   |
+---------+      +--------+
```

The filled diamond is always placed on the **parent (owner)** side.

---

# 🔑 Ownership

Composition represents **strong ownership**.

The parent object is responsible for:

* Creating the child
* Managing the child
* Destroying the child

The child object cannot manage its own lifetime independently.

---

# ⏳ Object Lifetime

In Composition:

* Parent is created
* Child is automatically created
* Parent is destroyed
* Child is automatically destroyed

This is called **dependent object lifetime**.

---

# 🧠 Memory Representation

```text
Stack Memory

+----------------------------+
| House                      |
| ├── Room bedroom           |
| └── Room kitchen           |
+----------------------------+
```

The child objects are part of the parent object.

They are **not independent objects**.

---

# 🏗 Constructor & Destructor Order

## Object Creation

When a parent object is created:

1. Member objects are created first.
2. Parent constructor executes.

Example:

```text
Room()

↓

Room()

↓

House()
```

---

## Object Destruction

When a parent object is destroyed:

1. Parent destructor executes.
2. Member objects are destroyed in reverse order.

Example:

```text
~House()

↓

~Room()

↓

~Room()
```

This order is guaranteed by C++.

---

# 💻 C++ Example

```cpp
#include <iostream>

using namespace std;

class Room
{
public:
    Room()
    {
        cout << "Room Created\n";
    }

    ~Room()
    {
        cout << "Room Destroyed\n";
    }
};

class House
{
private:
    Room bedroom;
    Room kitchen;

public:
    House()
    {
        cout << "House Created\n";
    }

    ~House()
    {
        cout << "House Destroyed\n";
    }
};

int main()
{
    House house;

    return 0;
}
```

### Output

```text
Room Created
Room Created
House Created
House Destroyed
Room Destroyed
Room Destroyed
```

Notice:

* Rooms are created automatically.
* Rooms are destroyed automatically.
* House owns its rooms.

---

# 🏗 Composition in LLD

Composition appears frequently in software design.

## Order Management System

```text
Order
  ◆
  |
Order Items
```

Deleting an Order removes its Order Items.

---

## Library System

```text
Book
 ◆
 |
Pages
```

Deleting a Book removes its Pages.

---

## Computer System

```text
Computer
   ◆
   |
CPU
RAM
Motherboard
```

These components are considered owned by the Computer in this model.

---

## Human Body

```text
Human
 ◆
 |
Heart
```

Heart is an integral part of Human.

---

# 🛡 RAII (Resource Acquisition Is Initialization)

Composition naturally supports **RAII**, one of the most important concepts in C++.

Resources are acquired during object construction and automatically released during destruction.

Examples:

* File handles
* Database connections
* Network sockets
* Mutex locks

RAII helps prevent memory leaks and resource leaks.

---

# ⚖️ Comparison

## Association vs Aggregation vs Composition

| Feature               | Association  | Aggregation        | Composition        |
| --------------------- | ------------ | ------------------ | ------------------ |
| Relationship          | Knows / Uses | Has-A              | Has-A              |
| Ownership             | None         | Weak               | Strong             |
| Lifetime              | Independent  | Independent        | Dependent          |
| Child Survives Parent | Yes          | Yes                | No                 |
| UML Symbol            | Line         | Hollow Diamond (◇) | Filled Diamond (◆) |
| Object Sharing        | Yes          | Yes                | No (typically)     |

---

## Aggregation vs Composition

| Feature              | Aggregation    | Composition    |
| -------------------- | -------------- | -------------- |
| Ownership            | Weak           | Strong         |
| Lifetime             | Independent    | Dependent      |
| Child Shared         | Yes            | No             |
| Parent Deletes Child | No             | Yes            |
| UML                  | Hollow Diamond | Filled Diamond |

---

# ✅ Advantages

* Clear ownership
* Automatic lifetime management
* Reduced memory leaks
* High encapsulation
* Strong object integrity
* Excellent for modelling real-world ownership

---

# ❌ Disadvantages

* Less flexibility
* Child cannot be reused independently
* Tight coupling between parent and child
* Difficult to share child objects

---

# ⭐ Best Practices

* Use Composition only when ownership is required.
* Prefer value members when possible.
* If dynamic allocation is required, use `std::unique_ptr` to express exclusive ownership.
* Avoid raw owning pointers.
* Let constructors initialize owned objects.
* Let destructors clean them automatically.

---

# 🚫 Common Mistakes

### ❌ Confusing Composition with Aggregation

Ask yourself:

> Can the child exist without the parent?

If **Yes**

→ Aggregation

If **No**

→ Composition

---

### ❌ Assuming every Has-A relationship is Composition

Not every Has-A relationship implies ownership.

Always analyze the business requirements.

---

### ❌ Using raw pointers for owned objects

Instead of:

```cpp
Room* room;
```

Prefer:

```cpp
Room room;
```

or

```cpp
std::unique_ptr<Room> room;
```

when dynamic allocation is needed.

---

# 🎤 Interview Questions

1. What is Composition?
2. Why is Composition called strong ownership?
3. Difference between Aggregation and Composition?
4. Explain dependent object lifetime.
5. Draw the UML notation for Composition.
6. Explain constructor and destructor order.
7. Why is Composition preferred over inheritance in many cases?
8. Give five real-world examples.
9. What is RAII?
10. Explain Composition using memory representation.

---

# 📝 Practice Problems

## Beginner

Design:

* Book
* Page

---

## Intermediate

Design:

* House
* Room

---

## Intermediate

Design:

* Computer
* CPU
* RAM
* Motherboard

---

## Advanced

Design an Online Shopping System.

Classes:

* Order
* Order Item
* Invoice

Deleting an Order should automatically remove:

* Order Items
* Invoice

Use Composition.

---

# 🧠 Key Takeaways

* Composition is a **strong Has-A relationship**.
* Parent owns the child.
* Child cannot exist independently.
* Parent controls creation and destruction.
* UML uses a **Filled Diamond (◆)**.
* Composition models ownership and lifecycle.
* RAII works naturally with Composition.
* Composition is one of the most important relationships in LLD.

---

# 📚 Revision Cheat Sheet

| Topic                | Key Point                              |
| -------------------- | -------------------------------------- |
| Relationship         | Has-A                                  |
| Ownership            | Strong                                 |
| Lifetime             | Dependent                              |
| UML Symbol           | Filled Diamond (◆)                     |
| Object Sharing       | No (typically)                         |
| Parent Deletes Child | Yes                                    |
| Common Examples      | House–Room, Book–Page, Order–OrderItem |

---

# 🚀 Next Lesson

**Lesson 4: Dependency**

Topics to be Covered:

* What is Dependency?
* Temporary Relationships
* Dependency vs Association
* Method Dependency
* Constructor Dependency
* UML Dependency Notation
* Dependency Injection (Introduction)
* C++ Examples
* LLD Use Cases
* Interview Questions
