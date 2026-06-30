# 📘 Advanced OOP for LLD

# Lesson 2: Aggregation

## 📌 Table of Contents

* Introduction
* What is Aggregation?
* Why Do We Need Aggregation?
* Characteristics
* Real-World Examples
* UML Representation
* Ownership
* Memory Representation
* C++ Implementation
* Lifetime of Objects
* Multiplicity
* Aggregation in Low-Level Design (LLD)
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

In Object-Oriented Programming (OOP), objects often need to work together. These relationships help us model real-world systems accurately.

**Aggregation** is one of the most commonly used object relationships in Low-Level Design (LLD).

It represents a **"Has-A"** relationship where one object contains or refers to another object, but **does not own its lifetime**.

---

# ✅ What is Aggregation?

### Definition

Aggregation is a **specialized form of Association** where one class contains or refers to another class, but both objects can exist independently.

The parent object uses the child object, but it is **not responsible for creating or destroying it**.

### Simple Definition

> Aggregation is a **Has-A relationship with weak ownership**.

---

# 🎯 Why Do We Need Aggregation?

Without Aggregation, every object would have to own the objects it works with.

Consider a university.

A university has professors.

If the university closes, should all professors disappear?

**No.**

Professors can join another university.

This demonstrates **independent object lifetime**, which is exactly what Aggregation models.

---

# ✨ Characteristics

* Has-A relationship
* Weak ownership
* Independent object lifetime
* Objects are reusable
* Parent does not destroy child
* Child can exist without parent
* Parent only maintains references/pointers

---

# 🌍 Real-World Examples

| Whole Object | Part Object |
| ------------ | ----------- |
| University   | Professor   |
| Department   | Employee    |
| Team         | Player      |
| Playlist     | Song        |
| Library      | Book        |
| Company      | Employee    |
| Hospital     | Doctor      |

---

# 📊 UML Representation

Aggregation is represented using a **Hollow Diamond (◇)**.

```text
+-------------+        +-----------+
| Department  |◇-------| Employee  |
+-------------+        +-----------+
```

The diamond is always placed on the **whole (parent)** side.

---

# 🔑 Ownership

Aggregation provides **weak ownership**.

The parent object only references the child object.

It does **not** control the child's lifetime.

### Example

Department has Employees.

Deleting the Department **does not** delete Employees.

Employees continue to exist.

---

# 🧠 Memory Representation

```text
Stack

+----------------------+
| Department           |
| employees ----------+------------------+
+----------------------+                  |
                                          |
+----------------------+                  |
| Employee Rahul       |<-----------------+
+----------------------+

+----------------------+
| Employee Priya       |<-----------------+
+----------------------+
```

The Department stores only references or pointers.

Employees are created independently.

---

# 💻 C++ Example

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

class Employee
{
public:
    string name;

    Employee(string name)
    {
        this->name = name;
    }
};

class Department
{
private:
    vector<Employee*> employees;

public:
    void addEmployee(Employee* emp)
    {
        employees.push_back(emp);
    }

    void showEmployees()
    {
        cout << "Employees:\n";

        for (Employee* emp : employees)
        {
            cout << emp->name << endl;
        }
    }
};

int main()
{
    Employee e1("Rahul");
    Employee e2("Priya");

    Department d;

    d.addEmployee(&e1);
    d.addEmployee(&e2);

    d.showEmployees();

    return 0;
}
```

### Output

```text
Employees:
Rahul
Priya
```

---

# ⏳ Lifetime of Objects

```cpp
{
    Department d;
}
```

Department is destroyed.

Employees remain alive.

This proves that Aggregation has **independent object lifetime**.

---

# 📈 Multiplicity

Multiplicity defines how many objects participate in a relationship.

| Notation | Meaning      |
| -------- | ------------ |
| 1        | Exactly one  |
| 0..1     | Zero or one  |
| *        | Many         |
| 1..*     | One or more  |
| 0..*     | Zero or more |

Example:

```text
Department 1 -------- * Employee
```

One Department has many Employees.

---

# 🏗 Aggregation in LLD

Aggregation appears frequently in real-world system design.

### Library Management System

```text
Library
    ◇
    |
 Books
