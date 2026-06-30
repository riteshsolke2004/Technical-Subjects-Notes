# Polymorphism in C++

# Introduction

**Polymorphism** is one of the four fundamental pillars of Object-Oriented Programming (OOP). The word **Polymorphism** comes from two Greek words:

* **Poly** = Many
* **Morph** = Forms

It means **"One Interface, Many Forms."**
 
Polymorphism allows the same function, method, or operator to perform different tasks depending on the object or the arguments provided.

---

# Definition

**Polymorphism** is the ability of an object or function to take many forms and perform different actions depending on the situation.

---

# Why Do We Need Polymorphism?

* Improves code reusability.
* Reduces code duplication.
* Makes programs flexible.
* Simplifies maintenance.
* Supports dynamic behavior in applications.

---

# Types of Polymorphism

There are **two types** of polymorphism in C++:

1. **Compile-Time Polymorphism (Static Polymorphism)**
2. **Run-Time Polymorphism (Dynamic Polymorphism)**

```text
                 Polymorphism
                       |
          -------------------------
          |                       |
   Compile-Time             Run-Time
   (Static)                 (Dynamic)
          |                       |
  ----------------         -----------------
  |              |         |
Function     Operator   Function
Overloading  Overloading Overriding
```

---

# 1. Compile-Time Polymorphism

## Definition

Compile-time polymorphism is achieved when the compiler determines which function to call during compilation.

It is also known as:

* Static Binding
* Early Binding

Compile-time polymorphism is achieved by:

* Function Overloading
* Operator Overloading

---

# Function Overloading

## Definition

Function overloading means creating multiple functions with the **same name** but **different parameter lists**.

---

## Example

```cpp
#include <iostream>
using namespace std;

class Calculator
{
public:

    int add(int a, int b)
    {
        return a + b;
    }

    float add(float a, float b)
    {
        return a + b;
    }

    int add(int a, int b, int c)
    {
        return a + b + c;
    }
};

int main()
{
    Calculator c;

    cout << c.add(5,10) << endl;
    cout << c.add(5.5f,2.5f) << endl;
    cout << c.add(2,4,6) << endl;

    return 0;
}
```

### Output

```
15
8
12
```

---

# Operator Overloading

## Definition

Operator overloading allows existing operators to perform different operations for user-defined objects.

---

## Example

```cpp
#include <iostream>
using namespace std;

class Number
{
public:

    int value;

    Number(int v)
    {
        value = v;
    }

    Number operator +(Number obj)
    {
        return Number(value + obj.value);
    }

    void display()
    {
        cout << value << endl;
    }
};

int main()
{
    Number n1(20);
    Number n2(30);

    Number n3 = n1 + n2;

    n3.display();

    return 0;
}
```

### Output

```
50
```

---

# 2. Run-Time Polymorphism

## Definition

Run-time polymorphism is achieved when the function to execute is decided during program execution.

It is also known as:

* Dynamic Binding
* Late Binding

Run-time polymorphism is achieved using:

* Function Overriding
* Virtual Functions

---

# Function Overriding

## Definition

Function overriding occurs when a derived class provides its own implementation of a function already defined in the base class.

---

## Example

```cpp
#include <iostream>
using namespace std;

class Animal
{
public:

    virtual void sound()
    {
        cout << "Animal makes sound" << endl;
    }
};

class Dog : public Animal
{
public:

    void sound() override
    {
        cout << "Dog barks" << endl;
    }
};

int main()
{
    Animal *ptr;

    Dog d;

    ptr = &d;

    ptr->sound();

    return 0;
}
```

### Output

```
Dog barks
```

---

# Virtual Function

## Definition

A **virtual function** is a member function declared with the `virtual` keyword in the base class.

It enables run-time polymorphism by allowing the derived class version of the function to be called through a base class pointer or reference.

---

## Syntax

```cpp
virtual return_type functionName();
```

---

## Example

