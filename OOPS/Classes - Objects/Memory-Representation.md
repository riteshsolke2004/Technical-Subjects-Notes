# Memory Representation of Class and Object

## Does Class Occupy Memory?

No.

A class is only a blueprint.

Example:

```cpp
class Student {
public:
    int age;
};
```

Memory = 0 bytes

---

## Does Object Occupy Memory?

Yes.

Example:

```cpp
Student s1;
```

Memory is allocated for:

- Data members

Not for:

- Member functions

---

## Example

```cpp
class Test {
public:
    int a;
    int b;
};
```

Object:

```cpp
Test t1;
```

Memory allocated:

```
a → 4 bytes
b → 4 bytes

Total = 8 bytes
```

---

## Memory Diagram

```
Class Student
----------------
age
name
display()

(No memory)

Object s1
----------------
age = 20
name = "Ritu"

(Memory allocated)
```

---

## Important Points

- Functions are shared by all objects.
- Variables get separate memory for each object.
- Class itself occupies no memory.

---

## Example Program

```cpp
#include<iostream>
using namespace std;

class Test {
public:
    int a;
    int b;
};

int main() {

    Test t1;

    cout << sizeof(t1);

    return 0;
}
```

---

## Output

```
8
```

---

## Interview Questions

### Does a class occupy memory?

No.

### What occupies memory?

Objects.

### Are member functions duplicated for each object?

No.
