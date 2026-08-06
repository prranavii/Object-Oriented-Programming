# Java OOP Interview Notes

---

# 1. What is Object-Oriented Programming (OOP) in Java?

## Definition
Object-Oriented Programming (OOP) is a programming paradigm that organizes software around **objects** rather than functions.

An **object** combines:
- **Data (State)** → Variables/Fields
- **Behavior** → Methods/Functions

OOP helps in building applications that are:
- Modular
- Reusable 
- Maintainable
- Scalable

### Example

```java
class Student {
    String name;          // State

    void study() {        // Behavior
        System.out.println(name + " is studying.");
    }
}

public class Main {
    public static void main(String[] args) {
        Student s = new Student();
        s.name = "John";
        s.study();
    }
}
```

---

# 2. What are the Four Pillars of OOP?

| Pillar | Meaning | Purpose |
|---------|----------|---------|
| **Encapsulation** | Protects data by wrapping it with methods | Protect |
| **Abstraction** | Hides implementation details | Hide |
| **Inheritance** | Allows one class to acquire properties of another | Reuse |
| **Polymorphism** | One interface, multiple implementations | Many Forms |

### Easy Mnemonic

- 🔒 **Encapsulation** → Protect
- 🎭 **Abstraction** → Hide
- 🧬 **Inheritance** → Reuse
- 🔄 **Polymorphism** → Many Forms

---

# 3. What is the difference between a Class and an Object?

| Class | Object |
|--------|--------|
| Blueprint or template | Real-world instance of a class |
| Does not occupy memory until objects are created | Occupies memory |
| Used to define properties and behaviors | Used to access properties and behaviors |
| Logical entity | Physical entity |

### Example

```java
class Car {
    String color;

    void drive() {
        System.out.println("Car is moving");
    }
}

public class Main {
    public static void main(String[] args) {
        Car c1 = new Car();   // Object
        c1.color = "Red";
        c1.drive();
    }
}
```

### Explanation

- **Class** → `Car`
- **Object** → `c1`

A **class** is a blueprint or template that defines the properties and behaviors of an object. An **object** is a real-world instance of that class.

### Real-Life Example 🏠

Imagine you want to build a house.

- First, you create a **blueprint (template)** that describes the design, number of rooms, doors, windows, etc. This blueprint is the **class**.
- Using the same blueprint, you build **10 different houses**. Each house can have a different **color**, **furniture**, or **interior design**, but they all follow the same blueprint. Each of these houses is an **object**.

**Therefore:**
- 📝 **Blueprint** → **Class**
- 🏠 **Each House** → **Object**

> **Remember:** A class is just a design; it does not exist physically until an object is created from it.

# 4. What are the State, Behavior, and Identity of an Object?

## Example

```java
class Car {

    // State (Instance Variables)
    String color;
    int speed;

    // Behavior (Method)
    void accelerate() {
        System.out.println("Car is accelerating");
    }

    public static void main(String[] args) {

        // Object Creation
        Car c1 = new Car();

        c1.color = "Red";
        c1.speed = 80;

        c1.accelerate();
    }
}
```

---

## Explanation

### **State**
The **state** of an object refers to the **data or values stored in its instance variables**.

In the above example:

- `color`
- `speed`

represent the **state** of the `Car` object.

---

### **Behavior**
The **behavior** of an object refers to the **actions it can perform**, which are defined using methods.

In the above example:

```java
accelerate()
```

is the behavior because it performs the action of accelerating the car.

---

### **Identity**
The **identity** of an object refers to its **unique existence in memory**.

In the above example:

```java
Car c1 = new Car();
```

- `c1` is the **reference variable** that refers to the `Car` object.
- The object created using `new Car()` has a unique identity (memory location).

Even if another object has the same values for `color` and `speed`, it will have a different identity because it occupies a different memory location.

---

# 5. What is encapsulation in Java? 

## Defination

**Encapsulation** is the process of wrapping data (variables) and methods (functions) into a single unit while restricting the direct access to the data. 