```cpp
class Animal
{
public:

    virtual void sound()
    {
        cout << "Animal";
    }
};
```

---

# Difference Between Overloading and Overriding

| Function Overloading     | Function Overriding  |
| ------------------------ | -------------------- |
| Same class               | Different classes    |
| Compile-time             | Run-time             |
| Different parameter list | Same parameter list  |
| No inheritance required  | Inheritance required |
| Static binding           | Dynamic binding      |

---

# Compile-Time vs Run-Time Polymorphism

| Compile-Time               | Run-Time                 |
| -------------------------- | ------------------------ |
| Early Binding              | Late Binding             |
| Faster                     | Slightly slower          |
| Decided during compilation | Decided during execution |
| Function Overloading       | Function Overriding      |
| Operator Overloading       | Virtual Functions        |

---

# Advantages

* Code reusability
* Flexibility
* Extensibility
* Easy maintenance
* Reduces complexity
* Supports dynamic behavior
* Improves scalability

---

# Disadvantages

* Run-time polymorphism is slightly slower.
* Virtual functions consume additional memory due to the virtual table (vtable).
* Complex inheritance hierarchies can make debugging difficult.

---

# Real-Life Examples

### Example 1

Vehicle

* Car
* Bike
* Truck

Each has its own implementation of:

```cpp
startEngine();
```

---

### Example 2

Animal

* Dog → Bark
* Cat → Meow
* Cow → Moo

Each overrides:

```cpp
sound();
```

---

### Example 3

Payment System

Payment methods:

* Credit Card
* UPI
* Net Banking

Each implements:

```cpp
pay();
```

---

# Common Mistakes

## 1. Different Parameter List in Overriding

Incorrect

```cpp
void sound(int x)
```

The parameter list must be the same as the base class function.

---

## 2. Forgetting `virtual`

Without `virtual`, the base class function is called instead of the derived class function when using a base class pointer.

---

## 3. Confusing Overloading with Overriding

Overloading

```cpp
add(int,int)
add(float,float)
```

Overriding

```cpp
class Animal
{
    virtual void sound();
};

class Dog : public Animal
{
    void sound() override;
};
```

---

# Viva Questions

### 1. What is polymorphism?

Polymorphism is the ability of one function or object to perform different tasks in different situations.

---

### 2. How many types of polymorphism are there?

* Compile-Time Polymorphism
* Run-Time Polymorphism

---

### 3. What is function overloading?

Using the same function name with different parameter lists.

---

### 4. What is function overriding?

Redefining a base class function in the derived class using the same signature.

---

### 5. What is a virtual function?

A function declared with the `virtual` keyword that enables run-time polymorphism.

---

### 6. Is inheritance required for function overloading?

No.

---

### 7. Is inheritance required for function overriding?

Yes.

---

### 8. Which is faster?

Compile-time polymorphism is generally faster than run-time polymorphism.

---

### 9. Can constructors be virtual?

No.

---

### 10. Which keyword is used for run-time polymorphism?

`virtual`

---

# Interview Questions

1. What is polymorphism?
2. Explain compile-time and run-time polymorphism.
3. What is the difference between overloading and overriding?
4. What is a virtual function?
5. What is dynamic binding?
6. What is early binding?
7. What is late binding?
8. Why do we use the `override` keyword?
9. What is a pure virtual function?
10. What is an abstract class?

---

# Summary

* **Polymorphism** means **One Interface, Many Forms**.
* It allows the same function or interface to behave differently in different contexts.
* There are **two types**:

  * **Compile-Time Polymorphism**

    * Function Overloading
    * Operator Overloading
  * **Run-Time Polymorphism**

    * Function Overriding
    * Virtual Functions
* Compile-time polymorphism uses **static binding**, while run-time polymorphism uses **dynamic binding**.
* Polymorphism improves flexibility, code reuse, and maintainability, making it one of the most important concepts in Object-Oriented Programming.
