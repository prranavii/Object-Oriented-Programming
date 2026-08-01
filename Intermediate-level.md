# What is Method Overloading, and What are its Rules?

## Definition

**Method Overloading** is a feature in Java where **multiple methods in the same class have the same name but different parameter lists**.

It is an example of **Compile-Time (Static) Polymorphism** because the compiler decides which method to call based on the method signature.

> **One-line Definition (Interview)**
>
> **Method Overloading is the process of defining multiple methods with the same name but different parameter lists in the same class.**

---

# Why Do We Need Method Overloading?

- Improves code readability.
- Increases code reusability.
- Eliminates the need to create multiple method names for similar operations.
- Provides flexibility by allowing methods to accept different types or numbers of arguments.

---

# Example

```java
class Calculator {

    int add(int a, int b) {
        return a + b;
    }

    int add(int a, int b, int c) {
        return a + b + c;
    }

    double add(double a, double b) {
        return a + b;
    }

    public static void main(String[] args) {

        Calculator c = new Calculator();

        System.out.println(c.add(10, 20));
        System.out.println(c.add(10, 20, 30));
        System.out.println(c.add(10.5, 20.5));
    }
}
```

### Output

```text
30
60
31.0
```

---

# How Does Java Identify an Overloaded Method?

Java uses the **method signature**.

A method signature consists of:

- Method name
- Number of parameters
- Data type of parameters
- Order of parameters

**Return type is NOT part of the method signature.**

---

# Rules of Method Overloading

## Rule 1: Method Name Must Be the Same

```java
void display() { }

void display(int x) { }
```

✔ Valid

---

## Rule 2: Parameter List Must Be Different

The parameter list can differ by:

### Different Number of Parameters

```java
void add(int a, int b) { }

void add(int a, int b, int c) { }
```

✔ Valid

---

### Different Data Types

```java
void print(int x) { }

void print(String x) { }
```

✔ Valid

---

### Different Order of Parameters

```java
void display(int a, String b) { }

void display(String b, int a) { }
```

✔ Valid

---

## Rule 3: Changing Only the Return Type is NOT Allowed

```java
int add(int a, int b) {
    return a + b;
}

double add(int a, int b) {    // ❌ Compile-time Error
    return a + b;
}
```

**Reason:** The compiler cannot distinguish methods based only on the return type.

---

## Rule 4: Access Modifiers Can Be Different

```java
public void display() { }

private void display(int x) { }
```

✔ Valid

---

## Rule 5: Static Methods Can Be Overloaded

```java
class Demo {

    static void show() { }

    static void show(int x) { }
}
```

✔ Valid

---

## Rule 6: Constructors Can Be Overloaded

```java
class Student {

    Student() { }

    Student(String name) { }

    Student(String name, int age) { }
}
```

✔ Valid

---

# Invalid Example

```java
class Demo {

    int add(int a, int b) {
        return a + b;
    }

    double add(int a, int b) {    // ❌ Error
        return a + b;
    }
}
```

### Why?

Both methods have the **same name** and the **same parameter list**.

The return type alone cannot distinguish overloaded methods.

---

# Real-Life Example 🧮

Imagine a **calculator**.

It has one **Add** button.

Depending on the inputs, it performs different operations.

```text
add(5, 10)
add(5, 10, 15)
add(5.5, 2.5)
```

The **method name is the same**, but the **parameters are different**.

This is **Method Overloading**.

---

# Advantages of Method Overloading

- Improves readability.
- Makes code cleaner.
- Reduces the number of method names.
- Increases flexibility.
- Supports compile-time polymorphism.

---

# Method Overloading vs Method Overriding

| Method Overloading | Method Overriding |
|--------------------|-------------------|
| Same class | Parent and child classes |
| Different parameters | Same parameters |
| Compile-time polymorphism | Run-time polymorphism |
| Inheritance not required | Inheritance required |
| Static binding | Dynamic binding |

---

#
**Yes.**

Access modifiers do not affect method overloading.

---

# Easy Trick to Remember

```text
Method Overloading

✔ Same Method Name
✔ Different Parameters

Different means:
• Number
• Type
• Order

❌ Return Type Alone
```

# What is Method Overriding, and What are its Rules?

## Definition

**Method Overriding** is a feature in Java where a **child class provides its own implementation of a method that is already defined in the parent class**.

The child class method **overrides** the parent class method, allowing different behavior for the same method.

It is an example of **Run-Time (Dynamic) Polymorphism** because the method to execute is determined at runtime.

> **One-line Definition (Interview)**
>
> **Method Overriding is the process in which a child class provides a new implementation of an inherited method with the same signature as the parent class.**

---

# Why Do We Need Method Overriding?

- To provide a specialized implementation in the child class.
- To achieve **Run-Time Polymorphism**.
- To improve flexibility and extensibility.
- To allow child classes to modify inherited behavior.

---

# Example

```java
class Animal {

    void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {

    @Override
    void sound() {
        System.out.println("Dog barks");
    }
}

public class Main {

    public static void main(String[] args) {

        Animal obj = new Dog();

        obj.sound();
    }
}
```

### Output

```text
Dog barks
```

---

# How Does It Work?

```java
Animal obj = new Dog();
```

- **Reference Type:** `Animal`
- **Object Type:** `Dog`

When:

```java
obj.sound();
```

Java checks the **actual object type (`Dog`)**, not the reference type (`Animal`).

Therefore:

```text
Dog barks
```

This is called **Dynamic Method Dispatch**.

---

# Rules of Method Overriding

## Rule 1: Inheritance is Required

Method overriding is only possible when one class inherits another.

```java
class Animal { }

class Dog extends Animal { }
```

✔ Valid

---

## Rule 2: Method Name Must Be the Same

```java
class Parent {

    void display() { }
}

class Child extends Parent {

    @Override
    void display() { }
}
```

✔ Valid

---

## Rule 3: Parameter List Must Be the Same

```java
class Parent {

    void show(int x) { }
}

class Child extends Parent {

    @Override
    void show(int x) { }
}
```

✔ Valid

Changing the parameters creates **Method Overloading**, not overriding.

---