It is achieved by:
-Declaring variables as **private** 
-Providing public getter and setter methods to access and modifying the data.

## Why is Encapsulation Needed?

- Protects sensitive data.
- Prevents unauthorized access.
- Improves data security.
- Makes the code modular and maintainable.
- Allows controlled access to data.


## Example

```java
class Student {

    // Private data members
    private String name;
    private int age;

    // Setter Methods
    public void setName(String name) {
        this.name = name;
    }

    public void setAge(int age) {
        if (age > 0) {
            this.age = age;
        }
    }

    // Getter Methods
    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}

public class Main {

    public static void main(String[] args) {

        Student s = new Student();

        s.setName("John");
        s.setAge(20);

        System.out.println(s.getName());
        System.out.println(s.getAge());
    }
}
```

## Explanation

### Step 1: Make Data Private

```java
private String name;
private int age;
```

The variables cannot be accessed directly from outside the class.

❌ Invalid:

```java
Student s = new Student();
s.age = 20;      // Error
```

---

### Step 2: Provide Controlled Access

```java
public void setAge(int age) {
    if (age > 0) {
        this.age = age;
    }
}
```

The setter checks whether the age is valid before storing it.

This prevents invalid data from entering the object.

---

### Step 3: Read Data Using Getters

```java
System.out.println(s.getAge());
```

Instead of accessing the variable directly, we use a getter method.

---

## Real-Life Example 🏦

Think of an **ATM machine**.

- You **cannot directly access** the cash stored inside the ATM.
- You interact with it using options like:
  - Withdraw Money
  - Deposit Money
  - Check Balance

The ATM protects its internal data and allows only controlled operations.

Similarly, in Java:

- **Private variables** → Money inside the ATM.
- **Getter/Setter methods** → ATM buttons.
- **User** → Program accessing the object.

---

## Advantages of Encapsulation

- ✅ Data Hiding
- ✅ Better Security
- ✅ Controlled Access
- ✅ Easy Maintenance
- ✅ Improved Reusability
- ✅ Better Flexibility

---

# 6. What is Abstraction in Java?

## Definition

**Abstraction** is the process of **hiding the implementation details** and **showing only the essential features** of an object.

In Java, abstraction is achieved using:
- **Abstract classes (0–100% abstraction)**
- **Interfaces (100% abstraction, conceptually)**

> **One-line Definition (Interview)**
>
> **Abstraction is the process of hiding implementation details and exposing only the necessary functionality to the user.**

---

## Why is Abstraction Needed?

- Hides complex implementation.
- Improves security.
- Reduces code complexity.
- Makes applications easier to maintain.
- Allows developers to focus on **what an object does** rather than **how it does it**.

---

## Example Using an Abstract Class

```java
abstract class Vehicle {

    // Abstract Method
    abstract void start();

    // Concrete Method
    void stop() {
        System.out.println("Vehicle stopped.");
    }
}

class Car extends Vehicle {

    @Override
    void start() {
        System.out.println("Car starts with a key or button.");
    }
}

public class Main {
    public static void main(String[] args) {

        Vehicle v = new Car();

        v.start();
        v.stop();
    }
}
```

---

## Explanation

### Step 1: Create an Abstract Class

```java
abstract class Vehicle
```

An **abstract class** cannot be instantiated directly.

❌ Invalid:

```java
Vehicle v = new Vehicle();   // Error
```

---

### Step 2: Declare an Abstract Method

```java
abstract void start();
```

An abstract method has **no implementation**.

It only tells **what** should happen, not **how** it should happen.

---

### Step 3: Implement the Method

```java
class Car extends Vehicle {

    @Override
    void start() {
        System.out.println("Car starts with a key or button.");
    }
}
```

The subclass provides the implementation of the abstract method.

---

### Step 4: Use the Object

```java
Vehicle v = new Car();
v.start();
```

The user only calls `start()` without knowing how it is implemented.

This is **abstraction**.

---

## Real-Life Example 🚗

Think about **driving a car**.

