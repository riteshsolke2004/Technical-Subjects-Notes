# Encapsulation in C++

# Introduction

**Encapsulation** is one of the four fundamental pillars of **Object-Oriented Programming (OOP)**. It is the process of combining **data members (variables)** and **member functions (methods)** into a single unit called a **class**, while restricting direct access to the data.

Encapsulation helps protect an object's internal state by allowing access only through controlled methods.

---

# Definition

**Encapsulation** is the process of **wrapping data members and member functions into a single unit (class)** and **restricting direct access to the data** using access specifiers.

It is also known as **Data Hiding**.

---

# Key Points

* Combines data and functions into one unit.
* Protects data from unauthorized access.
* Achieves data hiding using access specifiers.
* Improves code security and maintainability.
* Makes programs modular and reusable.

---

# Why Do We Need Encapsulation?

* Protect sensitive data.
* Prevent accidental modification.
* Improve code organization.
* Improve security.
* Increase maintainability.
* Allow controlled access through public methods.

---

# How Encapsulation Works

Encapsulation is achieved by:

1. Declaring data members as **private**.
2. Providing **public getter and setter functions** to access or modify the data.

```text id="afvg3n"
             Class
      ------------------
      |  Private Data  |
      |----------------|
      | Public Methods |
      ------------------
```

---

# Access Specifiers

C++ provides three access specifiers.

## 1. Public

* Accessible from anywhere.
* Used for member functions that should be available to users.

```cpp id="tmg3qz"
public:
```

---

## 2. Private

* Accessible only inside the class.
* Cannot be accessed directly from outside the class.

```cpp id="6feg5u"
private:
```

---

## 3. Protected

* Accessible inside the class and derived classes.
* Mainly used in inheritance.

```cpp id="sluxiu"
protected:
```

---

# Example Without Encapsulation

```cpp id="v81pkb"
#include <iostream>
using namespace std;

class Student
{
public:
    string name;
    int marks;
};

int main()
{
    Student s;

    s.name = "Ritesh";
    s.marks = -50;

    cout << s.name << endl;
    cout << s.marks << endl;
}
```

### Problem

Anyone can modify the data directly, even with invalid values.

---

# Example With Encapsulation

```cpp id="3q5kbl"
#include <iostream>
using namespace std;

class Student
{
private:
    string name;
    int marks;

public:

    void setName(string n)
    {
        name = n;
    }

    void setMarks(int m)
    {
        if(m >= 0 && m <= 100)
        {
            marks = m;
        }
        else
        {
            cout << "Invalid Marks" << endl;
        }
    }

    string getName()
    {
        return name;
    }

    int getMarks()
    {
        return marks;
    }
};

int main()
{
    Student s;

    s.setName("Ritesh");
    s.setMarks(95);

    cout << "Name  : " << s.getName() << endl;
    cout << "Marks : " << s.getMarks() << endl;

    return 0;
}
```

### Output

```text id="zdozok"
Name  : Ritesh
Marks : 95
```

---

# Getter Function

## Definition

A **getter** is a public member function used to read the value of a private data member.

### Example

```cpp id="v7e92s"
int getMarks()
{
    return marks;
}
```

---

# Setter Function

## Definition

A **setter** is a public member function used to modify the value of a private data member.

### Example

```cpp id="cv97fj"
void setMarks(int m)
{
    marks = m;
}
```

---

# Data Hiding

## Definition

Data hiding is the process of restricting direct access to the data members of a class.

Example:

```cpp id="eg8iwm"
private:
    int salary;
```

The variable `salary` cannot be accessed directly from outside the class.

---

# Encapsulation Flow

```text id="uhy18o"
User
   |
   |
Public Methods
(Getters/Setters)
   |
   |
Private Data
```

---

# Real-Life Example

### ATM Machine

When you use an ATM:

* You can deposit money.
* You can withdraw money.
* You can check your balance.

But you **cannot directly modify** the bank's database.