## Rule 4: Return Type Must Be the Same (or Covariant)

### Same Return Type

```java
class Parent {

    int getValue() {
        return 10;
    }
}

class Child extends Parent {

    @Override
    int getValue() {
        return 20;
    }
}
```

✔ Valid

---

### Covariant Return Type

A child class can return a subclass of the parent's return type.

```java
class Animal { }

class Dog extends Animal { }

class Parent {

    Animal getAnimal() {
        return new Animal();
    }
}

class Child extends Parent {

    @Override
    Dog getAnimal() {
        return new Dog();
    }
}
```

✔ Valid

---

## Rule 5: Access Modifier Cannot Be More Restrictive

### Valid

```java
class Parent {

    protected void display() { }
}

class Child extends Parent {

    @Override
    public void display() { }
}
```

✔ Allowed because access is increased.

---

### Invalid

```java
class Parent {

    public void display() { }
}

class Child extends Parent {

    @Override
    private void display() { }   // ❌ Error
}
```

A child class cannot reduce the visibility of an inherited method.

---

## Rule 6: `final` Methods Cannot Be Overridden

```java
class Parent {

    final void display() { }
}

class Child extends Parent {

    // void display() { }    ❌ Error
}
```

---

## Rule 7: `static` Methods Cannot Be Overridden

Static methods belong to the class, not the object.

```java
class Parent {

    static void display() {
        System.out.println("Parent");
    }
}

class Child extends Parent {

    static void display() {
        System.out.println("Child");
    }
}
```

This is **Method Hiding**, **not** Method Overriding.

---

## Rule 8: Constructors Cannot Be Overridden

Constructors are not inherited.

```java
class Parent {

    Parent() { }
}

class Child extends Parent {

    Child() { }
}
```

✔ Constructors can be **overloaded**, but **not overridden**.

---

## Rule 9: Private Methods Cannot Be Overridden

Private methods are not inherited.

```java
class Parent {

    private void display() { }
}

class Child extends Parent {

    void display() { }
}
```

This is **not** overriding because the child cannot inherit a private method.

---

## Rule 10: Use `@Override` Annotation

```java
class Parent {

    void display() { }
}

class Child extends Parent {

    @Override
    void display() {
        System.out.println("Overridden");
    }
}
```

The `@Override` annotation is optional but **strongly recommended** because the compiler checks that a method is actually being overridden.

---

# Real-Life Example 🚗

Imagine a vehicle.

```text
Vehicle
   │
   ├── start()
   │
Car
   │
   └── start() → Starts with a key or push button

Bike
   │
   └── start() → Starts with a self-start or kick
```

The method name is the same (`start()`), but each vehicle provides its own implementation.

This is **Method Overriding**.

---

# Method Overriding vs Method Overloading

| Method Overriding | Method Overloading |
|-------------------|--------------------|
| Parent & Child classes | Same class |
| Same method name | Same method name |
| Same parameters | Different parameters |
| Run-time polymorphism | Compile-time polymorphism |
| Inheritance required | Inheritance not required |
| Dynamic binding | Static binding |

---

# Advantages of Method Overriding

- Achieves Run-Time Polymorphism.
- Allows specialized behavior in child classes.
- Makes code more flexible and extensible.
- Supports the Open/Closed Principle (open for extension, closed for modification).

---

# Quick Interview Revision

- Inheritance is required.
- Method name must be the same.
- Parameters must be the same.
- Return type must be the same or covariant.
- Cannot reduce access level.
- `final`, `static`, `private`, and constructors cannot be overridden.
- Achieves Run-Time Polymorphism.

---

# Can Methods be Overloaded by Changing Only the Return Type?

## Answer

**No.**

In Java, **methods cannot be overloaded by changing only the return type**.

For method overloading to occur, the **parameter list must be different** (number, type, or order of parameters).

> **One-line Answer (Interview)**
>
> **No. Java does not allow method overloading by changing only the return type because the compiler identifies overloaded methods using their method signature, which does not include the return type.**

---

# Why is it Not Allowed?

Java identifies overloaded methods using the **method signature**.

A method signature consists of:

- Method name
- Number of parameters
- Data types of parameters
- Order of parameters

**The return type is NOT part of the method signature.**

---

# Invalid Example

```java
class Calculator {

    int add(int a, int b) {
        return a + b;
    }

    double add(int a, int b) {    // ❌ Compile-time Error
        return a + b;
    }
}
```

### Compile-Time Error

```text
method add(int,int) is already defined in class Calculator
```

---

# Why Does the Compiler Get Confused?

Consider the following call:

```java
Calculator c = new Calculator();

c.add(10, 20);
```

Which method should Java call?

```java
int add(int, int)
```

or

```java
double add(int, int)
```

Both methods have:

- Same method name ✔
- Same parameter types ✔

The compiler decides **which method to call before looking at the return value**, so it cannot distinguish between these methods.

---

# Correct Way to Overload Methods

## 1. Different Number of Parameters

```java
class Calculator {

    int add(int a, int b) {
        return a + b;
    }

    int add(int a, int b, int c) {
        return a + b + c;
    }
}
```

✔ Valid

---

## 2. Different Parameter Types

```java
class Calculator {

    void display(int x) {
        System.out.println(x);
    }

    void display(String x) {
        System.out.println(x);
    }
}
```

✔ Valid

---

## 3. Different Order of Parameters

```java
class Demo {

    void show(int age, String name) { }

    void show(String name, int age) { }
}
```

✔ Valid

---

# Method Signature

```java
int add(int a, int b)
```

The **method signature** is:

```text
add(int, int)
```

Notice that the return type (`int`) is **not included**.

---

# Real-Life Example 🏦

Imagine a bank has two employees with the **same employee ID**.

```text
Employee ID: 101
Employee ID: 101
```

The bank cannot identify which employee is which.

Similarly, Java identifies methods using their **method signature**.

If two methods have the same signature, the compiler treats them as duplicates, regardless of their return types.

---

# Valid vs Invalid

### ❌ Invalid

```java
class Demo {

    int square(int x) {
        return x * x;
    }

    double square(int x) {
        return x * x;
    }
}
```