- You simply press the **Start** button.
- You **don't need to know** how the engine starts, how fuel is injected, or how the battery powers the ignition.

You only know **what to do**, not **how it works internally**.

Similarly, in Java:

- User calls `start()`.
- The implementation is hidden inside the class.

---

## Abstraction vs Encapsulation

| Encapsulation | Abstraction |
|---------------|-------------|
| Hides **data** | Hides **implementation** |
| Achieved using `private` variables and getters/setters | Achieved using abstract classes and interfaces |
| Focuses on **security** | Focuses on **simplicity** |
| Answers **"How to protect data?"** | Answers **"How to hide complexity?"** |

---

## Advantages of Abstraction

- ✅ Hides unnecessary details.
- ✅ Reduces complexity.
- ✅ Improves code readability.
- ✅ Makes code easier to maintain.
- ✅ Supports loose coupling.
- ✅ Improves scalability.

---

# 8. ⭐ What is Inheritance in Java?

## Definition

**Inheritance** is an OOP concept in which **one class (child/subclass) acquires the properties and behaviors of another class (parent/superclass).**

It promotes **code reusability** by allowing a child class to reuse the fields and methods of its parent class.

Inheritance is implemented using the **`extends`** keyword in Java.

> **One-line Definition (Interview)**
>
> **Inheritance is the mechanism by which one class acquires the properties and methods of another class, enabling code reusability and establishing an "IS-A" relationship.**

---

## Why is Inheritance Needed?

- Reuse existing code.
- Avoid code duplication.
- Improve maintainability.
- Support method overriding.
- Establish an **IS-A** relationship between classes.

---

## Example

```java
// Parent Class
class Animal {

    void eat() {
        System.out.println("Animal is eating.");
    }
}

// Child Class
class Dog extends Animal {

    void bark() {
        System.out.println("Dog is barking.");
    }
}

public class Main {

    public static void main(String[] args) {

        Dog d = new Dog();

        d.eat();    // Inherited from Animal
        d.bark();   // Defined in Dog
    }
}
```

---

## Explanation

### Step 1: Create a Parent Class

```java
class Animal {

    void eat() {
        System.out.println("Animal is eating.");
    }
}
```

The `Animal` class contains a method `eat()`.

---

### Step 2: Create a Child Class

```java
class Dog extends Animal {
```

The `Dog` class **extends** the `Animal` class.

This means `Dog` automatically inherits all the accessible members of `Animal`.

---

### Step 3: Add Child-Specific Behavior

```java
void bark() {
    System.out.println("Dog is barking.");
}
```

The child class can have its own methods in addition to the inherited ones.

---

### Step 4: Create an Object

```java
Dog d = new Dog();
```

The object `d` can access:

- `eat()` → inherited from `Animal`
- `bark()` → defined in `Dog`

Output:

```text
Animal is eating.
Dog is barking.
```

---

## Real-Life Example 👨‍👩‍👦

Think of a **Father** and a **Son**.

- The **Father** has certain properties like surname or family traits.
- The **Son** automatically inherits those properties and can also have his own unique qualities.

Similarly:

- **Parent Class** → Animal
- **Child Class** → Dog

The child inherits the parent's features and can also define new ones.

---

## Types of Inheritance in Java

| Type | Supported in Java? | Description |
|------|--------------------|-------------|
| **Single** | ✅ Yes | One child inherits from one parent. |
| **Multilevel** | ✅ Yes | A class inherits from another child class. |
| **Hierarchical** | ✅ Yes | Multiple child classes inherit from one parent. |
| **Multiple** | ❌ No (with classes) | One class cannot inherit from multiple classes. Achieved using interfaces. |
| **Hybrid** | ❌ No (with classes) | Combination of inheritance types. Achieved using interfaces. |

---

# 9. Types of Inheritance with Examples

### 1. Single Inheritance

```java
class Animal { }
class Dog extends Animal { }
```

```
Animal
   │
   ▼
 Dog
```

---

### 2. Multilevel Inheritance

