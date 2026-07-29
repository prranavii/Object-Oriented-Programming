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
