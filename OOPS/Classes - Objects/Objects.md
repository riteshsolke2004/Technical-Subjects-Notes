# Object in OOP

## Definition

An object is an instance of a class.

It represents a real-world entity.

---

## Syntax

```cpp
Student s1;
```

Here:

- Student → Class
- s1 → Object

---

## Why Objects are Needed?

Objects allow us to:

- Store data separately
- Access member functions
- Represent real-world entities

---

## Example

```cpp
class Student {
public:
    string name;
};
```

Creating object:

```cpp
Student s1;
```

---

## Multiple Objects

```cpp
Student s1;
Student s2;
Student s3;
```

Each object has its own copy of data members.

---

## Real World Example

Class:

```
Car
```

Objects:

- BMW
- Audi
- Mercedes

---

## Complete Program

```cpp
#include<iostream>
using namespace std;

class Student {
public:
    string name;
};

int main() {

    Student s1;
    Student s2;

    s1.name = "Ritu";
    s2.name = "Rahul";

    cout << s1.name << endl;
    cout << s2.name << endl;

    return 0;
}
```

---

## Output

```
Ritu
Rahul
```

---

## Interview Questions

### What is an object?

An object is an instance of a class.

### Can multiple objects be created from one class?

Yes.

### Do objects share data members?

No. Each object has its own copy.

---

## Summary

Objects are used to represent real-world entities using classes.