The ATM provides controlled access to your account.

This is **Encapsulation**.

---

# Another Example

### Bank Account

Private Data

```text id="3uofqf"
Account Number
Balance
PIN
```

Public Functions

```text id="c5p4gc"
deposit()
withdraw()
checkBalance()
changePIN()
```

Users cannot access the private variables directly.

---

# Advantages

* Data Security
* Data Hiding
* Better Code Organization
* Easier Maintenance
* Improved Flexibility
* Increased Reusability
* Better Control Over Data
* Prevents Invalid Data Entry

---

# Disadvantages

* Slightly more code due to getter and setter methods.
* Additional methods increase class size.
* Can reduce flexibility if access is too restricted.

---

# Encapsulation vs Data Hiding

| Encapsulation                     | Data Hiding                                        |
| --------------------------------- | -------------------------------------------------- |
| Wraps data and functions together | Restricts direct access to data                    |
| Achieved using classes            | Achieved using private/protected access specifiers |
| Focuses on organization           | Focuses on security                                |
| One of the four OOP pillars       | A feature of encapsulation                         |

---

# Encapsulation vs Abstraction

| Encapsulation                    | Abstraction                                    |
| -------------------------------- | ---------------------------------------------- |
| Hides data                       | Hides implementation details                   |
| Achieved using access specifiers | Achieved using abstract classes and interfaces |
| Focuses on data protection       | Focuses on simplicity                          |
| Controls data access             | Controls functionality visibility              |

---

# Common Mistakes

## 1. Declaring Data Members as Public

```cpp id="8pygo8"
public:
    int marks;
```

Anyone can modify the data.

Better:

```cpp id="2e59cf"
private:
    int marks;
```

---

## 2. Not Validating Input in Setter

Incorrect

```cpp id="x1n6cf"
void setMarks(int m)
{
    marks = m;
}
```

Better

```cpp id="yz9f7g"
void setMarks(int m)
{
    if(m >= 0 && m <= 100)
        marks = m;
}
```

---

## 3. Accessing Private Data Directly

Incorrect

```cpp id="2sfe4v"
Student s;

s.marks = 90;
```

Correct

```cpp id="vlj9qy"
s.setMarks(90);
```

---

# Viva Questions

### 1. What is Encapsulation?

Encapsulation is the process of wrapping data members and member functions into a single unit (class) while restricting direct access to data.

---

### 2. Which OOP pillar is Encapsulation?

It is one of the four pillars of Object-Oriented Programming.

---

### 3. How is Encapsulation achieved in C++?

By using classes and access specifiers (`private`, `protected`, `public`).

---

### 4. What is Data Hiding?

Restricting direct access to data members using access specifiers.

---

### 5. What is a Getter?

A public function used to read the value of a private data member.

---

### 6. What is a Setter?

A public function used to modify the value of a private data member.

---

### 7. Why are data members usually private?

To protect the data from unauthorized or invalid modification.

---

### 8. Can private members be accessed directly outside the class?

No.

---

### 9. Which access specifier provides maximum security?

`private`

---

### 10. Give one real-life example of Encapsulation.

An ATM machine or a bank account system.

---

# Interview Questions

1. What is Encapsulation?
2. Explain Data Hiding.
3. Difference between Encapsulation and Abstraction.
4. Why should data members be private?
5. What are getter and setter methods?
6. Explain access specifiers.
7. How does Encapsulation improve security?
8. Can Encapsulation exist without getters and setters?
9. Explain Encapsulation with a bank account example.
10. What are the advantages of Encapsulation?

---

# Summary

* **Encapsulation** is the process of combining **data members and member functions** into a single unit called a **class**.
* It protects data by making data members **private** and providing **public getter and setter methods**.
* Encapsulation improves **security, maintainability, modularity, and code reusability**.
* It is commonly referred to as **Data Hiding** and is one of the **four pillars of Object-Oriented Programming (OOP)**.
