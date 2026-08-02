
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

# What Types of Methods Can an Interface Contain in Modern Java?

## Answer

In modern Java (Java 8 and Java 9+), an interface can contain the following types of methods:

1. **Abstract Methods**
2. **Default Methods** (Java 8+)
3. **Static Methods** (Java 8+)
4. **Private Methods** (Java 9+)
5. **Private Static Methods** (Java 9+)

> **One-line Answer (Interview)**
>
> **Modern Java interfaces can contain abstract, default, static, private, and private static methods.**

---

# 1. Abstract Methods

An **abstract method** has **no implementation**.

The implementing class **must override** it.

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
```

---

# 2. Default Methods (Java 8+)

A **default method** has an implementation inside the interface.

Implementing classes **may override** it, but they are **not required** to.

```java
interface Animal {

    default void eat() {
        System.out.println("Animal is eating");
    }
}

class Dog implements Animal {

}

public class Main {

    public static void main(String[] args) {

        Dog d = new Dog();

        d.eat();
    }
}
```

### Output

```text
Animal is eating
```

---

# 3. Static Methods (Java 8+)

A **static method** belongs to the interface itself.

It is called using the **interface name**, not an object.

```java
interface Animal {

    static void info() {
        System.out.println("Animal Interface");
    }
}

public class Main {

    public static void main(String[] args) {

        Animal.info();
    }
}
```

### Output

```text
Animal Interface
```

---

# 4. Private Methods (Java 9+)

A **private method** can be used **only inside the interface**.

It helps avoid duplicate code by allowing multiple default methods to share common logic.

```java
interface Animal {

    default void show() {
        helper();
    }

    private void helper() {
        System.out.println("Private Helper Method");
    }
}

public class Main {

    public static void main(String[] args) {

        Animal obj = new Animal() { };

        obj.show();
    }
}
```

### Output

```text
Private Helper Method
```

---

# 5. Private Static Methods (Java 9+)

A **private static method** is used internally by the interface's static methods.

```java
interface Animal {

    static void display() {
        helper();
    }

    private static void helper() {
        System.out.println("Private Static Helper");
    }
}

public class Main {

    public static void main(String[] args) {

        Animal.display();
    }
}
```

### Output

```text
Private Static Helper
```

---

# Summary Table

| Method Type | Java Version | Has Implementation? | Can be Overridden? |
|-------------|--------------|---------------------|--------------------|
| Abstract | Java 1 | ❌ No | ✅ Yes (Must) |
| Default | Java 8 | ✅ Yes | ✅ Yes (Optional) |
| Static | Java 8 | ✅ Yes | ❌ No |
| Private | Java 9 | ✅ Yes | ❌ No |
| Private Static | Java 9 | ✅ Yes | ❌ No |

---

# Why Were Default and Static Methods Added?

Before Java 8, interfaces could contain **only abstract methods**.

Suppose an interface was already used by thousands of classes:

```java
interface Animal {

    void sound();
}
```

Later, you wanted to add a new method:

```java
void eat();
```

Every implementing class would break because they would all have to implement the new method.

Java 8 introduced **default methods** so that new functionality could be added **without breaking existing code**.

---

# Real-Life Example 📱

Think of a smartphone charger standard.

The interface defines the standard.

- **Abstract Method** → Every charger must supply power.
- **Default Method** → Optional built-in fast charging behavior.
- **Static Method** → Utility information about the charging standard.
- **Private Method** → Internal helper logic used only inside the interface.

---

# Advantages

- Supports abstraction.
- Enables backward compatibility (default methods).
- Provides utility methods (static methods).
- Reduces duplicate code (private methods).
- Makes interfaces more powerful and flexible.

---

# Quick Interview Revision

Modern interfaces can contain:

- ✔ Abstract methods
- ✔ Default methods (Java 8+)
- ✔ Static methods (Java 8+)
- ✔ Private methods (Java 9+)
- ✔ Private static methods (Java 9+)

---

# Can an Interface Have Variables?

## Answer

**Yes.**

An **interface can have variables**, but all variables declared in an interface are **implicitly**:

- `public`
- `static`
- `final`

This means interface variables are **constants**.

> **One-line Answer (Interview)**
>
> **Yes. An interface can have variables, but they are always `public static final` by default.**

---

# Why?

An interface defines a **contract**, not an object's state.

Since interfaces cannot create objects, they cannot have instance variables.

Therefore, any variable declared inside an interface becomes a constant that is shared by all implementing classes.

---

# Example

```java
interface Animal {

