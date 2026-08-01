
# What is an Interface in Java?

## Definition

An **interface** in Java is a blueprint that defines a **contract** for classes.

It contains **method declarations** (without implementation by default) that a class must implement. A class uses the `implements` keyword to implement an interface.

Unlike an abstract class, an interface is primarily used to define **what a class should do**, not **how it should do it**.

> **One-line Definition (Interview)**
>
> **An interface is a blueprint that contains method declarations and constants, which implementing classes must provide implementations for.**

---

# Why Do We Need an Interface?

- To achieve **100% abstraction** (before Java 8).
- To support **multiple inheritance**.
- To define a common contract for unrelated classes.
- To achieve **loose coupling**.
- To make applications more flexible and maintainable.

---

# Syntax

```java
interface Animal {

    void sound();
}
```

A class implements the interface:

```java
class Dog implements Animal {

    @Override
    public void sound() {
        System.out.println("Dog Barks");
    }
}
```

---

# Example

```java
interface Animal {

    void sound();
}

class Dog implements Animal {

    @Override
    public void sound() {
        System.out.println("Dog Barks");
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
Dog Barks
```

---

# Explanation

### Step 1

Create an interface.

```java
interface Animal {

    void sound();
}
```

Here,

```java
void sound();
```

is an **abstract method**.

---

### Step 2

Implement the interface.

```java
class Dog implements Animal
```

The `implements` keyword is used instead of `extends`.

---

### Step 3

Implement all abstract methods.

```java
@Override
public void sound() {
    System.out.println("Dog Barks");
}
```

If `Dog` does not implement `sound()`, it must also be declared `abstract`.

---

### Step 4

Create the object.

```java
Animal obj = new Dog();
```

This is an example of **Runtime Polymorphism**.

---

# Characteristics of an Interface

- Cannot be instantiated.
- Uses the `interface` keyword.
- Implemented using `implements`.
- Supports multiple inheritance.
- Can contain abstract methods.
- Can contain default and static methods (Java 8+).
- Can contain private methods (Java 9+).
- Variables are implicitly `public static final`.

---

# Interface Variables

Every variable declared inside an interface is automatically:

- `public`
- `static`
- `final`

Example:

```java
interface Demo {

    int MAX = 100;
}
```

Java treats it as:

```java
public static final int MAX = 100;
```

Since it is `final`, its value cannot be changed.

---

# Interface Methods

### Before Java 8

Methods were implicitly:

```java
public abstract
```

Example:

```java
interface Animal {

    void sound();
}
```

Equivalent to:

```java
public abstract void sound();
```

---

### Since Java 8

Interfaces can also contain:

- **Default methods**
- **Static methods**

```java
interface Animal {

    default void eat() {
        System.out.println("Eating");
    }

    static void info() {
        System.out.println("Animal Interface");
    }
}
```

---

### Since Java 9

Interfaces can also contain **private methods**.

```java
interface Demo {

    private void helper() {
        System.out.println("Helper Method");
    }
}
```

---

# Real-Life Example 🔌

Think of a **mobile charger**.

A charger specifies:

- Voltage
- Pin design
- Power output

It tells manufacturers **what standards must be followed**, but **not how the internal circuitry should be built**.

Similarly:

An interface defines **what methods must exist**, while each class decides **how to implement them**.

---

# Interface vs Abstract Class

| Interface | Abstract Class |
|-----------|----------------|
| Uses `implements` | Uses `extends` |
| Supports multiple inheritance | Does not support multiple class inheritance |
| No constructors | Can have constructors |
| Variables are `public static final` | Can have any type of variables |
| Cannot maintain object state | Can maintain object state |
| Defines a contract | Provides partial implementation |

---

# Advantages of Interfaces

- Achieves abstraction.
- Supports multiple inheritance.
- Promotes loose coupling.
- Improves flexibility.
- Makes code easier to maintain and test.

---

# Quick Interview Revision

- Declared using the `interface` keyword.
- Implemented using `implements`.
- Cannot be instantiated.
- Supports multiple inheritance.
- Defines a contract that implementing classes must follow.

---

# Interview Follow-up Questions

## Can we create an object of an interface?

**No.**

```java
Animal obj = new Animal();   // ❌ Compile-time Error
```

---

## Can we create a reference of an interface?

**Yes.**

```java
Animal obj = new Dog();
```

This is the most common usage.

---

## Can an interface have constructors?

**No.**

Interfaces do not have constructors because they cannot be instantiated.

---

## Can an interface have implemented methods?

**Yes.**

Since Java 8:

- `default` methods
- `static` methods

Since Java 9:

- `private` methods

---

## Can a class implement multiple interfaces?

**Yes.**

```java
interface A {
    void show();
}

interface B {
    void display();
}

class Demo implements A, B {

    public void show() {
        System.out.println("Show");
    }

    public void display() {
        System.out.println("Display");
    }
}
```

Java supports **multiple inheritance through interfaces**.

---

# Easy Trick to Remember

```text
Interface

✔ Blueprint / Contract
✔ Cannot Create Objects
✔ Implemented using implements
✔ Supports Multiple Inheritance
```

### Mnemonic

> **"Interface Tells *What* to Do, Not *How* to Do It."**