---

### ✔ Valid

```java
class Demo {

    int square(int x) {
        return x * x;
    }

    double square(double x) {
        return x * x;
    }
}
```

---

# Quick Interview Revision

- Return type is **not** part of the method signature.
- Changing only the return type does **not** overload a method.
- Parameter list **must** be different.

---

# Interview Follow-up Questions

## Is the return type part of the method signature?

**No.**

The method signature includes only:

- Method name
- Parameter types
- Number of parameters
- Order of parameters

---

## How can we overload a method?

By changing the:

- Number of parameters
- Data types of parameters
- Order of parameters

---

## Why does Java not consider the return type?

Because the compiler selects the method to invoke **before** it knows or uses the returned value. Therefore, methods with the same name and parameter list would be ambiguous if only the return type differed.

---

# Easy Trick to Remember

```text
Method Overloading

✔ Same Name
✔ Different Parameters

❌ Same Name
❌ Same Parameters
❌ Different Return Type Only
```

### Mnemonic

> **"Return Type Doesn't Count — Parameters Decide."**

# 29. Can Constructors be Overloaded?

## Answer

**Yes.**

Java allows **constructor overloading**, which means a class can have **multiple constructors with the same name (the class name) but different parameter lists**.

Each constructor is used to initialize objects in different ways.

> **One-line Answer (Interview)**
>
> **Yes. Constructors can be overloaded by defining multiple constructors with different parameter lists in the same class.**

---

# Why Do We Need Constructor Overloading?

Constructor overloading provides multiple ways to create an object.

For example, a `Student` object can be created:

- Without any information.
- With only a name.
- With a name and age.
- With a name, age, and course.

