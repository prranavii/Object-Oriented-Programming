#  What is a Constructor in Java?

## Definition

A **constructor** is a special member of a class that is **automatically called when an object is created**. It is used to **initialize the object's state (instance variables)**.

Unlike methods, a constructor:

- Has the **same name as the class**.
- **Does not have a return type**, not even `void`.
- Is invoked automatically when an object is created using the `new` keyword.

> **One-line Definition (Interview)**
>
> **A constructor is a special member of a class used to initialize objects. It is automatically invoked when an object is created.**

---

## Why Do We Need Constructors?

- Initialize object data.
- Assign default or custom values to instance variables.
- Reduce repetitive initialization code.
- Ensure every object starts in a valid state.

---

## Syntax

```java
class ClassName {

    ClassName() {
        // Constructor
    }
}
```

---

# Example

```java
class Student {

    String name;
    int age;

    // Constructor
    Student() {
        name = "John";
        age = 20;
    }

    void display() {
        System.out.println(name);
        System.out.println(age);
    }
}

public class Main {

    public static void main(String[] args) {

        Student s = new Student();

        s.display();
    }
}
```

### Output

```text
John
20
```

---

# Explanation

### Step 1: Constructor Declaration

```java
Student() {
    name = "John";
    age = 20;
}
```

- The constructor has the **same name as the class** (`Student`).
- It initializes the object's instance variables.

---

### Step 2: Object Creation

```java
Student s = new Student();
```

When `new Student()` is executed:

1. Memory is allocated for the object.
2. The constructor is automatically called.
3. The instance variables are initialized.

---

### Step 3: Access the Object

```java
s.display();
```

Displays the initialized values.

---

# Characteristics of a Constructor

- Same name as the class.
- No return type.
- Called automatically during object creation.
- Can be overloaded.
- Cannot be overridden.
- Can have access modifiers (`public`, `private`, `protected`, or package-private).

---

# Types of Constructors

## 1. Default Constructor

A constructor **provided automatically by the Java compiler** if you do not write any constructor.

```java
class Student {

    String name;
    int age;
}
```

The compiler internally creates:

```java
Student() { }
```

---

## 2. No-Argument Constructor

A constructor written by the programmer that takes **no parameters**.

```java
class Student {

    Student() {
        System.out.println("Constructor Called");
    }
}
```

---

## 3. Parameterized Constructor

A constructor that accepts parameters to initialize an object with different values.

```java
class Student {

    String name;
    int age;

    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

public class Main {

    public static void main(String[] args) {

        Student s = new Student("Alice", 22);

        System.out.println(s.name);
        System.out.println(s.age);
    }
}
```

### Output

```text
Alice
22
```

---

# Real-Life Example 🏠

Imagine buying a new house.

When the house is built, it already has:

- Rooms
- Doors
- Windows

These initial settings are done **automatically before you move in**.

Similarly, when an object is created in Java, the **constructor initializes it automatically** before you use it.

---

# Constructor vs Method

| Constructor | Method |
|-------------|--------|
| Initializes an object | Performs an operation |
| Same name as the class | Can have any valid name |
| No return type | Must have a return type (or `void`) |
| Called automatically | Called explicitly |
| Executes once per object creation | Can be called multiple times |
| Cannot be overridden | Can be overridden |

---

# Advantages of Constructors

- Initializes objects automatically.
- Improves code readability.
- Avoids repetitive initialization code.
- Ensures objects are created in a valid state.

---

# Quick Interview Revision

- Constructor initializes an object.
- Same name as the class.
- No return type.
- Called automatically with `new`.
- Can be overloaded.
- Cannot be overridden.

---
