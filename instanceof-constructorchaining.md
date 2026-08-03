# What is the Purpose of `instanceof`?

## Definition

The **`instanceof`** operator is used to check whether an object is an instance of a particular class, subclass, or interface.

It returns:

- `true` → If the object belongs to the specified type (or its subclass/implements the interface).
- `false` → Otherwise.

It is mainly used to **perform safe downcasting** and avoid `ClassCastException`.

> **One-line Definition (Interview)**
>
> **`instanceof` checks whether an object is an instance of a specified class or interface and is commonly used before downcasting.**

---

# Syntax

```java
object instanceof ClassName
```

The result is always a boolean (`true` or `false`).

---

# Example

```java
class Animal { }

class Dog extends Animal { }

public class Main {

    public static void main(String[] args) {

        Animal obj = new Dog();

        System.out.println(obj instanceof Animal);

        System.out.println(obj instanceof Dog);
    }
}
```

### Output

```text
true
true
```

---

# Example with `false`

```java
class Animal { }

class Dog extends Animal { }

class Cat extends Animal { }

public class Main {

    public static void main(String[] args) {

        Animal obj = new Cat();

        System.out.println(obj instanceof Dog);
    }
}
```

### Output

```text
false
```

---

# Why Do We Use `instanceof`?

The most common use is to **avoid `ClassCastException`**.

### Without `instanceof`

```java
Animal obj = new Cat();

Dog d = (Dog) obj;      // ❌ Runtime Exception
```

### With `instanceof`

```java
Animal obj = new Cat();

if (obj instanceof Dog) {

    Dog d = (Dog) obj;

    d.bark();

} else {

    System.out.println("Cannot Cast");
}
```

### Output

```text
Cannot Cast
```

No exception occurs.

---

# `instanceof` with Interfaces

```java
interface Animal { }

class Dog implements Animal { }

public class Main {

    public static void main(String[] args) {

        Dog d = new Dog();

        System.out.println(d instanceof Animal);
    }
}
```

### Output

```text
true
```

---

# Memory Representation

```java
Animal obj = new Dog();
```

```text
Reference

Animal obj
      │
      ▼

Object

Dog
```

Checks:

```java
obj instanceof Animal
```

✔ `true`

---

```java
obj instanceof Dog
```

✔ `true`

---

# Real-Life Example 🎓

Imagine a university.

A student belongs to the **Student** category.

Before giving access to the student library, the university checks:

```text
Is this person a Student?
```

If **Yes**, access is granted.

Similarly, `instanceof` checks whether an object belongs to a particular type before performing operations like downcasting.

---

# Advantages

- Prevents `ClassCastException`.
- Enables safe downcasting.
- Helps identify an object's actual type.
- Improves code safety.

---

# Quick Interview Revision

- Returns `true` or `false`.
- Checks class, subclass, or interface type.
- Commonly used before downcasting.
- Prevents `ClassCastException`.

---

# 65. What is Pattern Matching with `instanceof`?

## Definition

**Pattern Matching with `instanceof`** is a feature introduced in **Java 16** that combines:

1. Type checking using `instanceof`
2. Automatic type casting

It removes the need to manually cast the object after checking its type.

> **One-line Definition (Interview)**
>
> **Pattern Matching with `instanceof` automatically casts an object after a successful type check, making the code shorter, safer, and more readable.**

---

# Before Java 16

Suppose we want to access a child-specific method.

```java
class Animal { }

class Dog extends Animal {

    void bark() {
        System.out.println("Dog Barks");
    }
}

public class Main {

    public static void main(String[] args) {

        Animal obj = new Dog();

        if (obj instanceof Dog) {

            Dog d = (Dog) obj;

            d.bark();
        }
    }
}
```

Notice that after checking:

```java
obj instanceof Dog
```

we still have to write:

```java
Dog d = (Dog) obj;
```

This is repetitive.

---

# Java 16+ (Pattern Matching)

Java allows us to combine the check and the cast.

```java
class Animal { }

class Dog extends Animal {

    void bark() {
        System.out.println("Dog Barks");
    }
}

public class Main {

    public static void main(String[] args) {

        Animal obj = new Dog();

        if (obj instanceof Dog d) {

            d.bark();
        }
    }
}
```

### Output

```text
Dog Barks
```

---

# How Does It Work?

```java
if (obj instanceof Dog d)
```

Java performs two operations:

### Step 1

Checks:

```java
obj instanceof Dog
```

↓

If the result is `true`

↓

### Step 2

Automatically creates:

```java
Dog d = (Dog) obj;
```

No explicit cast is required.

---

# Comparison

### Before Java 16

```java
if (obj instanceof Dog) {

    Dog d = (Dog) obj;

    d.bark();
}
```

---

### Java 16+

```java
if (obj instanceof Dog d) {

    d.bark();
}
```

Much shorter and cleaner.

---

# Benefits

- Eliminates explicit casting.
- Reduces boilerplate code.
- Improves readability.
- Makes code safer by combining the check and cast.

---

# Real-Life Example 🎫

Imagine entering a concert.

Old process:

1. Check the ticket.
2. Issue a wristband.

New process:

1. Check the ticket and immediately issue the wristband if valid.

Pattern matching does the same by combining **type checking** and **casting** into a single step.

---

# Quick Interview Revision

- Introduced in **Java 16**.
- Combines `instanceof` and type casting.
- Eliminates explicit casts.
- Makes code cleaner and safer.

---