    int MAX_AGE = 20;
}

public class Main {

    public static void main(String[] args) {

        System.out.println(Animal.MAX_AGE);
    }
}
```

### Output

```text
20
```

---

# What Does Java Actually Create?

When you write:

```java
interface Animal {

    int MAX_AGE = 20;
}
```

Java automatically treats it as:

```java
interface Animal {

    public static final int MAX_AGE = 20;
}
```

All three keywords are added automatically by the compiler.

---

# Why Can't We Modify Interface Variables?

Since they are `final`, their value cannot be changed.

```java
interface Animal {

    int MAX_AGE = 20;
}

public class Main {

    public static void main(String[] args) {

        Animal.MAX_AGE = 25;     // ❌ Compile-time Error
    }
}
```

### Error

```text
Cannot assign a value to final variable MAX_AGE
```

---

# Accessing Interface Variables

Since interface variables are `static`, they should be accessed using the **interface name**.

```java
interface Animal {

    int MAX_AGE = 20;
}

public class Main {

    public static void main(String[] args) {

        System.out.println(Animal.MAX_AGE);
    }
}
```

✔ Recommended

Although an implementing class can access it directly through inheritance:

```java
class Dog implements Animal {

    void display() {
        System.out.println(MAX_AGE);
    }
}
```

Using the interface name (`Animal.MAX_AGE`) is clearer and recommended.

---

# Memory Representation

```text
              Animal Interface
        ---------------------------
        MAX_AGE = 20
        ---------------------------
               ▲
         Shared by all classes
```

Only **one copy** of the variable exists because it is `static`.

---

# Real-Life Example 🌍

Imagine an interface for vehicles.

```java
interface Vehicle {

    int MAX_SPEED = 120;
}
```

Every vehicle follows the same speed limit.

Since the value is common to all vehicles, it is stored **once** as a constant.

---

# Interface Variables vs Class Variables

| Interface Variable | Class Variable |
|--------------------|----------------|
| Always `public static final` | Can be instance or static |
| Cannot be modified | Can be modified (unless `final`) |
| Shared by all classes | Depends on declaration |
| Used as constants | Used to store object or class data |

---

# Advantages

- Stores constants.
- Shared among all implementing classes.
- Saves memory.
- Improves readability by keeping common constant values in one place.

---

# Quick Interview Revision

- Interfaces **can** have variables.
- They are always:
  - `public`
  - `static`
  - `final`
- They act as **constants**.
- They cannot be modified.

---

# Why are Interface Fields Implicitly `public static final`?

## Answer

All fields (variables) declared in an interface are **implicitly `public`, `static`, and `final`** because an interface is meant to define a **contract**, not to store the state of objects.

Since interfaces **cannot be instantiated**, they cannot have instance variables. Therefore, every variable in an interface is treated as a **constant** shared by all implementing classes.

> **One-line Answer (Interview)**
>
> **Interface fields are implicitly `public static final` because interfaces define constants that are shared by all implementing classes, not object state.**

---

# Why `public`?

Interface members are intended to be used by any class that implements the interface.

If interface fields were private or protected, implementing classes would not be able to access them.

```java
interface Animal {

    int MAX_AGE = 20;
}

class Dog implements Animal {

    void display() {
        System.out.println(MAX_AGE);   // ✔ Accessible
    }
}
```

Java automatically treats it as:

```java
public static final int MAX_AGE = 20;
```

---

# Why `static`?

An interface cannot create objects.

```java
Animal obj = new Animal();   // ❌ Not Allowed
```

Since there are no interface objects, variables cannot belong to an object.

Therefore, they belong to the **interface itself** (class level).

```java
System.out.println(Animal.MAX_AGE);
```

Only **one copy** exists in memory.

---

# Why `final`?

An interface defines a **contract**.

The values declared in an interface should remain constant for all implementing classes.

```java
interface Animal {

    int MAX_AGE = 20;
}

Animal.MAX_AGE = 30;   // ❌ Compile-time Error
```

Making the field `final` prevents accidental modification.

---

# What Does Java Actually Create?

When you write:

```java
interface Animal {

    int MAX_AGE = 20;
}
```

The compiler treats it as:

```java
interface Animal {

