# Constructors in C++

## Introduction

A **constructor** is a special member function of a class that is automatically called when an object of the class is created. It is primarily used to initialize the data members of an object.

Constructors help ensure that every object starts with meaningful values without requiring an explicit function call.

---

# Definition

A **constructor** is a special member function that:

* Has the same name as the class.
* Has no return type (not even `void`).
* Is automatically invoked when an object is created.
* Is used to initialize the object's data members.

---

# Characteristics of a Constructor

* Constructor name must be the same as the class name.
* It does not have any return type.
* It is called automatically when an object is created.
* It can be overloaded.
* It can have default arguments.
* It cannot be declared as `virtual`, `static`, or `const`.

---

# Syntax

```cpp
class ClassName
{
public:
    ClassName()
    {
        // Initialization code
    }
};
```

---

# Basic Example

```cpp
#include <iostream>
using namespace std;

class Student
{
public:
    Student()
    {
        cout << "Constructor Called!" << endl;
    }
};

int main()
{
    Student s;

    return 0;
}
```

### Output

```text
Constructor Called!
```

---

# Why Do We Need Constructors?

* Automatically initialize objects.
* Reduce repetitive initialization code.
* Improve code readability.
* Ensure objects are created in a valid state.

---

# Types of Constructors

1. Default Constructor
2. Parameterized Constructor
3. Copy Constructor
4. Dynamic Constructor
5. Constructor Overloading

---

# 1. Default Constructor

A constructor with **no parameters** is called a default constructor.

### Example

```cpp
#include <iostream>
using namespace std;

class Student
{
public:
    Student()
    {
        cout << "Default Constructor Called" << endl;
    }
};

int main()
{
    Student s;

    return 0;
}
```

### Output

```text
Default Constructor Called
```

---

# 2. Parameterized Constructor

A constructor that accepts one or more parameters.

### Example

```cpp
#include <iostream>
using namespace std;

class Student
{
private:
    string name;
    int rollNo;

public:
    Student(string n, int r)
    {
        name = n;
        rollNo = r;
    }

    void display()
    {
        cout << "Name : " << name << endl;
        cout << "Roll No : " << rollNo << endl;
    }
};

int main()
{
    Student s("Ritesh", 23);

    s.display();

    return 0;
}
```

### Output

```text
Name : Ritesh
Roll No : 23
```

---

# 3. Copy Constructor

A constructor that creates a new object by copying an existing object.

### Syntax

```cpp
ClassName(const ClassName &obj);
```

### Example

```cpp
#include <iostream>
using namespace std;

class Student
{
private:
    string name;

public:
    Student(string n)
    {
        name = n;
    }

    Student(const Student &obj)
    {
        name = obj.name;
    }

    void display()
    {
        cout << name << endl;
    }
};

int main()
{
    Student s1("Ritesh");

    Student s2 = s1;

    s2.display();

    return 0;
}
```

### Output

```text
Ritesh
```

---

# 4. Dynamic Constructor

A constructor that allocates memory dynamically using `new`.

### Example

```cpp
#include <iostream>
#include <cstring>
using namespace std;

class Student
{
private:
    char *name;

public:
    Student(const char *n)
    {
        name = new char[strlen(n) + 1];
        strcpy(name, n);
    }

    void display()
    {
        cout << "Name : " << name << endl;
    }

    ~Student()
    {
        delete[] name;
    }
};

int main()
{
    Student s("Ritesh");

    s.display();

    return 0;
}
```

---

# 5. Constructor Overloading

Having multiple constructors with different parameter lists in the same class.

### Example

```cpp
#include <iostream>
using namespace std;

class Student
{
public:
    Student()
    {
        cout << "Default Constructor" << endl;
    }

    Student(string name)
    {
        cout << "Parameterized Constructor : " << name << endl;
    }

    Student(string name, int roll)
    {
        cout << name << " " << roll << endl;
    }
};

int main()
{
    Student s1;
    Student s2("Ritesh");
    Student s3("Rahul", 45);

    return 0;
}
```

---

# Constructor Overloading Diagram

```text
                Student()
                    |
     -------------------------------
     |                             |
Student(string)       Student(string,int)
```

---

# Constructor vs Normal Function

| Constructor                      | Normal Function              |
| -------------------------------- | ---------------------------- |
| Same name as class               | Any valid name               |
| No return type                   | Has a return type            |
| Called automatically             | Called explicitly            |
| Initializes objects              | Performs operations          |
| Invoked once per object creation | Can be called multiple times |

---

# Rules for Constructors

* Constructor name must match the class name.
* Constructors cannot return a value.
* Constructors are automatically called.
* Constructors can be overloaded.
* Constructors cannot be inherited.
* Constructors cannot be `virtual`.
* Constructors cannot be `static`.

---

# Advantages

* Automatic object initialization.
* Improves code readability.
* Saves time.
* Reduces initialization errors.
* Supports constructor overloading.

---

# Disadvantages

* Slight increase in memory usage for initialization logic.
* Incorrect constructor design can create ambiguity.
* Dynamic constructors require proper memory management.

---

# Real-Life Examples

* Creating a bank account with an initial balance.
* Registering a student with a name and roll number.
* Creating a car object with brand and model.
* Creating an employee with ID and salary.

---

# Common Mistakes

### 1. Giving a return type

❌ Incorrect

```cpp
void Student()
{
}
```

### Correct

```cpp
Student()
{
}
```

---

### 2. Calling a parameterized constructor incorrectly

```cpp
Student s("Ritesh", 23);
```

If the constructor expects:

```cpp
Student(string name, int roll)
```

the argument order must match.

---

### 3. Forgetting the Default Constructor

If only a parameterized constructor exists:

```cpp
Student(string name)
{
}
```

then:

```cpp
Student s;
```

will produce an error because no default constructor exists.

---

# Viva Questions

### 1. What is a constructor?

A constructor is a special member function that initializes an object and is automatically called when the object is created.

### 2. Can a constructor have a return type?

No.

### 3. Can constructors be overloaded?

Yes.

### 4. What is a default constructor?

A constructor with no parameters.

### 5. What is a parameterized constructor?

A constructor that accepts parameters.

### 6. What is a copy constructor?

A constructor that initializes one object using another object of the same class.

### 7. Why is a dynamic constructor used?

To allocate memory dynamically during object creation.

### 8. How many times is a constructor called?

Once for every object created.

### 9. Can constructors be inherited?

No.

### 10. Can constructors be virtual?

No.

---

# Interview Questions

1. What is a constructor?
2. Explain different types of constructors.
3. What is constructor overloading?
4. What is a copy constructor?
5. What is a dynamic constructor?
6. Why can't constructors have a return type?
7. Difference between constructor and destructor.
8. When is a copy constructor called?
9. Explain shallow copy and deep copy.
10. Why is a destructor needed with a dynamic constructor?

---

# Summary

* A constructor is a special member function used to initialize objects.
* It is automatically called when an object is created.
* Constructors have the same name as the class and do not have a return type.
* The main types of constructors are:

  * Default Constructor
  * Parameterized Constructor
  * Copy Constructor
  * Dynamic Constructor
  * Constructor Overloading
* Constructors make object creation simple, safe, and efficient in Object-Oriented Programming.
