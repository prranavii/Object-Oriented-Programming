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

# 66. ⭐ What is Constructor Chaining?

## Definition

**Constructor Chaining** is the process of calling one constructor from another constructor to reuse initialization code.

In Java, constructor chaining can happen in two ways:

1. **Using `this()`** → Calls another constructor in the **same class**.
2. **Using `super()`** → Calls a constructor of the **parent class**.

It helps avoid code duplication and ensures proper object initialization.

> **One-line Definition (Interview)**
>
> **Constructor chaining is the process of invoking one constructor from another using `this()` or `super()`.**

---

# Types of Constructor Chaining

| Keyword | Calls |
|---------|-------|
| `this()` | Another constructor in the same class |
| `super()` | Constructor of the parent class |

---

# Example

```java
class Parent {

    Parent() {
        System.out.println("Parent Constructor");
    }
}

class Child extends Parent {

    Child() {
        System.out.println("Child Constructor");
    }

    public static void main(String[] args) {

        new Child();
    }
}
```

### Output

```text
Parent Constructor
Child Constructor
```

---

# Why Do We Need Constructor Chaining?

- Avoids duplicate initialization code.
- Improves code reusability.
- Ensures parent objects are initialized first.
- Makes constructors easier to maintain.

---

# Quick Interview Revision

- Constructor chaining = constructor calling another constructor.
- `this()` → Same class.
- `super()` → Parent class.

---

# Easy Trick

```text
this()

↓

Same Class

super()

↓

Parent Class
```

# 67. How Does Constructor Chaining Work Using `this()`?

## Definition

The **`this()`** keyword is used to call **another constructor of the same class**.

It is mainly used to reuse initialization code and avoid duplication.

> **One-line Answer (Interview)**
>
> **`this()` calls another constructor in the same class and must be the first statement in the constructor.**

---

# Example

```java
class Student {

    Student() {
        this("Pranavi");
        System.out.println("Default Constructor");
    }

    Student(String name) {
        System.out.println(name);
    }

    public static void main(String[] args) {

        new Student();
    }
}
```

### Output

```text
Pranavi
Default Constructor
```

---

# Constructor Flow

```text
Student()

      │

      ▼

this("Pranavi")

      │

      ▼

Student(String)

      │

      ▼

Returns

      │

      ▼

Default Constructor
```

---

# Rules

- Must be the **first statement**.
- Can call only one constructor.
- Cannot be used with `super()` in the same constructor.

---

# Easy Trick

```text
this()

↓

Same Class Constructor
```

# 68. How Does Constructor Chaining Work Using `super()`?

## Definition

The **`super()`** keyword is used to call a **constructor of the parent class**.

It ensures that the parent class is initialized before the child class.

> **One-line Answer (Interview)**
>
> **`super()` invokes the parent class constructor and must be the first statement in the child constructor.**

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
        super();
        System.out.println("Dog Constructor");
    }

    public static void main(String[] args) {

        new Dog();
    }
}
```

### Output

```text
Animal Constructor
Dog Constructor
```

---

# Flow

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

Returns

      │

      ▼

Dog()
```

---

# Note

If you do **not** write `super()`, Java inserts it automatically (provided the parent has a no-argument constructor).

---

# Easy Trick

```text
super()

↓

Parent Constructor
```

# 69. Can `this()` and `super()` Appear in the Same Constructor?

## Answer

**No.**

A constructor **cannot contain both `this()` and `super()`** because both must be the **first statement** in the constructor.

> **One-line Answer (Interview)**
>
> **No. `this()` and `super()` cannot appear in the same constructor because both must be the first statement.**

---

# Invalid Example

```java
class Parent {

    Parent() { }
}

class Child extends Parent {

    Child() {

        this();

        super();      // ❌ Compile-time Error
    }

    Child(int x) { }
}
```

---

# Why?

The compiler cannot execute two statements first.

Only one constructor call is allowed as the first statement.

---

# Correct Example

```java
Child() {

    this(10);
}
```

OR

```java
Child() {

    super();
}
```

---

# Easy Trick

```text
Constructor

First Statement

↓

Either

this()

OR

super()

Never Both
```

# 70. Why Must `this()` or `super()` Be the First Constructor Statement?

## Answer

Java requires `this()` or `super()` to be the **first statement** because the object must be initialized in the correct order.

The parent part of an object (or another constructor in the same class) must be initialized **before** executing the current constructor's code.

> **One-line Answer (Interview)**
>
> **`this()` and `super()` must be first to ensure proper constructor chaining and object initialization.**

---

# Example

```java
class Parent {

    Parent() {
        System.out.println("Parent");
    }
}

class Child extends Parent {

    Child() {

        System.out.println("Hello");

        super();      // ❌ Compile-time Error
    }
}
```

Java reports an error because `super()` is not the first statement.

---

# Correct Order

```java
Child() {

    super();

    System.out.println("Hello");
}
```

---

# Easy Trick

```text
Constructor

↓

Parent First

↓

Child Next
```

# 71. What is the Order of Constructor Execution in Inheritance?