    public static final int MAX_AGE = 20;
}
```

All three keywords are added automatically.

---

# Memory Representation

```text
            Animal Interface
      -------------------------
      MAX_AGE = 20
      -------------------------
             ▲
      Shared by all classes
```

Since the field is `static`, only one copy exists.

---

# Real-Life Example 🌍

Imagine a traffic rules interface.

```java
interface TrafficRules {

    int SPEED_LIMIT = 80;
}
```

Every vehicle follows the same speed limit.

The value should:

- Be accessible to everyone (`public`)
- Exist only once (`static`)
- Never change (`final`)

---

# Advantages

- Stores constants.
- Prevents accidental modification.
- Saves memory.
- Provides a common set of values for all implementing classes.

---

# What is the Difference Between an Interface and an Abstract Class?

## Definition

Both **interfaces** and **abstract classes** are used to achieve **abstraction**, but they serve different purposes.

- An **abstract class** provides a **partial implementation** and can maintain state.
- An **interface** defines a **contract** that implementing classes must follow.

> **One-line Answer (Interview)**
>
> **An abstract class is used for sharing common code and state among related classes, whereas an interface is used to define a contract that can be implemented by any class.**

---

# Interface vs Abstract Class

| Feature | Interface | Abstract Class |
|---------|-----------|----------------|
| Keyword | `interface` | `abstract class` |
| Inheritance Keyword | `implements` | `extends` |
| Object Creation | ❌ Not Allowed | ❌ Not Allowed |
| Constructors | ❌ No | ✅ Yes |
| Instance Variables | ❌ No | ✅ Yes |
| Fields | Always `public static final` | Can be instance, static, or final |
| Abstract Methods | ✅ Yes | ✅ Yes |
| Concrete Methods | ✅ Yes (`default`, `static`, `private`) | ✅ Yes |
| Multiple Inheritance | ✅ Supported | ❌ Not Supported (for classes) |
| Object State | ❌ Cannot maintain | ✅ Can maintain |
| Purpose | Defines a contract | Provides partial implementation and common state |

---

# Abstract Class Example

```java
abstract class Animal {

    String name;

    Animal(String name) {
        this.name = name;
    }

    abstract void sound();

    void eat() {
        System.out.println(name + " is eating.");
    }
}

class Dog extends Animal {

    Dog(String name) {
        super(name);
    }

    @Override
    void sound() {
        System.out.println("Dog Barks");
    }
}
```

The abstract class:

- Stores state (`name`)
- Has a constructor
- Has both abstract and concrete methods

---

# Interface Example

```java
interface Animal {

    void sound();

    default void eat() {
        System.out.println("Eating");
    }
}

class Dog implements Animal {

    @Override
    public void sound() {
        System.out.println("Dog Barks");
    }
}
```

The interface defines **what** should be done, while the implementing class defines **how** it is done.

---

# When Should You Use an Abstract Class?

Use an abstract class when:

- Classes are closely related.
- You want to share common code.
- You need constructors.
- You need instance variables.
- You want to provide partial implementation.

Example:

```text
Vehicle
├── Car
├── Bike
└── Bus
```

All vehicles share common properties such as wheels or engine details.

---

# When Should You Use an Interface?

Use an interface when:

- Unrelated classes should follow the same contract.
- Multiple inheritance is required.
- You want loose coupling.
- You only want to specify behavior.

Example:

```text
Flyable

Bird
Airplane
Drone
```

These classes are unrelated but all can **fly**.

---

# Real-Life Example 🏠

### Abstract Class → House Blueprint

The blueprint already contains:

- Foundation
- Walls
- Rooms

Every house shares these common features.

---

### Interface → Electrical Socket Standard

Every appliance must support the same plug standard.

The interface specifies **what must be provided**, but each manufacturer decides **how to implement it**.

---

# Advantages

## Abstract Class

- Shares common code.
- Maintains object state.
- Reduces code duplication.

## Interface

- Supports multiple inheritance.
- Promotes loose coupling.
- Defines a common contract.
- Makes applications more flexible.

---

# Quick Interview Revision

### Abstract Class

- Can have constructors.
- Can have instance variables.
- Can maintain state.
- Used for partial implementation.

### Interface

- No constructors.
- No instance variables.
- Defines a contract.
- Supports multiple inheritance.

---

# Why Doesn't Java Support Multiple Inheritance Through Classes?

## Answer

Java **does not support multiple inheritance through classes** because it can lead to **ambiguity**, commonly known as the **Diamond Problem**.

If a class inherits from two parent classes that contain the same method, the compiler cannot determine **which parent's method should be inherited**.

To avoid this ambiguity and keep Java simple and predictable, multiple inheritance of classes is not allowed.

> **One-line Answer (Interview)**
>
> **Java does not support multiple inheritance through classes to avoid ambiguity (Diamond Problem) and maintain code simplicity.**

---

# What is the Diamond Problem?

Suppose Java allowed this:

```java
class A {

