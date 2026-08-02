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
