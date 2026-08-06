# 40. What is an Abstract Class?

## Definition

An **abstract class** is a class that **cannot be instantiated (objects cannot be created directly)**. It is designed to be **extended by subclasses** and is used to provide a common base for related classes.

An abstract class can contain:

- **Abstract methods** (methods without a body)
- **Concrete methods** (methods with a body)
- Variables
- Constructors
- Static methods
- Final methods

It is declared using the **`abstract`** keyword.

> **One-line Definition (Interview)** 
>
> **An abstract class is a class that cannot be instantiated and may contain both abstract and concrete methods.**

---

# Why Do We Need an Abstract Class?

- To achieve abstraction.
- To provide a common base class.
- To enforce common behavior in subclasses.
- To avoid code duplication.
- To support code reusability.

---

# Syntax

```java
abstract class Vehicle {

    abstract void start();

    void stop() {
        System.out.println("Vehicle Stopped");
    }
}
```

---

# Example

```java
abstract class Animal {

    // Abstract Method
    abstract void sound();

    // Concrete Method
    void eat() {
        System.out.println("Animal is eating.");
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

        Animal obj = new Dog();

        obj.sound();
        obj.eat();
    }
}
```

### Output

```text
Dog barks.
Animal is eating.
```

---

# Explanation

### Step 1: Create an Abstract Class

```java
abstract class Animal
```

The `abstract` keyword makes the class abstract.

An abstract class **cannot be instantiated**.

```java
Animal obj = new Animal();   // ❌ Compile-time Error
```

---

### Step 2: Declare an Abstract Method

```java
abstract void sound();
```

An abstract method:

- Has **no method body**.
- Must be implemented by the subclass.

---

### Step 3: Declare a Concrete Method

```java
void eat() {
    System.out.println("Animal is eating.");
}
```

Concrete methods already have an implementation and can be inherited as they are.

---

### Step 4: Implement the Abstract Method

```java
class Dog extends Animal {

    @Override
    void sound() {
        System.out.println("Dog barks.");
    }
}
```

The subclass provides the implementation of the abstract method.

---

### Step 5: Create the Object

```java
Animal obj = new Dog();
```

Although an object of `Animal` cannot be created, a **reference** of the abstract class can refer to an object of its subclass.

---

# Characteristics of an Abstract Class

- Cannot be instantiated.
- Can contain abstract and concrete methods.
- Can have constructors.
- Can have instance and static variables.
- Can have static and final methods.
- Can be inherited.
- May contain **zero or more abstract methods**.

> **Note:** A class can be abstract even if it has **no abstract methods**.

---

# Real-Life Example 🚗

Think of a **Vehicle**.

Every vehicle has:

- Start
- Stop

But **how a vehicle starts** depends on the type of vehicle.

- Car → Starts with a key or push button.
- Bike → Starts with a self-start or kick.
- Bus → Starts differently.

So the base class defines:

```java
abstract void start();
```

Each subclass provides its own implementation.

---

# Abstract Class vs Concrete Class

| Abstract Class | Concrete Class |
|----------------|----------------|
| Cannot create objects | Objects can be created |
| May contain abstract methods | Cannot contain abstract methods |
| Can contain concrete methods | Contains only concrete methods |
| Used as a base class | Used to create objects |

---

# Advantages of Abstract Classes

- Achieves abstraction.
- Reduces code duplication.
- Improves code reusability.
- Provides a common template for subclasses.
- Supports partial implementation.

---

# Quick Interview Revision

- Declared using the `abstract` keyword.
- Cannot be instantiated.
- Can contain both abstract and concrete methods.
- Must be extended by subclasses.
- Supports abstraction and code reuse.

---

# Interview Follow-up Questions

## Can we create an object of an abstract class?

**No.**

```java
Animal obj = new Animal();   // ❌ Error
```

---

## Can an abstract class have constructors?

**Yes.**

Constructors are called when a subclass object is created.

```java
abstract class Animal {

    Animal() {
        System.out.println("Animal Constructor");
    }
}
```

---

## Can an abstract class have static methods?

**Yes.**

```java
abstract class Animal {

    static void display() {
        System.out.println("Static Method");
    }
}
```

---

## Can an abstract class have final methods?

**Yes.**

```java
abstract class Animal {

    final void eat() {
        System.out.println("Eating");
    }
}
```

The method can be inherited but **cannot be overridden**.

---

## Can an abstract class have no abstract methods?

**Yes.**

```java
abstract class Animal {

    void eat() {
        System.out.println("Eating");
    }
}
```

A class can still be declared `abstract` to prevent object creation.

---

# Easy Trick to Remember