    void show() {
        System.out.println("Class A");
    }
}

class B extends A {

}

class C extends A {

}

class D extends B, C {      // ❌ Not Allowed in Java

}
```

Now imagine:

```java
D obj = new D();

obj.show();
```

Question:

Which `show()` should Java execute?

- `B`'s inherited version?
- `C`'s inherited version?

This creates ambiguity.

---

# Another Example

```java
class Father {

    void property() {
        System.out.println("Father Property");
    }
}

class Mother {

    void property() {
        System.out.println("Mother Property");
    }
}

class Child extends Father, Mother { }    // ❌ Not Allowed
```

If:

```java
Child c = new Child();

c.property();
```

Which method should be called?

Java cannot decide.

---

# Diamond Representation

```text
          A
        /   \
       B     C
        \   /
          D
```

When `D` calls a method inherited from `A`, ambiguity may arise.

This is called the **Diamond Problem**.

---

# How Java Solves This

Java allows:

```java
class B extends A { }
```

But **not**:

```java
class D extends B, C { }    // ❌
```

This eliminates ambiguity.

---

# Real-Life Example 👨‍👩‍👦

Imagine a child receives two different instructions:

Father:

> "Wake up at 6 AM."

Mother:

> "Wake up at 7 AM."

The child doesn't know which instruction to follow.

Similarly, Java cannot decide which inherited implementation should be used.

---

# Advantages of This Design

- Prevents ambiguity.
- Makes code easier to understand.
- Simplifies method resolution.
- Improves maintainability.

---

# How Does Java Achieve Multiple Inheritance Using Interfaces?

## Answer

Java supports **multiple inheritance through interfaces**.

A class can implement **multiple interfaces** because interfaces define **behavior (contracts)** rather than object state.

If conflicts occur (such as two default methods with the same signature), Java requires the programmer to resolve them explicitly.

> **One-line Answer (Interview)**
>
> **Java achieves multiple inheritance by allowing a class to implement multiple interfaces using the `implements` keyword.**

---

# Example

```java
interface Camera {

    void takePhoto();
}

interface MusicPlayer {

    void playMusic();
}

class Smartphone implements Camera, MusicPlayer {

    @Override
    public void takePhoto() {
        System.out.println("Taking Photo");
    }

    @Override
    public void playMusic() {
        System.out.println("Playing Music");
    }

    public static void main(String[] args) {

        Smartphone phone = new Smartphone();

        phone.takePhoto();
        phone.playMusic();
    }
}
```

### Output

```text
Taking Photo
Playing Music
```

---

# Why is This Safe?

Interfaces usually contain **method declarations**, not object state.

The implementing class provides the implementation, so there is no ambiguity.

---

# Real-Life Example 📱

A smartphone can act as:

- Camera
- Music Player
- GPS
- Phone

Instead of inheriting from multiple classes, it implements multiple interfaces.

---

# Quick Interview Revision

- Multiple inheritance through classes → ❌ Not Supported
- Multiple inheritance through interfaces → ✅ Supported

---

# Easy Trick to Remember

```text
Class

extends → One Class

implements → Many Interfaces
```

# What Happens if Two Interfaces Contain Methods with the Same Signature?

## Answer

If two interfaces contain **abstract methods** with the **same signature**, there is **no conflict**.

The implementing class only needs to provide **one implementation** of that method.

> **One-line Answer (Interview)**
>
> **If two interfaces have the same abstract method signature, the implementing class provides a single implementation that satisfies both interfaces.**

---

# Example

```java
interface A {

    void display();
}

interface B {

    void display();
}

class Demo implements A, B {

    @Override
    public void display() {
        System.out.println("Display Method");
    }