## Answer

When an object of a child class is created:

1. Parent constructor executes first.
2. Child constructor executes next.

If there are multiple inheritance levels, constructors execute **from the topmost parent to the bottommost child**.

---

# Example

```java
class A {

    A() {
        System.out.println("A");
    }
}

class B extends A {

    B() {
        System.out.println("B");
    }
}

class C extends B {

    C() {
        System.out.println("C");
    }

    public static void main(String[] args) {

        new C();
    }
}
```

### Output

```text
A
B
C
```

---

# Constructor Order

```text
Object Creation

↓

A()

↓

B()

↓

C()
```

---

# Easy Trick

```text
Top Parent

↓

Child

↓

Grandchild
```

# 72. What Happens if a Constructor Calls an Overridable Method?

## Answer

A constructor **can call an overridable method**, but **it is not recommended**.

If the method is overridden in a child class, the **child's version** is executed **before the child constructor runs**.

This may lead to unexpected behavior because the child object may not be fully initialized.

> **One-line Answer (Interview)**
>
> **Calling an overridable method from a constructor is dangerous because the overridden child method executes before the child constructor finishes.**

---

# Example

```java
class Parent {

    Parent() {
        show();
    }

    void show() {
        System.out.println("Parent");
    }
}

class Child extends Parent {

    int x = 10;

    @Override
    void show() {
        System.out.println(x);
    }

    public static void main(String[] args) {

        new Child();
    }
}
```

### Output

```text
0
```

---

# Why?

Execution order:

```text
Create Child Object

↓

Parent Constructor

↓

show()

↓

Child.show()

↓

Child Variables Not Initialized Yet

↓

x = 0
```

The child constructor hasn't run yet, so `x` still has its default value.

---

# Best Practice

❌ Avoid calling overridable methods from constructors.

# 73. Can a Constructor be Private?

## Answer

**Yes.**

A constructor **can be private**.

A private constructor prevents object creation from outside the class.

It is commonly used in:

- Singleton Design Pattern
- Utility classes
- Factory methods

---

# Example

```java
class Demo {

    private Demo() {
        System.out.println("Private Constructor");
    }

    public static void main(String[] args) {

        new Demo();
    }
}
```

### Output

```text
Private Constructor
```

Outside the class:

```java
Demo d = new Demo();   // ❌ Compile-time Error
```

---

# Easy Trick

```text
Private Constructor

↓

No External Object Creation
```

# 74. Can a Constructor be `static`, `final`, or `abstract`?

## Answer

**No.**

A constructor **cannot** be declared as:

- `static`
- `final`
- `abstract`

---

# Why?

## `static`

Constructors are used to initialize **objects**, while `static` belongs to the **class**.

```java
static Demo() { }    // ❌
```

---

## `final`

Constructors are **never inherited**, so preventing overriding makes no sense.

```java
final Demo() { }     // ❌
```

---

## `abstract`

An abstract method has no body.

A constructor must always have a body because it initializes an object.

```java
abstract Demo();     // ❌
```

---

# Quick Table

| Modifier | Allowed? | Reason |
|----------|----------|--------|
| `static` | ❌ | Constructor belongs to objects |
| `final` | ❌ | Constructors cannot be overridden |
| `abstract` | ❌ | Constructors must have a body |

---

# Easy Trick

```text
Constructor

❌ static

❌ final

❌ abstract
```

# 75. What Happens if the Parent Class Has No No-Argument Constructor?

## Answer

If the parent class **does not have a no-argument (default) constructor**, the child class **must explicitly call one of the parent's parameterized constructors using `super(...)`**.

Otherwise, the code will fail to compile.

> **One-line Answer (Interview)**
>
> **If the parent has no default constructor, the child must explicitly call a parent constructor using `super(...)`; otherwise, a compile-time error occurs.**

---

# Example

```java
class Parent {

    Parent(int x) {
        System.out.println(x);
    }
}

class Child extends Parent {

    Child() {

        super();      // ❌ Compile-time Error
    }
}
```

### Error

```text
Constructor Parent() is undefined
```

---

# Correct Example

```java
class Parent {

    Parent(int x) {
        System.out.println("Parent: " + x);
    }
}

class Child extends Parent {

    Child() {

        super(10);

        System.out.println("Child");
    }

    public static void main(String[] args) {

        new Child();
    }
}
```

### Output

```text
Parent: 10
Child
```

---

# Why?

If you don't write:

```java
super(...);
```

Java automatically inserts:

```java
super();
```

If the parent doesn't have a no-argument constructor, the compiler cannot find `Parent()` and reports an error.

---

# Constructor Flow

```text
Child()

↓

super(10)

↓

Parent(int)

↓

Child()
```

---

# Quick Interview Revision

- Parent has a default constructor → `super()` is inserted automatically.
- Parent has **only parameterized constructors** → Child **must** call `super(arguments)`.
- Otherwise → **Compile-time Error**.

---

# Easy Trick

```text
No Parent Default Constructor

↓

Write super(arguments)

↓

Otherwise Compile-Time Error
```
