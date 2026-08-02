# What Happens When the Reference Type is Parent but the Object Type is Child?

## Definition

In Java, a **parent class reference can refer to a child class object**.

This is known as **Upcasting** and is one of the most important concepts used to achieve **Runtime Polymorphism**.

```java
Parent obj = new Child();
```

Here:

- **Reference Type** → `Parent`
- **Object Type** → `Child`

> **One-line Answer (Interview)**
>
> **When the reference type is Parent and the object type is Child, the reference can access only the members declared in the Parent class, but overridden methods are executed from the Child class at runtime.**

---

# Example

```java
class Animal {

    void sound() {
        System.out.println("Animal makes a sound");
    }

    void eat() {
        System.out.println("Animal is eating");
    }
}

class Dog extends Animal {

    @Override
    void sound() {
        System.out.println("Dog barks");
    }

    void bark() {
        System.out.println("Dog is barking");
    }
}

public class Main {

    public static void main(String[] args) {

        Animal obj = new Dog();

        obj.sound();
        obj.eat();

        // obj.bark();   // ❌ Compile-time Error
    }
}
```

### Output

```text
Dog barks
Animal is eating
```

---

# What Happens Internally?

```java
Animal obj = new Dog();
```

- The **reference** is of type `Animal`.
- The **actual object** created is `Dog`.

Memory Representation:

```text
Stack

obj
 │
 ▼

Heap

Dog Object
```

> There is **no Animal object** in memory.
>
> The reference of type `Animal` simply points to a `Dog` object.

---

# Rule 1: Reference Type Decides What Can Be Accessed

The compiler checks the **reference type**.

```java
Animal obj = new Dog();
```

The `Animal` class contains:

```java
void sound();

void eat();
```

Therefore,

```java
obj.sound();   // ✔
obj.eat();     // ✔
```

are allowed.

---

# Rule 2: Object Type Decides Which Overridden Method Executes

The `sound()` method is overridden.

```java
obj.sound();
```

At runtime, Java checks the **actual object type**.

Since the object is `Dog`, Java executes:

```java
Dog.sound();
```

Output:

```text
Dog barks
```

This is called **Dynamic Method Dispatch** or **Runtime Polymorphism**.

---

# Rule 3: Child-Specific Methods Cannot Be Accessed

The `Dog` class contains:

```java
void bark() { }
```

The `Animal` class does **not**.

Therefore,

```java
obj.bark();
```

❌ Compile-time Error

Why?

Because the compiler only looks at the **reference type (`Animal`)**, which doesn't declare `bark()`.

---

# Accessing Child-Specific Methods

If you're certain that the object is actually a `Dog`, you can **downcast** the reference.

```java
Animal obj = new Dog();

Dog d = (Dog) obj;

d.bark();
```

### Output

```text
Dog is barking
```

---

# Variables vs Methods

Consider:

```java
class Parent {

    int x = 10;

    void show() {
        System.out.println("Parent");
    }
}

class Child extends Parent {

    int x = 20;

    @Override
    void show() {
        System.out.println("Child");
    }
}
```

```java
Parent obj = new Child();

System.out.println(obj.x);

obj.show();
```

### Output

```text
10
Child
```

---

# Why?

### Variables

Variables are resolved at **compile time**.

The compiler checks the **reference type**.

```java
obj.x
```

Reference type:

```text
Parent
```

Output:

```text
10
```

---

### Methods

Methods are resolved at **runtime**.

Java checks the **object type**.

```java
obj.show();
```

Object type:

```text
Child
```

Output:

```text
Child
```

---

# Summary Table

| Member | Decided By |
|---------|------------|
| Instance Variable | **Reference Type** |
| Static Variable | **Reference Type** |
| Static Method | **Reference Type** |
| Overridden Instance Method | **Object Type** |

---

# Real-Life Example 🚗

Imagine a parking lot.

```java
Vehicle v = new Car();
```

The security guard only knows:

```text
Vehicle
```

So he allows only operations common to all vehicles:

- Start
- Stop

He doesn't know about:

- Open Sunroof

because that is specific to `Car`.

However, when the **Start** button is pressed, the actual **Car** starts using its own implementation.

---

# Why Do We Use This?

Using a parent reference allows us to write flexible code.