```java
class Animal { }
class Dog extends Animal { }
class Puppy extends Dog { }
```

```
Animal
   │
   ▼
 Dog
   │
   ▼
Puppy
```

---

### 3. Hierarchical Inheritance

```java
class Animal { }
class Dog extends Animal { }
class Cat extends Animal { }
```

```
        Animal
       /      \
     Dog      Cat
```

---

### 4. Multiple Inheritance (Not Supported with Classes)

```java
class A { }
class B { }

// Not Allowed
class C extends A, B { }   // Compile-time Error
```

Java does **not** allow multiple inheritance with classes to avoid the **Diamond Problem**.

It can be achieved using **interfaces**.

---

## Advantages of Inheritance

- ✅ Code Reusability
- ✅ Reduces Code Duplication
- ✅ Easier Maintenance
- ✅ Supports Method Overriding
- ✅ Promotes Extensibility
- ✅ Represents Real-World Relationships

---

# 10.  What is Polymorphism in Java?

## Definition

**Polymorphism** is one of the four pillars of Object-Oriented Programming (OOP). The word **Polymorphism** comes from two Greek words:

- **Poly** → Many
- **Morph** → Forms

It means **"one interface, many forms."**

In Java, polymorphism allows the **same method or object reference to perform different behaviors depending on the situation.**

> **One-line Definition (Interview)**
>
> **Polymorphism is the ability of a method or object to take many forms, allowing the same interface to perform different actions.**

---

# Why is Polymorphism Needed?

- Enables code reusability.
- Improves flexibility.
- Makes code easier to maintain.
- Supports dynamic method invocation.
- Promotes loose coupling.

---

# Types of Polymorphism in Java

Java supports two types of polymorphism:

| Type | Also Known As | Achieved By | Binding |
|------|---------------|-------------|---------|
| **Compile-Time Polymorphism** | Static Polymorphism | Method Overloading | Early Binding |
| **Run-Time Polymorphism** | Dynamic Polymorphism | Method Overriding | Late Binding |

---

# 1. Compile-Time Polymorphism (Method Overloading)

Compile-time polymorphism occurs when **multiple methods have the same name but different parameter lists**.

The compiler decides which method to call based on the arguments passed.

## Example

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
}

public class Main {

    public static void main(String[] args) {

        Calculator c = new Calculator();

        System.out.println(c.add(5, 10));
        System.out.println(c.add(5, 10, 15));
        System.out.println(c.add(5.5, 2.5));
    }
}
```

### Output

```text
15
30
8.0
```

---

# 2. Run-Time Polymorphism (Method Overriding)

Run-time polymorphism occurs when a **child class overrides a method of its parent class**.

The method to execute is decided **at runtime** based on the actual object.

## Example

```java
class Animal {

    void sound() {
        System.out.println("Animal makes a sound.");
    }
}

class Dog extends Animal {

    @Override
    void sound() {
        System.out.println("Dog barks.");
    }
}

public class Main {

