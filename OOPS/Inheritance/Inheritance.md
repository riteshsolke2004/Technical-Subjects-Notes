# Inheritance in C++

## Introduction

Inheritance is one of the four fundamental pillars of Object-Oriented Programming (OOP). It allows a new class (derived class) to inherit the properties and behaviors (data members and member functions) of an existing class (base class). This promotes code reusability, reduces redundancy, and helps organize programs in a hierarchical manner.

---

# Definition

**Inheritance** is the process by which one class acquires the properties and methods of another class.

* **Base Class (Parent Class):** The class whose members are inherited.
* **Derived Class (Child Class):** The class that inherits from the base class.

---

# Syntax

```cpp
class BaseClass
{
    // Data members and member functions
};

class DerivedClass : accessSpecifier BaseClass
{
    // Additional members
};
```

Example:

```cpp
class Student
{
public:
    void display()
    {
        cout << "Student Class";
    }
};

class Result : public Student
{
};
```

---

# Why Use Inheritance?

* Promotes code reusability.
* Reduces code duplication.
* Makes code easier to maintain.
* Represents real-world relationships.
* Improves readability and scalability.

---

# Types of Inheritance

## 1. Single Inheritance

A derived class inherits from one base class.

```text
Student
   |
   |
 Result
```

Example:

```cpp
class Student
{
};

class Result : public Student
{
};
```

---

## 2. Multiple Inheritance

A class inherits from more than one base class.

```text
Student     Sports
     \       /
      \     /
      Result
```

Example:

```cpp
class Student
{
};

class Sports
{
};

class Result : public Student, public Sports
{
};
```

---

## 3. Multilevel Inheritance

A class is derived from another derived class.

```text
Student
   |
 Test
   |
 Result
```

Example:

```cpp
class Student
{
};

class Test : public Student
{
};

class Result : public Test
{
};
```

---

## 4. Hierarchical Inheritance

Multiple derived classes inherit from the same base class.

```text
          Person
         /      \
    Student    Teacher
```

Example:

```cpp
class Person
{
};

class Student : public Person
{
};

class Teacher : public Person
{
};
```

---

## 5. Hybrid Inheritance

Combination of two or more types of inheritance.

```text
          Person
         /      \
    Student   Sports
         \      /
          Result
```

---

# Access Specifiers in Inheritance

| Access Specifier | Meaning                                        |
| ---------------- | ---------------------------------------------- |
| public           | Members remain public in the derived class.    |
| protected        | Public and protected members become protected. |
| private          | Public and protected members become private.   |

---

# Visibility Table

| Base Class Member | Public Inheritance | Protected Inheritance | Private Inheritance |
| ----------------- | ------------------ | --------------------- | ------------------- |
| Public            | Public             | Protected             | Private             |
| Protected         | Protected          | Protected             | Private             |
| Private           | Not Accessible     | Not Accessible        | Not Accessible      |

---

# Example Program

```cpp
#include <iostream>
using namespace std;

class Student
{
protected:
    string name;
    int rollNo;

public:
    void getStudentData()
    {
        cout << "Enter Name: ";
        cin >> name;

        cout << "Enter Roll No: ";
        cin >> rollNo;
    }

    void displayStudentData()
    {
        cout << "\nName : " << name << endl;
        cout << "Roll No : " << rollNo << endl;
    }
};

class Result : public Student
{
private:
    int marks[5];
    int total = 0;
    float percentage;

public:
    void getMarks()
    {
        cout << "\nEnter Marks of 5 Subjects\n";

        for(int i = 0; i < 5; i++)
        {
            cout << "Subject " << i + 1 << ": ";
            cin >> marks[i];
            total += marks[i];
        }

        percentage = total / 5.0;
    }

    void displayResult()
    {
        displayStudentData();

        cout << "\nMarks\n";

        for(int i = 0; i < 5; i++)
        {
            cout << "Subject " << i + 1 << " : " << marks[i] << endl;
        }

        cout << "\nTotal : " << total << endl;
        cout << "Percentage : " << percentage << "%" << endl;
    }
};

int main()
{
    Result r;

    r.getStudentData();
    r.getMarks();
    r.displayResult();

    return 0;
}
```

---

# Advantages

* Code reusability
* Easy maintenance
* Reduced redundancy
* Better code organization
* Supports polymorphism
* Faster application development
* Improves scalability

---

# Disadvantages

* Increases coupling between classes
* Can make debugging difficult
* Deep inheritance trees become complex
* Improper use may reduce flexibility

---

# Real-Life Examples

* Person → Student
* Person → Employee
* Animal → Dog
* Vehicle → Car
* Shape → Circle
* Bank Account → Savings Account

---

# Difference Between Base and Derived Class

| Base Class                           | Derived Class                                             |
| ------------------------------------ | --------------------------------------------------------- |
| Parent class                         | Child class                                               |
| Provides common properties           | Extends the base class                                    |
| Cannot access child-specific members | Can access public and protected members of the base class |

---

# Viva Questions

### 1. What is inheritance?

Inheritance is the process of acquiring the properties and methods of one class into another class.

### 2. Why is inheritance used?

It is used for code reusability, reducing redundancy, and improving maintainability.

### 3. What is a base class?

A class whose members are inherited by another class.

### 4. What is a derived class?

A class that inherits properties and methods from a base class.

### 5. Name the five types of inheritance.

* Single
* Multiple
* Multilevel
* Hierarchical
* Hybrid

### 6. Which access specifiers are used in inheritance?

* Public
* Protected
* Private

### 7. Can private members be inherited?

Private members are inherited but cannot be accessed directly by the derived class.

### 8. Which type of inheritance is most commonly used?

Single inheritance.

---

# Interview Questions

1. What is inheritance?
2. Explain the types of inheritance.
3. Difference between inheritance and composition.
4. Why can't private members be accessed directly in a derived class?
5. What is the purpose of protected access specifier?
6. Explain multilevel inheritance with an example.
7. What is the diamond problem?
8. What is virtual inheritance?
9. What are the advantages and disadvantages of inheritance?
10. Explain public, protected, and private inheritance.

---

# Summary

* Inheritance is an OOP feature that allows one class to inherit the properties and methods of another class.
* It promotes code reuse and simplifies maintenance.
* There are five types of inheritance:

  * Single
  * Multiple
  * Multilevel
  * Hierarchical
  * Hybrid
* Public inheritance is the most commonly used form.
* Inheritance is one of the four pillars of Object-Oriented Programming.