    public static void main(String[] args) {

        Demo obj = new Demo();

        obj.display();
    }
}
```

### Output

```text
Display Method
```

---

# Why is There No Ambiguity?

Both interfaces only declare **what** should be done.

Neither provides an implementation.

Therefore, the implementing class supplies the implementation, eliminating ambiguity.

---

# Interview Tip

This is **different** from two interfaces having the **same default method**, which **does** create a conflict.

# 53. What Happens if Two Interfaces Provide the Same Default Method?

## Answer

If two interfaces provide a **default method with the same signature**, the implementing class **must override** the method.

Otherwise, the compiler reports an error because Java cannot decide which default implementation to use.

> **One-line Answer (Interview)**
>
> **When two interfaces provide the same default method, the implementing class must override it to resolve the conflict.**

---

# Example

```java
interface A {

    default void show() {
        System.out.println("A");
    }
}

interface B {

    default void show() {
        System.out.println("B");
    }
}

class Demo implements A, B {

    @Override
    public void show() {
        System.out.println("Resolved");
    }

    public static void main(String[] args) {

        Demo obj = new Demo();

        obj.show();
    }
}
```

### Output

```text
Resolved
```

---

# Calling Both Default Methods

You can explicitly invoke both interface implementations.

```java
class Demo implements A, B {

    @Override
    public void show() {

        A.super.show();

        B.super.show();
    }
}
```

### Output

```text
A
B
```

---

# Why?

Both interfaces provide an implementation, so Java cannot choose automatically.

The programmer must resolve the ambiguity.

---

# Easy Trick

```text
Two Default Methods

↓

Override Required
```

# What is a Default Method in an Interface?

## Definition

A **default method** is a method inside an interface that has a **method body**.

It is declared using the `default` keyword.

Default methods were introduced in **Java 8** to allow new methods to be added to interfaces **without breaking existing implementations**.

> **One-line Definition (Interview)**
>
> **A default method is a method with an implementation inside an interface, declared using the `default` keyword.**

---

# Syntax

```java
interface Animal {

    default void eat() {
        System.out.println("Animal is eating");
    }
}
```

---

# Example

```java
interface Animal {

    default void eat() {
        System.out.println("Animal is eating");
    }
}

class Dog implements Animal {

}

public class Main {

    public static void main(String[] args) {

        Dog d = new Dog();

        d.eat();
    }
}
```

### Output

```text
Animal is eating
```

---

# Can It Be Overridden?

**Yes.**

```java
class Dog implements Animal {

    @Override
    public void eat() {
        System.out.println("Dog is eating");
    }
}
```

---

# Why Were Default Methods Introduced?

Suppose an interface is used by thousands of classes.

Adding a new abstract method would force every class to implement it.

Default methods allow new functionality to be added without breaking existing code.

---

# Quick Interview Revision

- Introduced in **Java 8**
- Declared using `default`
- Has an implementation
- Can be overridden
- Supports backward compatibility

---

# Easy Trick

```text
default

✔ Method Body
✔ Can Override
✔ Java 8
```

# What is a Static Method in an Interface?

## Definition

A **static method** in an interface is a method that belongs to the **interface itself**, not to the implementing class.

It is declared using the `static` keyword and is called using the **interface name**.

Static methods were introduced in **Java 8**.

> **One-line Definition (Interview)**
>
> **A static method in an interface belongs to the interface and is invoked using the interface name.**

---

# Example

```java
interface Animal {

    static void info() {
        System.out.println("Animal Interface");
    }
}

public class Main {

    public static void main(String[] args) {

        Animal.info();
    }
}
```

### Output

```text
Animal Interface
```

---

# Can a Static Interface Method Be Overridden?

**No.**

Static methods belong to the interface and are **not inherited** by implementing classes.

```java
class Dog implements Animal {

    static void info() {
        System.out.println("Dog");
    }
}
```

This is **not overriding**.

---

# Why Use Static Methods?

- Utility methods related to the interface.
- Common helper methods.
- Avoid creating separate utility classes.

---

# Static Method vs Default Method

| Static Method | Default Method |
|---------------|----------------|
| Belongs to the interface | Inherited by implementing classes |
| Called using interface name | Called using object |
| Cannot be overridden | Can be overridden |
| Introduced in Java 8 | Introduced in Java 8 |

---

# Quick Interview Revision

- Introduced in Java 8.
- Belongs to the interface.
- Called using the interface name.
- Cannot be overridden.

---

# Easy Trick

```text
static Interface Method

✔ Interface Name
✔ No Object Needed
✔ Cannot Override
```

### Mnemonic

> **"Default Methods are Inherited, Static Methods Stay with the Interface."**
