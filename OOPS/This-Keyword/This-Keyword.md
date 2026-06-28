# `this` Keyword in C++

## Introduction

The `this` keyword is a special pointer available in every non-static member function of a class. It points to the **current object** that invokes the member function.

Whenever a member function is called using an object, the compiler automatically passes the address of that object using the `this` pointer.

---

# Definition

The **`this` pointer** is a special pointer that holds the address of the current object.

* It is automatically available inside all **non-static member functions**.
* It points to the object that called the member function.

---

# Syntax

```cpp
this
```

Accessing members using `this`:

```cpp
this->variableName;
this->functionName();
```

---

# Why Use `this` Keyword?

* To refer to the current object.
* To resolve naming conflicts between data members and parameters.
* To return the current object.
* To enable method chaining.
* To pass the current object as an argument.

---

# Basic Example

```cpp
#include <iostream>
using namespace std;

class Student
{
private:
    string name;

public:
    void setName(string name)
    {
        this->name = name;
    }

    void display()
    {
        cout << "Name : " << this->name << endl;
    }
};

int main()
{
    Student s;

    s.setName("Ritesh");
    s.display();

    return 0;
}
```

---

# How `this` Works

```cpp
class Student
{
    int rollNo;

public:
    void setRollNo(int rollNo)
    {
        this->rollNo = rollNo;
    }
};
```

Here:

```cpp
this->rollNo = rollNo;
```

means:

```text
Current Object's rollNo = Function Parameter rollNo
```

---

# Uses of `this` Keyword

## 1. Resolve Variable Name Conflict

```cpp
#include <iostream>
using namespace std;

class Student
{
private:
    string name;

public:
    void setName(string name)
    {
        this->name = name;
    }

    void display()
    {
        cout << name;
    }
};

int main()
{
    Student s;

    s.setName("Ritesh");
    s.display();
}
```

---

## 2. Access Current Object

```cpp
#include <iostream>
using namespace std;

class Student
{
public:
    void showAddress()
    {
        cout << this << endl;
    }
};

int main()
{
    Student s1, s2;

    s1.showAddress();
    s2.showAddress();
}
```

Output:

```text
0x61ff08
0x61ff00
```

Each object has a different address.

---

## 3. Return Current Object

```cpp
#include <iostream>
using namespace std;

class Student
{
private:
    int marks;

public:
    Student* setMarks(int m)
    {
        marks = m;
        return this;
    }

    void display()
    {
        cout << marks << endl;
    }
};

int main()
{
    Student s;

    s.setMarks(90)->display();
}
```

---

## 4. Method Chaining

```cpp
#include <iostream>
using namespace std;

class Student
{
private:
    string name;
    int age;

public:
    Student& setName(string n)
    {
        name = n;
        return *this;
    }

    Student& setAge(int a)
    {
        age = a;
        return *this;
    }

    void display()
    {
        cout << name << " " << age << endl;
    }
};

int main()
{
    Student s;

    s.setName("Ritesh")
     .setAge(20)
     .display();
}
```

Output

```text
Ritesh 20
```

---

## 5. Pass Current Object as Argument

```cpp
#include <iostream>
using namespace std;

class Student;

class Demo
{
public:
    void show(Student* obj);
};

class Student
{
private:
    int roll = 101;

public:
    friend class Demo;

    void sendObject(Demo d)
    {
        d.show(this);
    }
};

void Demo::show(Student* obj)
{
    cout << obj->roll;
}

int main()
{
    Student s;
    Demo d;

    s.sendObject(d);
}
```

---

# `this` Pointer in Constructor

```cpp
#include <iostream>
using namespace std;

class Student
{
private:
    string name;
    int rollNo;

public:
    Student(string name, int rollNo)
    {
        this->name = name;
        this->rollNo = rollNo;
    }

    void display()
    {
        cout << name << " " << rollNo;
    }
};

int main()
{
    Student s("Ritesh", 23);

    s.display();
}
```

---

# Important Points

* `this` is a pointer.
* Available only in non-static member functions.
* Automatically created by the compiler.
* Points to the current object.
* Cannot be modified.
* Used mainly to distinguish data members from local variables.

---

# Advantages

* Removes ambiguity between class members and parameters.
* Improves code readability.
* Enables method chaining.
* Makes object-oriented code cleaner.
* Allows returning the current object.

---

# Limitations

* Cannot be used in static member functions.
* Cannot be reassigned.
* Available only inside class member functions.

---

# Difference Between Without and With `this`

Without `this`

```cpp
void setRoll(int roll)
{
    roll = roll;
}
```

No value is assigned to the class member.

With `this`

```cpp
void setRoll(int roll)
{
    this->roll = roll;
}
```

Correctly assigns the parameter to the object's data member.

---

# Real-Life Example

Suppose two students exist:

```text
Student 1 → Ritesh
Student 2 → Rahul
```

When:

```cpp
s1.display();
```

`this` points to **Ritesh**.

When:

```cpp
s2.display();
```

`this` points to **Rahul**.

Thus, `this` always points to the object that calls the member function.

---

# Viva Questions

### 1. What is the `this` keyword?

`this` is a pointer that stores the address of the current object.

### 2. Is `this` a pointer or an object?

It is a pointer.

### 3. Can we use `this` in a static function?

No.

### 4. Why do we use `this`?

To refer to the current object and resolve naming conflicts.

### 5. Can `this` be modified?

No.

### 6. Can `this` be returned?

Yes.

### 7. Can `this` be passed as an argument?

Yes.

### 8. What does `this->name = name;` mean?

It assigns the function parameter `name` to the current object's data member `name`.

---

# Interview Questions

1. What is the `this` pointer?
2. Why is `this` required?
3. How does `this` resolve variable ambiguity?
4. Can `this` be used inside a constructor?
5. Why can't `this` be used in static functions?
6. Explain method chaining using `this`.
7. What is the difference between `this` and `*this`?
8. Can `this` be `nullptr`?
9. Explain returning `*this`.
10. Give a real-life example of the `this` pointer.

---

# Summary

* `this` is a special pointer available in every non-static member function.
* It points to the current object.
* It is mainly used to resolve naming conflicts, return the current object, support method chaining, and pass the current object as an argument.
* `this` cannot be used inside static member functions because they do not belong to any specific object.
