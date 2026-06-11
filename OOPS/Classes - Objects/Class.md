# Class in OOP

## Definition

A class is a user-defined blueprint or template used to create objects.

It contains:

- Data Members (Variables)
- Member Functions (Methods)

---

## Syntax

```cpp
class Student {
public:
    string name;
    int age;

    void display() {
        cout << name << endl;
        cout << age << endl;
    }
};
```

---

## Components of a Class

### 1. Data Members

Variables declared inside a class.

Example:

```cpp
string name;
int age;
```

---

### 2. Member Functions

Functions defined inside a class.

Example:

```cpp
void display() {
    cout << name;
}
```

---

### 3. Access Specifiers

- Public
- Private
- Protected

---

## Characteristics of Class

- User-defined data type
- Acts as a blueprint
- Supports encapsulation
- Improves modularity
- Enables code reuse

---

## Real World Example

### Class → Car

Properties:

- Brand
- Color
- Speed

Methods:

- Start()
- Stop()
- Accelerate()

---

## Advantages

- Organizes code
- Easy maintenance
- Supports OOP concepts
- Reduces complexity

---

## Complete Example

```cpp
#include<iostream>
using namespace std;

class Student {
public:
    string name;
    int age;

    void display() {
        cout << "Name : " << name << endl;
        cout << "Age : " << age << endl;
    }
};

int main() {

    Student s1;

    s1.name = "Ritu";
    s1.age = 20;

    s1.display();

    return 0;
}
```

---

## Output

```
Name : Ritu
Age : 20
```

---

## Interview Questions

### What is a class?

A class is a blueprint used to create objects.

### Does a class occupy memory?

No. Memory is allocated only when objects are created.

### Which keyword is used to create a class?

`class`

---

## Summary

A class defines the structure and behavior of objects.