```java
Animal a;

a = new Dog();
a.sound();

a = new Cat();
a.sound();

a = new Lion();
a.sound();
```

The same reference works with multiple subclasses.

This is the foundation of **Runtime Polymorphism**.

---

# 57. Which Members are Decided Using Reference Type and Which Using Object Type?

## Definition

When a parent reference points to a child object:

```java
Parent obj = new Child();
```

Java uses **both the reference type and the object type**, but for different purposes.

- **Reference Type** determines **what members are accessible** at compile time.
- **Object Type** determines **which overridden instance method executes** at runtime.

> **One-line Answer (Interview)**
>
> **Reference type decides member accessibility, while object type decides the execution of overridden instance methods.**

---

# Example

```java
class Parent {

    int x = 10;

    static int y = 100;

    void show() {
        System.out.println("Parent show()");
    }

    static void display() {
        System.out.println("Parent display()");
    }
}

class Child extends Parent {

    int x = 20;

    static int y = 200;

    @Override
    void show() {
        System.out.println("Child show()");
    }

    static void display() {
        System.out.println("Child display()");
    }

    void childMethod() {
        System.out.println("Child Method");
    }
}

public class Main {

    public static void main(String[] args) {

        Parent obj = new Child();

        System.out.println(obj.x);
        System.out.println(obj.y);

        obj.show();
        obj.display();

        // obj.childMethod();   ❌ Compile-time Error
    }
}
```

### Output

```text
10
100
Child show()
Parent display()
```

---

# Explanation

## 1. Instance Variables

```java
System.out.println(obj.x);
```

Output:

```text
10
```

### Why?

Variables are resolved at **compile time**.

Java checks the **reference type** (`Parent`), so it accesses:

```java
Parent.x
```

---

## 2. Static Variables

```java
System.out.println(obj.y);
```

Output:

```text
100
```

Static variables belong to the class.

They are resolved using the **reference type**.

---

## 3. Instance Methods (Overridden)

```java
obj.show();
```

Output:

```text
Child show()
```

Java checks the **actual object type** (`Child`) at runtime.

This is called **Dynamic Method Dispatch**.

---

## 4. Static Methods

```java
obj.display();
```

Output:

```text
Parent display()
```

Static methods belong to the class, not the object.

They are resolved using the **reference type**.

This is **Method Hiding**, not Method Overriding.

---

## 5. Child-Specific Methods

```java
obj.childMethod();
```

❌ Compile-time Error

Why?

The compiler only checks the **reference type** (`Parent`).

Since `Parent` doesn't declare `childMethod()`, it cannot be accessed directly.

---

# Complete Summary Table

| Member | Decided By | Runtime Polymorphism? |
|---------|------------|-----------------------|
| Instance Variable | **Reference Type** | ❌ No |
| Static Variable | **Reference Type** | ❌ No |
| Static Method | **Reference Type** | ❌ No (Method Hiding) |
| Overridden Instance Method | **Object Type** | ✅ Yes |
| Child-Specific Method | **Reference Type** (must exist in parent) | ❌ Not directly accessible |

---

# Memory Representation

```java
Parent obj = new Child();
```

```text
Reference Type

Parent obj
     │
     ▼

Object Type

Child Object
```

There is **only one object** in memory:

```text
Child Object
```

The `Parent` reference simply points to it.

---

# Real-Life Example 🚗

Imagine a **Vehicle** reference pointing to a **Car** object.

```java
Vehicle v = new Car();
```

The compiler only knows about methods available in `Vehicle`.

```text
Vehicle
--------
start()
stop()
```

So these are allowed:

```java
v.start();
v.stop();
```

Suppose `Car` has:

```java
openSunroof();
```

Then:

```java
v.openSunroof();
```

❌ Compile-time Error

because `Vehicle` doesn't declare `openSunroof()`.

However, if `start()` is overridden in `Car`, then:

```java
v.start();
```

executes **Car's** version because Java checks the **object type** at runtime.

---

# Why Does Java Do This?

Java separates responsibilities:

### Compile Time

The compiler uses the **reference type** to verify that the method or variable exists.

### Runtime

For overridden **instance methods**, Java uses the **object type** to achieve polymorphism.

This provides both:

- **Type safety**
- **Runtime flexibility**

---
