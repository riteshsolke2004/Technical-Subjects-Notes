# Creating Objects

## Syntax

```cpp
ClassName objectName;
```

Example:

```cpp
Student s1;
```

---

## Accessing Members

Using dot operator:

```cpp
s1.name = "Ritu";
s1.display();
```

---

## Creating Multiple Objects

```cpp
Student s1;
Student s2;
Student s3;
```

---

## Example Program

```cpp
#include<iostream>
using namespace std;

class Employee {
public:
    string name;
    int salary;
};

int main() {

    Employee e1;
    Employee e2;

    e1.name = "Ritu";
    e1.salary = 50000;

    e2.name = "Rahul";
    e2.salary = 60000;

    cout << e1.name << endl;
    cout << e2.name << endl;

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

## Dot Operator

The dot operator (.) is used to access:

- Variables
- Functions

Example:

```cpp
object.variable
object.function()
```

---

## Summary

Objects are created using class names and accessed using the dot operator.