Instead of creating different constructor names (which Java doesn't allow), we overload constructors.

---

# Example

```java
class Student {

    String name;
    int age;

    // Default Constructor
    Student() {
        name = "Unknown";
        age = 0;
    }

    // Parameterized Constructor
    Student(String name) {
        this.name = name;
        age = 0;
    }

    // Parameterized Constructor
    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    void display() {
        System.out.println(name + " " + age);
    }

    public static void main(String[] args) {

        Student s1 = new Student();
        Student s2 = new Student("Alice");
        Student s3 = new Student("Bob", 21);

        s1.display();
        s2.display();
        s3.display();
    }
}
```

### Output

```text
Unknown 0
Alice 0
Bob 21
```

---

# How Does Java Decide Which Constructor to Call?

Java matches the constructor based on the **arguments passed during object creation**.

```java
new Student();
```

Calls:

```java
Student()
```

---

```java
new Student("Alice");
```

Calls:

```java
Student(String name)
```

---

```java
new Student("Bob", 21);
```

Calls:

```java
Student(String name, int age)
```

The compiler selects the appropriate constructor at **compile time**.

---

# Rules of Constructor Overloading

## Rule 1: Constructor Name Must Be the Same as the Class Name

```java
class Student {

    Student() { }

    Student(String name) { }
}
```

✔ Valid

---

## Rule 2: Parameter List Must Be Different

Constructors can differ by:

- Number of parameters
- Data types
- Order of parameters

### Different Number of Parameters

```java
Student() { }

Student(String name) { }
```

✔ Valid

---

### Different Data Types

```java
Student(int age) { }

Student(String name) { }
```

✔ Valid

---

### Different Order of Parameters

```java
Student(String name, int age) { }

Student(int age, String name) { }
```

✔ Valid

---

## Rule 3: Return Type is Not Allowed

Constructors **do not have a return type**, not even `void`.

```java
class Student {

    void Student() { }    // ❌ Not a constructor, it's a method
}
```

---

## Rule 4: Constructors Cannot Be Overloaded by Changing Only the Access Modifier

```java
class Student {

    public Student() { }

    private Student() { }    // ❌ Compile-time Error
}
```

Both constructors have the **same parameter list**, so changing only the access modifier is not enough.

---

# Constructor Overloading Using `this()`

One constructor can call another constructor in the same class using `this()`.

```java
class Student {

    String name;
    int age;

    Student() {
        this("Unknown", 0);
    }

    Student(String name) {
        this(name, 0);
    }

    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    void display() {
        System.out.println(name + " " + age);
    }

    public static void main(String[] args) {

        Student s1 = new Student();
        Student s2 = new Student("Alice");
        Student s3 = new Student("Bob", 21);

        s1.display();
        s2.display();
        s3.display();
    }
}
```

### Output

```text
Unknown 0
Alice 0
Bob 21
```

### Benefits of `this()`

- Reduces code duplication.
- Makes constructors easier to maintain.
- Ensures common initialization logic is written only once.

---

# Constructor Overloading vs Method Overloading

| Constructor Overloading | Method Overloading |
|--------------------------|--------------------|
| Constructor name is the class name | Method can have any valid name |
| No return type | Has a return type |
| Called automatically during object creation | Called explicitly using an object or class name |
| Used to initialize objects | Used to perform operations |
| Parameter list must be different | Parameter list must be different |

---

# Real-Life Example 🏠

Imagine buying a mobile phone.

You can purchase it in different ways:

```text
Phone()

→ Default phone

Phone("Samsung")

→ Phone with brand

Phone("Samsung", 256)

→ Phone with brand and storage

Phone("Samsung", 256, 45000)

→ Fully customized phone
```

The object is the same, but there are **multiple ways to initialize it**.

This is **Constructor Overloading**.

---

# Advantages

- Multiple ways to initialize objects.
- Improves flexibility.
- Makes code cleaner and more readable.
- Reduces duplicate initialization code when combined with `this()`.

---

# Quick Interview Revision

- Constructors **can** be overloaded.
- Constructor name must match the class name.
- Parameter list must be different.
- Constructors have **no return type**.
- `this()` can be used to call another constructor in the same class.

---

# Interview Follow-up Questions

## Can constructors be overridden?

**No.**

Constructors are **not inherited**, so they cannot be overridden.

---

## Can constructors be overloaded?

**Yes.**

By changing the:

- Number of parameters
- Data types
- Order of parameters

---

## Can a constructor call another constructor?

**Yes.**

Using the `this()` keyword.

```java
Student() {
    this("Unknown");
}
```

---

## Can we overload constructors by changing only the access modifier?

**No.**

The parameter list must be different.

---

## Can a constructor have a return type?

**No.**

If you specify a return type (even `void`), it becomes a regular method, not a constructor.

---

# Easy Trick to Remember

```text
Constructor Overloading

✔ Same Constructor Name (Class Name)
✔ Different Parameters

Different means:
• Number
• Type
• Order

❌ Return Type
❌ Access Modifier Only
```

### Mnemonic

> **"One Class, Many Ways to Create Objects."**

# 30. Can Constructors be Overridden?

## Answer

**No.**

Constructors **cannot be overridden** in Java because they are **not inherited** by child classes.

Method overriding requires **inheritance**, but constructors are not inherited. Therefore, overriding is not possible.

> **One-line Answer (Interview)**
>
> **No. Constructors cannot be overridden because they are not inherited by subclasses.**

---

# Why Can't Constructors Be Overridden?

To override a method:

- The method must be inherited.
- The child class must provide a new implementation of that inherited method.

Constructors do **not** satisfy the first condition because they are **never inherited**.

Every class has its own constructor, which is responsible for initializing objects of **that class only**.

---

# Example

```java
class Animal {

    Animal() {
        System.out.println("Animal Constructor");
    }
}

class Dog extends Animal {

    Dog() {
        System.out.println("Dog Constructor");
    }

    public static void main(String[] args) {

        Dog d = new Dog();
    }
}
```

### Output

```text
Animal Constructor
Dog Constructor
```

---

# Explanation

When this statement executes:

```java
Dog d = new Dog();
```

Java performs the following steps:

1. Calls the parent constructor (`Animal()`).
2. Executes the child constructor (`Dog()`).

The parent constructor is **called**, **not overridden**.

This happens because Java automatically inserts:

```java
super();
```

as the first statement in every constructor (if you don't write it explicitly).

---

# Constructor Call Flow

```text
Dog()

        │
        ▼

super()

        │
        ▼

Animal()

        │
        ▼

Returns to Dog()

        │
        ▼

Dog Constructor Executes
```

---

# Incorrect Attempt

```java
class Parent {

    Parent() { }
}

class Child extends Parent {

    Parent() { }    // ❌ Compile-time Error
}
```

### Why?

A constructor's name **must exactly match its own class name**.

The constructor inside `Child` must be named:

```java
Child()
```

not

```java
Parent()
```

---

# Parent Constructor vs Method Overriding

### Constructor

```java
class Parent {

    Parent() {
        System.out.println("Parent");
    }
}

class Child extends Parent {

    Child() {
        System.out.println("Child");
    }
}
```

Constructors are **called** using `super()`, not overridden.

---

### Method

```java
class Parent {

    void display() {
        System.out.println("Parent");
    }
}

class Child extends Parent {

    @Override
    void display() {
        System.out.println("Child");
    }
}
```

Methods **can** be overridden because they are inherited.

---

# Constructor Overloading vs Constructor Overriding

| Constructor Overloading | Constructor Overriding |
|--------------------------|------------------------|
| ✅ Possible | ❌ Not Possible |
| Same class | Parent & Child |
| Different parameter lists | Not allowed |
| Multiple constructors | Constructors are not inherited |

---

# Real-Life Example 🏠

Imagine building a house.

- Every floor has its **own construction process**.
- The second floor **cannot replace** the construction process of the first floor.
- It simply **builds on top of it**.

Similarly:

- The child constructor does **not replace** the parent constructor.
- It calls the parent constructor first using `super()` and then performs its own initialization.

---

# Advantages of This Design

- Ensures proper initialization of parent class members.
- Maintains the object creation hierarchy.
- Prevents accidental replacement of parent initialization logic.

---

# Quick Interview Revision

- Constructors are **not inherited**.
- Overriding requires inheritance.
- Therefore, constructors **cannot be overridden**.
- Parent constructors are invoked using `super()`.

---

# Interview Follow-up Questions

## Can constructors be overloaded?

**Yes.**

A class can have multiple constructors with different parameter lists.

---

## Can constructors be inherited?

**No.**

Each class defines its own constructors.

---

## How is the parent constructor called?

Using:

```java
super();
```

If not written explicitly, Java inserts it automatically (provided the parent has an accessible no-argument constructor).

---

## Can we call a parent constructor explicitly?

**Yes.**

```java
class Parent {

    Parent(String name) {
        System.out.println(name);
    }
}

class Child extends Parent {

    Child() {
        super("Alice");
    }
}
```

---

# Easy Trick to Remember

```text
Constructors

✔ Can be Overloaded
✔ Can Call Parent using super()

❌ Cannot be Overridden
❌ Cannot be Inherited
```

### Mnemonic

> **"Constructors Create Objects, They Don't Participate in Overriding."**

# 31. Can Private Methods be Overloaded?

## Answer

**Yes.**

**Private methods can be overloaded** because method overloading occurs **within the same class**, and access modifiers do not affect overloading.

As long as the methods have the **same name** but **different parameter lists**, they can be overloaded—even if they are declared `private`.

> **One-line Answer (Interview)**
>
> **Yes. Private methods can be overloaded because overloading depends on the method signature, not the access modifier.**

---

# Why is it Allowed?

Method overloading depends on the **method signature**, which includes:

- Method name
- Number of parameters
- Data types of parameters
- Order of parameters

It **does not depend** on:

- Access modifiers (`private`, `protected`, `public`)
- Return type

Since all overloaded methods exist **inside the same class**, Java can distinguish them using their parameter lists.

---

# Example

```java
class Calculator {

    private void add() {
        System.out.println("No Parameters");
    }

    private void add(int a) {
        System.out.println("One Integer: " + a);
    }

    private void add(int a, int b) {
        System.out.println("Sum = " + (a + b));
    }

    public static void main(String[] args) {

        Calculator c = new Calculator();

        c.add();
        c.add(10);
        c.add(10, 20);
    }
}
```

### Output

```text
No Parameters
One Integer: 10
Sum = 30
```

---

# How Does Java Choose the Correct Method?

The compiler looks at the **arguments** passed during the method call.

```java
c.add();
```

Calls:

```java
add()
```

---

```java
c.add(10);
```

Calls:

```java
add(int)
```

---

```java
c.add(10, 20);
```

Calls:

```java
add(int, int)
```

This is decided at **compile time**, which is why method overloading is known as **Compile-Time Polymorphism**.

---

# Invalid Example

Changing only the return type is **not** overloading.

```java
class Demo {

    private int show(int x) {
        return x;
    }

    private double show(int x) {   // ❌ Compile-time Error
        return x;
    }
}
```

### Why?

Both methods have the **same name** and **same parameter list**.

The return type alone cannot distinguish overloaded methods.

---

# Private Methods: Overloading vs Overriding

## Overloading ✔

```java
class Parent {

    private void display() { }

    private void display(int x) { }
}
```

✔ Allowed because both methods are in the **same class**.

---

## Overriding ❌

```java
class Parent {

    private void display() {
        System.out.println("Parent");
    }
}

class Child extends Parent {

    void display() {
        System.out.println("Child");
    }
}
```

This is **not** method overriding.

**Reason:** Private methods are **not inherited**, so the child class cannot override them.

---

# Real-Life Example 🔒

Imagine a company.

A manager has several **private notes**.

They can organize those notes in different formats:

```text
note()
note(String title)
note(String title, int priority)
```

The notes are still **private**, but they can exist in multiple forms.

This is similar to **private method overloading**.

---

# Advantages

- Improves readability.
- Provides flexibility within the class.
- Reduces the need for multiple method names.
- Keeps implementation details hidden while supporting multiple input formats.

---

# Quick Interview Revision

- Private methods **can** be overloaded.
- Overloading depends on the **method signature**.
- Access modifiers do **not** affect overloading.
- Private methods **cannot** be overridden.

---

# Interview Follow-up Questions

## Can private methods be overloaded?

**Yes.**

They can have different parameter lists within the same class.

---

## Can private methods be overridden?

**No.**

Private methods are not inherited by child classes.

---

## Does the access modifier affect method overloading?

**No.**

Only the **method signature** matters.

---

## Can private static methods be overloaded?

**Yes.**

```java
class Demo {

    private static void show() { }

    private static void show(int x) { }
}
```

✔ Valid.

---

# Easy Trick to Remember

```text
Private Methods

✔ Can be Overloaded
❌ Cannot be Overridden
```

### Mnemonic

> **"Private Stays Inside the Class—So It Can Overload, But It Can't Be Overridden."**

# 32. Can Private Methods be Overridden?

## Answer

**No.**

**Private methods cannot be overridden** because they are **not inherited** by child classes.

Method overriding requires inheritance. Since private methods are accessible **only within the class in which they are declared**, the child class cannot inherit or override them.

> **One-line Answer (Interview)**
>
> **No. Private methods cannot be overridden because they are not inherited by subclasses.**

---

# Why Can't Private Methods be Overridden?

For method overriding to occur:

1. The method must be **inherited** by the child class.
2. The child class must provide its own implementation.

Private methods fail the first condition because they are **not visible outside their own class**.

```text
Parent Class
    │
private method
    │
    ✖ Not Inherited
    │
Child Class
```

Since the child class does not inherit the private method, there is nothing to override.

---

# Example

```java
class Parent {

    private void display() {
        System.out.println("Parent Display");
    }

    public void show() {
        display();      // Calls Parent's private method
    }
}

class Child extends Parent {

    void display() {
        System.out.println("Child Display");
    }

    public static void main(String[] args) {

        Child c = new Child();

        c.display();    // Calls Child's method
        c.show();       // Calls Parent's private method
    }
}
```

### Output

```text
Child Display
Parent Display
```

---

# Explanation

The `Child` class defines a method named `display()`.

```java
void display() {
    System.out.println("Child Display");
}
```

This **does not override** the parent's private method.

Instead, it creates a **new and unrelated method** with the same name.

When:

```java
c.display();
```

The child method is executed.

When:

```java
c.show();
```

The `show()` method belongs to `Parent`, so it internally calls the parent's private `display()`.

---

# Visual Representation

```text
Parent

private display()

        │
        │  (Not Inherited)
        ▼

Child

display()
```

These are **two separate methods**, not an overridden pair.

---

# Why Doesn't `@Override` Work?

```java
class Parent {

    private void display() { }
}

class Child extends Parent {

    @Override
    void display() { }      // ❌ Compile-time Error
}
```

### Error

```text
Method does not override or implement a method from a supertype
```

The compiler reports an error because there is **no inherited method** to override.

---

# Private Methods vs Public Methods

### Public Method (Overriding ✔)

```java
class Parent {

    public void display() {
        System.out.println("Parent");
    }
}

class Child extends Parent {

    @Override
    public void display() {
        System.out.println("Child");
    }
}
```

✔ This is method overriding.

---

### Private Method (Overriding ❌)

```java
class Parent {

    private void display() { }
}

class Child extends Parent {

    void display() { }
}
```

❌ This is **not** method overriding.

---

# Real-Life Example 🔒

Imagine a company.

The CEO has a **private diary**.

Employees cannot access or modify it.

If an employee creates their **own diary**, it is completely separate from the CEO's diary.

Similarly:

- Parent's private method → Only the parent class can access it.
- Child's method with the same name → A completely new method.

---

# Private Method vs Protected Method

| Feature | Private Method | Protected Method |
|---------|----------------|------------------|
| Inherited | ❌ No | ✅ Yes |
| Can be Overridden | ❌ No | ✅ Yes |
| Accessible in Child Class | ❌ No | ✅ Yes |

---

# Advantages of Private Methods

- Improves encapsulation.
- Hides implementation details.
- Prevents accidental overriding.
- Increases security.

---

# Can Final Methods be Overloaded?

## Answer

**Yes.**

A **final method can be overloaded** in Java because **method overloading depends on the method signature**, not on whether the method is declared `final`.

The `final` keyword only prevents **method overriding** in a subclass. It does **not** prevent creating multiple methods with the same name but different parameter lists in the same class.

> **One-line Answer (Interview)**
>
> **Yes. Final methods can be overloaded because overloading occurs within the same class and depends on different parameter lists, while `final` only prevents overriding.**

---

# Why is it Allowed?

Method overloading and method overriding are different concepts.

- **Method Overloading** → Same class, different parameter lists.
- **Method Overriding** → Parent and child classes, same method signature.

The `final` keyword only affects **overriding**, not overloading.

---

# Example

```java
class Calculator {

    final void add() {
        System.out.println("No Parameters");
    }

    final void add(int a) {
        System.out.println("One Number: " + a);
    }

    final void add(int a, int b) {
        System.out.println("Sum = " + (a + b));
    }

    public static void main(String[] args) {

        Calculator c = new Calculator();

        c.add();
        c.add(10);
        c.add(10, 20);
    }
}
```

### Output

```text
No Parameters
One Number: 10
Sum = 30
```

---

# Why Can't a Final Method be Overridden?

```java
class Parent {

    final void display() {
        System.out.println("Parent Display");
    }
}

class Child extends Parent {

    @Override
    void display() {      // ❌ Compile-time Error
        System.out.println("Child Display");
    }
}
```

### Error

```text
Cannot override the final method from Parent
```

A `final` method is considered complete and cannot be modified by subclasses.

---

# Overloading vs Overriding of Final Methods

### ✔ Final Method Overloading

```java
class Demo {

    final void show() { }

    final void show(int x) { }

    final void show(String msg) { }
}
```

**Result:** ✔ Valid

---

### ❌ Final Method Overriding

```java
class Parent {

    final void show() { }
}

class Child extends Parent {

    void show() { }     // ❌ Compile-time Error
}
```

**Result:** ❌ Invalid

---

# Real-Life Example 📚

Imagine a textbook.

The chapter **"Introduction"** is marked as **final**.

- Another author **cannot rewrite** that chapter. (No overriding.)
- The same author can write:
  - `Introduction()`
  - `Introduction(String topic)`
  - `Introduction(String topic, int page)`

These are different versions with different inputs, similar to **method overloading**.

---

# Advantages of Final Methods

- Protects important business logic.
- Prevents accidental overriding.
- Ensures consistent behavior in subclasses.
- Still allows flexibility through overloading.

---

# Final Method vs Normal Method

| Feature | Final Method | Normal Method |
|---------|--------------|---------------|
| Can be Overloaded | ✅ Yes | ✅ Yes |
| Can be Overridden | ❌ No | ✅ Yes |
| Inherited | ✅ Yes | ✅ Yes |

---

# Quick Interview Revision

- `final` methods **can** be overloaded.
- `final` methods **cannot** be overridden.
- Overloading depends on **different parameter lists**.
- `final` only restricts overriding.

---

# 34. Can Final Methods be Overridden?

## Answer

**No.**

A **final method cannot be overridden** in Java because the `final` keyword prevents a subclass from changing the implementation of that method.

When a method is declared as `final`, it becomes the **final implementation**, and all subclasses must use it as it is.

> **One-line Answer (Interview)**
>
> **No. Final methods cannot be overridden because the `final` keyword prevents subclasses from providing a new implementation.**

---

# Why Can't Final Methods be Overridden?

Method overriding allows a child class to provide its own implementation of a parent class method.

However, when a method is marked as `final`, Java locks its implementation to ensure that it cannot be modified by subclasses.

```text
Parent Class

final method()

        │
        │
        ✖ Cannot Override
        │
Child Class
```

This helps preserve important or sensitive business logic.

---

# Example

```java
class Parent {

    final void display() {
        System.out.println("Parent Display");
    }
}

class Child extends Parent {

    @Override
    void display() {      // ❌ Compile-time Error
        System.out.println("Child Display");
    }
}
```

### Compile-Time Error

```text
Cannot override the final method from Parent
```

---

# Valid Example

```java
class Parent {

    final void display() {
        System.out.println("Parent Display");
    }
}

class Child extends Parent {

    void show() {
        System.out.println("Child Method");
    }

    public static void main(String[] args) {

        Child obj = new Child();

        obj.display();   // Inherited final method
        obj.show();
    }
}
```

### Output

```text
Parent Display
Child Method
```

The child class **inherits** the `final` method and can use it, but **cannot modify it**.

---

# Why Do We Use Final Methods?

Suppose a banking application has a method that verifies a user's PIN.

```java
class BankAccount {

    final void verifyPIN() {
        System.out.println("PIN Verified");
    }
}
```

If subclasses were allowed to override this method, someone could bypass or weaken the security logic.

Using `final` ensures that the original implementation is always used.

---

# Final Method vs Normal Method

| Feature | Final Method | Normal Method |
|---------|--------------|---------------|
| Can be Overridden | ❌ No | ✅ Yes |
| Can be Overloaded | ✅ Yes | ✅ Yes |
| Inherited | ✅ Yes | ✅ Yes |
| Can Change Behavior in Child Class | ❌ No | ✅ Yes |

---

# Final Method vs Final Class

| Final Method | Final Class |
|--------------|-------------|
| Prevents method overriding | Prevents class inheritance |
| Child class can still inherit the class | No child class can extend it |

---

# Real-Life Example 🚦

Think of traffic rules.

A **red light means STOP**.

No driver can decide to change that rule.

Similarly, a `final` method defines behavior that **cannot be changed by subclasses**.

---

# Advantages of Final Methods

- Prevents accidental overriding.
- Protects critical business logic.
- Ensures consistent behavior across all subclasses.
- Improves code reliability and maintainability.

---

# Quick Interview Revision

- `final` methods **cannot** be overridden.
- They **can** be inherited.
- They **can** be overloaded.
- The `final` keyword protects the method implementation.

---

# 36. What is Method Hiding in Java?

## Definition

**Method Hiding** is a feature in Java where a **child class declares a static method with the same name and the same parameter list as a static method in the parent class**.

In this case, the child class **hides** the parent's static method instead of overriding it.

Method hiding occurs **only with static methods**.

> **One-line Definition (Interview)**
>
> **Method Hiding occurs when a child class defines a static method with the same signature as a static method in the parent class.**

---

# Why Does Method Hiding Happen?

Static methods belong to the **class**, not to objects.

Since they are resolved at **compile time**, Java cannot perform **runtime polymorphism** on them.

Therefore, when a child class defines a static method with the same signature, it **hides** the parent's method instead of overriding it.

---

# Example

```java
class Parent {

    static void display() {
        System.out.println("Parent Static Method");
    }
}

class Child extends Parent {

    static void display() {
        System.out.println("Child Static Method");
    }

    public static void main(String[] args) {

        Parent p = new Parent();
        Child c = new Child();

        p.display();
        c.display();
    }
}
```

### Output

```text
Parent Static Method
Child Static Method
```

---

# Method Hiding with Parent Reference

```java
class Parent {

    static void show() {
        System.out.println("Parent");
    }
}

class Child extends Parent {

    static void show() {
        System.out.println("Child");
    }

    public static void main(String[] args) {

        Parent obj = new Child();

        obj.show();
    }
}
```

### Output

```text
Parent
```

---

# Explanation

```java
Parent obj = new Child();
```

- **Reference Type:** `Parent`
- **Object Type:** `Child`

When calling:

```java
obj.show();
```

Java checks the **reference type**, not the object type, because `show()` is **static**.

Therefore, it executes:

```java
Parent.show();
```

This is called **Method Hiding**.

---

# Memory Representation

```text
Parent Class
-----------------
display()
-----------------

        ▲
        │
inherits
        │

Child Class
-----------------
display()
-----------------
```

The child class has its own static method.

It **does not replace** the parent's method.

Both methods exist independently.

---

# Method Hiding vs Method Overriding

| Method Hiding | Method Overriding |
|---------------|-------------------|
| Static methods | Instance methods |
| Compile-time binding | Runtime binding |
| Depends on reference type | Depends on object type |
| No runtime polymorphism | Supports runtime polymorphism |
| Parent method is hidden | Parent method is overridden |

---

# Method Hiding vs Method Overloading

| Method Hiding | Method Overloading |
|---------------|--------------------|
| Parent & Child classes | Same class |
| Same method name | Same method name |
| Same parameter list | Different parameter lists |
| Static methods | Any methods |
| Compile-time binding | Compile-time binding |

---

# Real-Life Example 🏫

Imagine a school.

The principal publishes a **school notice**.

Each classroom can publish its own notice with the same title.

When you look at the classroom notice board, you see the classroom's notice.

The principal's notice still exists—it has just been **hidden**, not replaced.

Similarly:

- Parent static method → School notice.
- Child static method → Classroom notice.

The child method hides the parent method.

---

# Advantages of Method Hiding

- Allows a subclass to define its own class-level behavior.
- Maintains separate implementations for parent and child classes.
- Useful when class-specific static functionality is needed.

---

# Quick Interview Revision

- Applies only to **static methods**.
- Same method name and same parameter list.
- Parent and child classes.
- Compile-time binding.
- Depends on **reference type**.
- Not runtime polymorphism.

---

# 37. Can the `main()` Method be Overloaded?

## Answer

**Yes.**

The `main()` method **can be overloaded** in Java because it is just like any other **static method**.

You can define multiple `main()` methods with different parameter lists. However, **the JVM always starts execution from the standard `main()` method**.

> **Standard Main Method**
>
> ```java
> public static void main(String[] args)
> ```

> **One-line Answer (Interview)**
>
> **Yes. The `main()` method can be overloaded, but the JVM invokes only the standard `public static void main(String[] args)` method.**

---

# Why is it Allowed?

Method overloading depends on:

- Same method name
- Different parameter lists

Since `main()` is a method, it follows the same overloading rules.

---

# Example

```java
class Demo {

    public static void main(String[] args) {

        System.out.println("Original Main");

        main(10);
        main("Java");
    }

    static void main(int x) {
        System.out.println("Integer Main: " + x);
    }

    static void main(String name) {
        System.out.println("String Main: " + name);
    }
}
```

### Output

```text
Original Main
Integer Main: 10
String Main: Java
```

---

# What Happens if the Standard `main()` is Missing?

```java
class Demo {

    static void main(int x) {
        System.out.println(x);
    }
}
```

### Result

```text
Error: Main method not found in class Demo
```

The JVM searches specifically for:

```java
public static void main(String[] args)
```

If it is not found, the program cannot start.

---

# Rules for Overloading `main()`

- Same method name (`main`)
- Different parameter list
- Standard `main()` must exist if the class is to be executed directly by the JVM

---

# Real-Life Example 🚪

Imagine a building.

The **main entrance** is the only entrance visitors use to enter.

Inside the building, there may be many other doors.

Similarly:

- Standard `main()` → Main entrance (used by the JVM)
- Overloaded `main()` methods → Internal doors (called manually from code)

---

# Advantages

- Useful for testing.
- Allows helper versions of `main()`.
- Demonstrates method overloading concepts.

---

# Quick Interview Revision

- `main()` **can** be overloaded.
- JVM calls only:
  ```java
  public static void main(String[] args)
  ```
- Other overloaded `main()` methods must be called explicitly.

---

# Interview Follow-up Questions

## Which `main()` method does the JVM execute?

Only:

```java
public static void main(String[] args)
```

---

## Can overloaded `main()` methods execute automatically?

**No.**

They must be called from the standard `main()` method or another method.

---

# Easy Trick to Remember

```text
main()

✔ Can be Overloaded

JVM Starts Only From

public static void main(String[] args)
```

### Mnemonic

> **"Many `main()` Methods, One JVM Entry Point."**

# 38. Can the `main()` Method be Overridden?

## Answer

**No.**

The `main()` method **cannot be overridden** because it is **static**.

Static methods belong to the **class**, not to objects. If a child class defines another `main()` method with the same signature, it **hides** the parent's `main()` method instead of overriding it.

> **One-line Answer (Interview)**
>
> **No. The `main()` method cannot be overridden because it is static. A child class defining its own `main()` method results in method hiding, not overriding.**

---

# Why Can't `main()` be Overridden?

The standard `main()` method is declared as:

```java
public static void main(String[] args)
```

Since it is **static**, it follows the rules of static methods:

- Static methods cannot be overridden.
- They can only be hidden.

---

# Example

```java
class Parent {

    public static void main(String[] args) {
        System.out.println("Parent Main");
    }
}

class Child extends Parent {

    public static void main(String[] args) {
        System.out.println("Child Main");
    }
}
```

---

# What Happens?

If you run:

```text
Parent
```

### Output

```text
Parent Main
```

If you run:

```text
Child
```

### Output

```text
Child Main
```

Each class has its **own** `main()` method.

The child's `main()` **does not override** the parent's `main()`.

---

# Explanation

Both methods exist independently.

```text
Parent Class

main()

        ▲
        │
inherits
        │

Child Class

main()
```

The child's method **hides** the parent's method.

---

# Method Hiding Example

```java
class Parent {

    static void show() {
        System.out.println("Parent");
    }
}

class Child extends Parent {

    static void show() {
        System.out.println("Child");
    }

    public static void main(String[] args) {

        Parent obj = new Child();

        obj.show();
    }
}
```

### Output

```text
Parent
```

This demonstrates **method hiding**, which is the same concept that applies to `main()`.

---

# `main()` Overloading vs Overriding

| Feature | Overloading | Overriding |
|---------|-------------|------------|
| Allowed? | ✅ Yes | ❌ No |
| Reason | Different parameter lists | `main()` is static |
| JVM Entry Point | Standard `main()` only | Not applicable |

---

# Real-Life Example 🏫

Think of a school.

Each classroom has its own notice board.

The notice board in one classroom does **not replace** the notice board in another classroom.

Similarly:

- Parent class has its own `main()`.
- Child class has its own `main()`.
- One does not override the other.

---

# Quick Interview Revision

- `main()` is **static**.
- Static methods **cannot** be overridden.
- Child `main()` methods **hide** parent `main()` methods.
- Each class can have its own entry point.

---

# Interview Follow-up Questions

## Can `main()` be overloaded?

**Yes.**

By changing the parameter list.

---

## Can `main()` be hidden?

**Yes.**

Because it is a static method.

---

## Which `main()` runs?

The `main()` of the class you execute.

Example:

```bash
java Parent
```

Runs `Parent.main()`.

```bash
java Child
```

Runs `Child.main()`.

---

# Easy Trick to Remember

```text
main()

✔ Can be Overloaded
✔ Can be Hidden
❌ Cannot be Overridden
```

### Mnemonic

> **"`main()` is Static → It Hides, It Doesn't Override."**

# 39. Can a Class be Both `abstract` and `final`?

## Answer

**No.**

A class **cannot** be declared as both **`abstract`** and **`final`** because these two keywords have **opposite meanings**.

- **`abstract`** means the class **must be inherited** so that its abstract methods can be implemented.
- **`final`** means the class **cannot be inherited**.

Since a class cannot be both inherited and not inherited at the same time, Java does not allow a class to be both `abstract` and `final`.

> **One-line Answer (Interview)**
>
> **No. A class cannot be both `abstract` and `final` because `abstract` requires inheritance, while `final` prevents inheritance.**

---

# Why is it Not Allowed?

### `abstract` Class

An abstract class is **incomplete**.

It is designed to be **extended** by another class.

```java
abstract class Animal {

    abstract void sound();
}
```

---

### `final` Class

A final class is **complete**.

It **cannot be extended**.

```java
final class Animal { }
```

---

Combining both:

```java
abstract final class Animal { }   // ❌ Compile-time Error
```

creates a contradiction.

- `abstract` → "Please inherit me."
- `final` → "No one can inherit me."

---

# Example

```java
abstract final class Animal {

    abstract void sound();
}
```

### Compile-Time Error

```text
Illegal combination of modifiers: abstract and final
```

---

# Visual Representation

```text
abstract
     │
     ▼
Must Be Inherited
```

```text
final
     │
     ▼
Cannot Be Inherited
```

```text
abstract + final

Must Be Inherited
        +
Cannot Be Inherited

❌ Contradiction
```

---

# Real-Life Example 🚪

Imagine a door with two instructions:

```text
Door 1:
"Please Enter"

Door 2:
"Do Not Enter"
```

Now imagine a single door displaying both messages:

```text
Please Enter
Do Not Enter
```

This is contradictory.

Similarly:

- `abstract` → "Subclass me."
- `final` → "Don't subclass me."

Therefore, Java does not allow both together.

---

# Abstract Class vs Final Class

| Abstract Class | Final Class |
|----------------|-------------|
| Can be inherited | Cannot be inherited |
| May contain abstract methods | Cannot contain abstract methods (since it cannot be extended) |
| Used as a base class | Used to prevent inheritance |
| Incomplete implementation | Complete implementation |

---

# Advantages

### Abstract Class

- Supports abstraction.
- Encourages code reuse.
- Provides a common base for subclasses.

### Final Class

- Prevents inheritance.
- Protects implementation.
- Improves security and immutability.

---

# Quick Interview Revision

- `abstract` → Must be inherited.
- `final` → Cannot be inherited.
- `abstract + final` → ❌ Not allowed.

---

# Interview Follow-up Questions

## Can an abstract class have final methods?

**Yes.**

A final method can exist in an abstract class.

```java
abstract class Animal {

    final void eat() {
        System.out.println("Eating");
    }

    abstract void sound();
}
```

Here:

- `eat()` cannot be overridden.
- `sound()` must be implemented by subclasses.

✔ Valid.

---

## Can an abstract method be final?

**No.**

An abstract method **must be overridden**, while a final method **cannot be overridden**.

```java
abstract class Animal {

    final abstract void sound();    // ❌ Compile-time Error
}
```

This is contradictory.

---

## Can a final class have abstract methods?

**No.**

Since a final class cannot be inherited, there is no subclass to implement the abstract methods.

---

# Easy Trick to Remember

```text
abstract → Must Extend

final → Cannot Extend

abstract + final

❌ Not Allowed
```

### Mnemonic

> **"`abstract` Wants Inheritance, `final` Stops Inheritance."**