```text
Abstract Class

✔ Cannot Create Objects
✔ Can Have Abstract Methods
✔ Can Have Concrete Methods
✔ Can Be Extended
```

### Mnemonic

> **"Abstract Class = Incomplete Blueprint for Other Classes."**

# 41. Can an Abstract Class Have a Constructor?

## Answer

**Yes.**

An **abstract class can have a constructor** in Java.

Although an abstract class **cannot be instantiated directly**, its constructor is called **automatically when an object of its subclass is created**.

The constructor is mainly used to initialize the common data and behavior shared by all subclasses.

> **One-line Answer (Interview)**
>
> **Yes. An abstract class can have a constructor. It is executed when a subclass object is created to initialize the common members of the abstract class.**

---

# Why Does an Abstract Class Need a Constructor?

An abstract class cannot have its own object, but it can have:

- Instance variables
- Concrete methods
- Common initialization code

The constructor initializes these common members before the subclass constructor executes.

---

# Example

```java
abstract class Animal {

    Animal() {
        System.out.println("Animal Constructor");
    }

    abstract void sound();
}

class Dog extends Animal {

    Dog() {
        System.out.println("Dog Constructor");
    }

    @Override
    void sound() {
        System.out.println("Dog Barks");
    }

    public static void main(String[] args) {

        Dog obj = new Dog();
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
Dog obj = new Dog();
```

Java performs the following steps:

### Step 1

Memory is allocated for the `Dog` object.

↓

### Step 2

The constructor of the parent class (`Animal`) is called.

↓

### Step 3

The constructor of the child class (`Dog`) is executed.

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

Even though `Animal` is abstract, its constructor still runs.

---

# Why is This Useful?

Suppose every animal has a unique ID.

Instead of initializing it in every subclass, we initialize it once in the abstract class.

```java
abstract class Animal {

    int id;

    Animal() {
        id = 1001;
        System.out.println("Animal Initialized");
    }

    abstract void sound();
}

class Dog extends Animal {

    @Override
    void sound() {
        System.out.println("Dog Barks");
    }

    public static void main(String[] args) {

        Dog d = new Dog();

        System.out.println(d.id);
    }
}
```

### Output

```text
Animal Initialized
1001
```

The common initialization code is written only once.

---

# Can We Create an Object of an Abstract Class?

**No.**

```java
Animal obj = new Animal();   // ❌ Compile-time Error
```

Even though the class has a constructor, Java does not allow direct object creation.

The constructor is executed **only when a subclass object is created**.

---

# Can an Abstract Class Have a Parameterized Constructor?

**Yes.**

```java
abstract class Animal {

    Animal(String name) {
        System.out.println(name);
    }
}

class Dog extends Animal {

    Dog() {
        super("Dog");
    }
}
```

### Output

```text
Dog
```

The child class explicitly calls the parameterized constructor using `super()`.

---

# Real-Life Example 🏠

Imagine building a house.

Every house has:

- Foundation
- Electricity connection
- Water connection

These common tasks are completed **before** adding room-specific features.

Similarly:

- The abstract class constructor initializes the common part.
- The subclass constructor initializes the specific part.

---

# Abstract Class Constructor vs Normal Constructor

| Abstract Class Constructor | Normal Class Constructor |
|-----------------------------|--------------------------|
| Cannot create object directly | Creates object normally |
| Called by subclass constructor | Called when object is created |
| Initializes common members | Initializes object members |

---

# Advantages

- Initializes common data.
- Avoids code duplication.
- Improves code reusability.
- Ensures proper constructor chaining.

---

# Quick Interview Revision

- Abstract classes **can** have constructors.
- Constructors initialize common data.
- Constructors are called when a subclass object is created.
- Abstract classes **cannot** be instantiated directly.

---

# Interview Follow-up Questions

## Can an abstract class have a constructor?

**Yes.**

---

## Can we create an object of an abstract class if it has a constructor?

**No.**

The constructor executes only when a subclass object is created.

---

## Why do we use constructors in abstract classes?

To initialize common fields and perform common setup shared by all subclasses.

---

## Can an abstract class have multiple constructors?

**Yes.**

Like any normal class, it can have constructor overloading.

```java
abstract class Animal {

    Animal() { }

    Animal(String name) { }
}
```

---

## Is `super()` used to call an abstract class constructor?

**Yes.**

The subclass constructor calls the abstract class constructor using `super()` (explicitly or implicitly).

---

# Easy Trick to Remember

```text
Abstract Class

✔ Can Have Constructors
✔ Constructor Executes

❌ Cannot Create Object
```

### Mnemonic

> **"No Object, But Constructor Still Runs Through the Child."**