```

Books can move to another library.

---

### Hospital Management System

```text
Hospital
    ◇
    |
 Doctors
```

Doctors may work elsewhere.

---

### Company Management System

```text
Company
    ◇
    |
 Employees
```

Employees can resign or join another company.

---

### School Management System

```text
School
    ◇
    |
 Teachers
```

Teachers are independent entities.

---

# ⚖️ Comparison

## Association vs Aggregation

| Feature      | Association     | Aggregation         |
| ------------ | --------------- | ------------------- |
| Relationship | Knows           | Has                 |
| Ownership    | No              | Weak                |
| Lifetime     | Independent     | Independent         |
| UML          | Simple Line     | Hollow Diamond      |
| Example      | Student–Teacher | Department–Employee |

---

## Aggregation vs Composition

| Feature          | Aggregation    | Composition        |
| ---------------- | -------------- | ------------------ |
| Ownership        | Weak           | Strong             |
| Lifetime         | Independent    | Dependent          |
| Sharing          | Allowed        | Not Allowed        |
| Parent Destroyed | Child survives | Child is destroyed |
| UML              | Hollow Diamond | Filled Diamond     |

---

# ✅ Advantages

* Encourages object reuse
* Loose coupling
* Flexible design
* Easy maintenance
* Independent object lifetime
* Suitable for real-world modelling

---

# ❌ Disadvantages

* Parent does not control child lifecycle
* Relationships must be managed carefully
* Dangling pointers are possible when using raw pointers incorrectly
* Ownership rules must be clearly defined

---

# ⭐ Best Practices

* Prefer references or smart pointers over raw pointers when appropriate.
* Clearly document ownership.
* Keep Aggregation loosely coupled.
* Avoid unnecessary object creation.
* Model real-world relationships accurately.

---

# 🚫 Common Mistakes

### ❌ Creating child objects inside the parent

```cpp
class Department
{
    Employee employee;
};
```

This is **not Aggregation**.

---

### ❌ Deleting objects you do not own

```cpp
delete employee;
```

Never destroy an object unless your class owns it.

---

### ❌ Confusing Aggregation with Composition

Remember:

Aggregation → Weak ownership

Composition → Strong ownership

---

# 🎤 Interview Questions

1. What is Aggregation?
2. Why is Aggregation called weak ownership?
3. Difference between Association and Aggregation?
4. Difference between Aggregation and Composition?
5. Explain Aggregation using a real-world example.
6. Draw the UML notation for Aggregation.
7. What happens when the parent object is destroyed?
8. Why are pointers or references commonly used in Aggregation?
9. Can one child object belong to multiple parent objects?
10. Where is Aggregation used in LLD?

---

# 📝 Practice Problems

### Beginner

* School → Teacher
* Team → Player
* Library → Book

### Intermediate

Design:

* Company
* Employee
* Department

### Advanced

Design a Hospital Management System with:

* Hospital
* Department
* Doctor
* Patient

Use Aggregation wherever appropriate.

---

# 🧠 Key Takeaways

* Aggregation is a **Has-A** relationship.
* It is a specialized form of Association.
* It represents **weak ownership**.
* Parent and child have **independent lifetimes**.
* UML uses a **Hollow Diamond (◇)**.
* Widely used in Low-Level Design.
* Objects can be shared and reused.
* The parent does not create or destroy the child.

---

# 📚 Revision Cheat Sheet

| Topic                 | Key Point                                          |
| --------------------- | -------------------------------------------------- |
| Relationship          | Has-A                                              |
| Ownership             | Weak                                               |
| Lifetime              | Independent                                        |
| UML Symbol            | Hollow Diamond (◇)                                 |
| Object Sharing        | Allowed                                            |
| Parent Deletes Child? | No                                                 |
| Common Examples       | Department–Employee, Library–Book, Hospital–Doctor |

---

# 🚀 Next Lesson

**Lesson 3: Composition**

Topics to be covered:

* Strong Ownership
* Dependent Object Lifetime
* Filled Diamond in UML
* Memory Management
* RAII Concept
* C++ Implementation
* LLD Examples
* Interview Questions
* Aggregation vs Composition (In-depth)