    public static void main(String[] args) {

        Animal a = new Dog();

        a.sound();
    }
}
```

### Output

```text
Dog barks.
```

Although the reference type is `Animal`, the object is `Dog`, so the overridden method in `Dog` is executed.

---

# Explanation

### Compile-Time Polymorphism

```java
c.add(5, 10);
```

The compiler selects the correct `add()` method based on the number and type of parameters.

This is called **Method Overloading**.

---

### Run-Time Polymorphism

```java
Animal a = new Dog();
a.sound();
```

- Reference Type → `Animal`
- Object Type → `Dog`

At runtime, Java calls the `Dog` implementation of `sound()`.

This is called **Method Overriding**.

---

# Real-Life Example 🚗

Imagine a **person driving different vehicles**.

The action is always:

```text
drive()
```

But the behavior changes depending on the vehicle.

- Car → Drive with a steering wheel.
- Bike → Ride using handlebars.
- Truck → Drive a heavy vehicle.

The **same action (`drive()`)** has **different implementations**.

This is polymorphism.

---

# Compile-Time vs Run-Time Polymorphism

| Compile-Time | Run-Time |
|--------------|----------|
| Method Overloading | Method Overriding |
| Decided by Compiler | Decided at Runtime |
| Static Binding | Dynamic Binding |
| Faster | Slightly Slower |
| Same Class | Parent and Child Classes |

---

# Advantages of Polymorphism

- ✅ Code Reusability
- ✅ Flexibility
- ✅ Easy Maintenance
- ✅ Supports Dynamic Method Dispatch
- ✅ Promotes Loose Coupling
- ✅ Makes Code Scalable

---

# Quick Interview Revision

- **Polymorphism = Many Forms**
- Allows one interface to perform different actions.
- Two types:
  1. Compile-Time Polymorphism → Method Overloading
  2. Run-Time Polymorphism → Method Overriding

---
# 11. What is the Difference Between Method Overloading and Method Overriding?

## Definition

### Method Overloading

**Method Overloading** is the process of defining **multiple methods with the same name but different parameter lists** in the **same class**.

It is an example of **Compile-Time (Static) Polymorphism**.

---

### Method Overriding

**Method Overriding** is the process where a **child class provides its own implementation** of a method that is already defined in its parent class.

It is an example of **Run-Time (Dynamic) Polymorphism**.

---

# Method Overloading Example

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
}

public class Main {

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

# Method Overriding Example

```java
class Animal {

    void sound() {
        System.out.println("Animal makes a sound.");
    }
}

class Dog extends Animal {

    @Override
    void sound() {
        System.out.println("Dog barks.");
    }
}

public class Main {

    public static void main(String[] args) {

        Animal a = new Dog();

        a.sound();
    }
}
```

### Output

```text
Dog barks.
```

---

# Difference Between Method Overloading and Method Overriding

| Feature | Method Overloading | Method Overriding |
|---------|--------------------|-------------------|
| Definition | Same method name with **different parameter lists** | Child class provides a **new implementation** of a parent class method |
| Polymorphism Type | Compile-Time (Static) | Run-Time (Dynamic) |
| Binding | Early Binding | Late Binding |
| Inheritance Required | ❌ No | ✅ Yes |
| Class | Usually within the **same class** | Parent and Child classes |
| Method Name | Same | Same |
| Parameters | **Must be different** | **Must be the same** |
| Return Type | Can be different (but not by return type alone) | Must be the same or covariant |
| Access Modifier | No restriction | Cannot reduce the visibility of the parent method |
| `static` Methods | Can be overloaded | Cannot be overridden (they are hidden) |
| `final` Methods | Can be overloaded | Cannot be overridden |
| Decision Made | At Compile Time | At Runtime |

---

# Key Rules

## Method Overloading

✔ Same method name

✔ Different parameter list:
- Number of parameters
- Type of parameters
- Order of parameters

❌ Changing only the return type is **not** method overloading.

Example:

```java
int sum(int a, int b)

double sum(double a, double b)

int sum(int a, int b, int c)
```

---

## Method Overriding

✔ Same method name

✔ Same parameter list

✔ Child class extends parent class

✔ Use the `@Override` annotation (recommended)

Example:

```java
class Animal {
    void sound() { }
}

class Dog extends Animal {

    @Override
    void sound() { }
}
```

---

# Real-Life Example 🚗

## Method Overloading

Imagine a **calculator**.

The **Add** button works differently based on the inputs:

- Add(2,3)
- Add(2,3,4)
- Add(2.5,4.5)

The operation name is the same, but the parameters differ.

---

## Method Overriding

Imagine a **remote control**.

Every TV has a **Power** button.

- Samsung TV → Turns on Samsung TV.
- Sony TV → Turns on Sony TV.
- LG TV → Turns on LG TV.

The button is the same, but each TV provides its own implementation.

---

# Quick Interview Revision

## Method Overloading

- Same method name
- Different parameters
- Same class
- Compile-Time Polymorphism
- No inheritance required

---

## Method Overriding

- Same method name
- Same parameters
- Parent & Child classes
- Run-Time Polymorphism
- Inheritance required

---

# Covariant Return Type in Java

## Definition

A **Covariant Return Type** allows an overridden method in a child class to return a **more specific type (subclass)** than the return type declared in the parent class.

This feature was introduced in **Java 5**.

> **One-line Definition (Interview)**
>
> **A covariant return type allows an overridden method to return the same type or a subclass of the parent's return type.**

---

## Syntax

```java
class Parent {

