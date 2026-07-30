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