    Parent getObject() {
        return new Parent();
    }
}

class Child extends Parent {

    @Override
    Child getObject() {
        return new Child();
    }
}
```

---

## Example

```java
class Animal {

    Animal getObject() {
        System.out.println("Returning Animal");
        return new Animal();
    }
}

class Dog extends Animal {

    @Override
    Dog getObject() {
        System.out.println("Returning Dog");
        return new Dog();
    }
}

public class Main {

    public static void main(String[] args) {

        Animal a = new Dog();

        Animal obj = a.getObject();
    }
}
```

### Output

```text
Returning Dog
```

---

## Explanation

### Parent Class

```java
Animal getObject()
```

The parent method returns an object of type `Animal`.

---

### Child Class

```java
Dog getObject()
```

The child overrides the method and returns a `Dog` object.

Since **Dog is a subclass of Animal**, Java allows this.

This is called a **Covariant Return Type**.

---

## Visual Representation

```text
        Animal
           ▲
           │
          Dog
```

- Parent returns **Animal**
- Child returns **Dog**

✔ Allowed because **Dog IS-A Animal**.

---

## Valid Example

```java
class Vehicle { }

class Car extends Vehicle { }

class Parent {

    Vehicle create() {
        return new Vehicle();
    }
}

class Child extends Parent {

    @Override
    Car create() {
        return new Car();
    }
}
```

---

## Invalid Example

```java
class Animal { }

class Car { }

class Parent {

    Animal create() {
        return new Animal();
    }
}

class Child extends Parent {

    @Override
    Car create() {      // ❌ Compile-time Error
        return new Car();
    }
}
```

### Why?

`Car` is **not** a subclass of `Animal`.

The overridden method can return:
- ✅ The same return type
- ✅ A subclass of the return type
- ❌ An unrelated class

---

## Covariant Return Type Rules

- Applicable only in **Method Overriding**.
- Child class can return:
  - The **same** return type.
  - A **subclass** of the parent's return type.
- Works only with **reference types (objects)**.
- Does **not** work with primitive data types (`int`, `double`, `char`, etc.).

---

## Primitive Return Type Example

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

✔ Valid because the return type remains the same.

---

## Invalid Primitive Example

```java
class Parent {

    int getValue() {
        return 10;
    }
}

class Child extends Parent {

    @Override
    double getValue() {      // ❌ Compile-time Error
        return 20.5;
    }
}
```

Primitive return types **cannot** be changed while overriding.

---

## Advantages

- Eliminates unnecessary type casting.
- Improves code readability.
- Provides more specific return types.
- Enhances flexibility in method overriding.

---

## Quick Interview Revision

- **Only used in Method Overriding.**
- Child method can return:
  - ✔ Same return type.
  - ✔ Subclass of the parent's return type.
- Applicable only to **reference types**.
- Primitive return types cannot be changed.

---

## Interview Questions

### What is a covariant return type?

A covariant return type allows an overridden method to return a **more specific (subclass)** return type than the parent method.

---

### Does it work with primitive data types?

**No.** It works only with **reference types (objects)**.

---

### Is a subclass return type mandatory?

**No.** The child method can return:
- The **same** return type.
- A **subclass** of the parent's return type.

---

## Easy Trick to Remember

```text
Parent Return Type
        │
        ▼
     Animal
        ▲
        │
      Dog

✔ Allowed
```

```text
Parent Return Type
        │
        ▼
     Animal

        Car

❌ Not Allowed
```

### Mnemonic

> **Same or Child → Allowed**  
> **Unrelated Type → Not Allowed**
