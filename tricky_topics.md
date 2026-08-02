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

# Which Members are Decided Using Reference Type and Which Using Object Type?

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

# What Happens When Parent and Child Have an Instance Variable with the Same Name?

## Answer

When a **parent class and a child class have instance variables with the same name**, the child variable **hides** the parent variable.

Unlike methods, **instance variables are not overridden**.

The variable that is accessed depends on the **reference type**, **not** on the object type.

> **One-line Answer (Interview)**
>
> **Instance variables are not overridden. If both parent and child have variables with the same name, the variable accessed is determined by the reference type at compile time.**

---

# Example

```java
class Parent {

    int x = 10;
}

class Child extends Parent {

    int x = 20;
}

public class Main {

    public static void main(String[] args) {

        Parent p = new Parent();
        Child c = new Child();
        Parent obj = new Child();

        System.out.println(p.x);
        System.out.println(c.x);
        System.out.println(obj.x);
    }
}
```

### Output

```text
10
20
10
```

---

# Explanation

## Case 1

```java
Parent p = new Parent();

System.out.println(p.x);
```

Output:

```text
10
```

The reference and object are both `Parent`.

---

## Case 2

```java
Child c = new Child();

System.out.println(c.x);
```

Output:

```text
20
```

The reference and object are both `Child`.

---

## Case 3 (Most Important)

```java
Parent obj = new Child();

System.out.println(obj.x);
```

Output:

```text
10
```

Although the object is `Child`, Java prints the **Parent's variable**.

### Why?

Variables are resolved at **compile time**.

The compiler checks only the **reference type**.

Reference Type:

```text
Parent
```

Therefore, Java accesses:

```java
Parent.x
```

---

# Memory Representation

```java
Parent obj = new Child();
```

```text
Stack

obj
 │
 ▼

Heap

Child Object

---------------
Parent.x = 10
Child.x  = 20
---------------
```

The `Child` object actually contains **both variables**:

- `Parent.x`
- `Child.x`

The reference determines **which one is accessible**.

---

# Variable Hiding

This behavior is called **Variable Hiding** (also known as **Field Hiding**).

The child variable **hides** the parent variable.

It is **not** method overriding.

---

# Variable Hiding vs Method Overriding

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

public class Main {

    public static void main(String[] args) {

        Parent obj = new Child();

        System.out.println(obj.x);

        obj.show();
    }
}
```

### Output

```text
10
Child
```

### Why?

#### Variable

```java
obj.x
```

Reference type decides.

Output:

```text
10
```

---

#### Method

```java
obj.show();
```

Object type decides.

Output:

```text
Child
```

---

# Accessing Both Variables

```java
class Parent {

    int x = 10;
}

class Child extends Parent {

    int x = 20;

    void display() {

        System.out.println(x);

        System.out.println(super.x);
    }
}
```

### Output

```text
20
10
```

Here:

- `x` → Child's variable.
- `super.x` → Parent's variable.

---

# Real-Life Example 👨‍👦

Imagine a father and son both have a bank account named **Balance**.

```text
Father Balance = ₹10,000

Son Balance = ₹20,000
```

If someone asks using the **Father's identity**, they see the father's balance.

If they ask using the **Son's identity**, they see the son's balance.

Similarly:

- **Reference Type** acts like the identity.
- It determines which variable is accessed.

---

# Why Doesn't Variable Overriding Exist?

Variables represent **state**, not behavior.

Allowing runtime overriding of variables would make programs confusing and unpredictable.

Therefore, Java resolves variables at **compile time** using the reference type.

---

# Quick Interview Revision

- Variables are **not overridden**.
- Variables are **hidden**.
- Variable access depends on the **reference type**.
- Method execution depends on the **object type**.

---

# Summary Table

| Member | Decided By | Polymorphism |
|---------|------------|--------------|
| Instance Variable | Reference Type | ❌ No |
| Static Variable | Reference Type | ❌ No |
| Static Method | Reference Type | ❌ No |
| Overridden Instance Method | Object Type | ✅ Yes |

---

# What Happens When Parent and Child Have a Static Method with the Same Signature?

## Answer

When a **parent class and a child class have static methods with the same signature**, the child method **does not override** the parent method.

Instead, it **hides** the parent method. This is called **Method Hiding**.

The method that gets executed is determined by the **reference type**, not the object type.

> **One-line Answer (Interview)**
>
> **If Parent and Child have static methods with the same signature, the child method hides the parent method. This is Method Hiding, and the method call is resolved using the reference type at compile time.**

---

# Why Doesn't Overriding Happen?

Method overriding requires **runtime polymorphism**.

Static methods:

- Belong to the **class**, not the object.
- Are resolved at **compile time**.
- Cannot participate in runtime polymorphism.

Therefore, static methods are **hidden**, not overridden.

---

# Example

```java
class Parent {

    static void display() {
        System.out.println("Parent Static Method");
    }
}

class Child extends Parent {

    static void display() {
        System.out.println("Child Static Method");
    }

    public static void main(String[] args) {

        Parent p = new Parent();
        Child c = new Child();
        Parent obj = new Child();

        p.display();
        c.display();
        obj.display();
    }
}
```

### Output

```text
Parent Static Method
Child Static Method
Parent Static Method
```

---

# Explanation

## Case 1

```java
Parent p = new Parent();

p.display();
```

Output:

```text
Parent Static Method
```

Reference type:

```text
Parent
```

---

## Case 2

```java
Child c = new Child();

c.display();
```

Output:

```text
Child Static Method
```

Reference type:

```text
Child
```

---

## Case 3 (Most Important)

```java
Parent obj = new Child();

obj.display();
```

Output:

```text
Parent Static Method
```

Although the object is `Child`, Java executes the **Parent's static method**.

### Why?

Static methods belong to the **class**.

The compiler checks the **reference type**, which is:

```text
Parent
```

Therefore, Java executes:

```java
Parent.display();
```

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

For **static methods**, Java ignores the object type and uses only the **reference type**.

---

# Method Hiding

This behavior is known as **Method Hiding**.

The child class defines another static method with the same signature, but it **does not replace** the parent's method.

Both methods exist independently.

---

# Method Hiding vs Method Overriding

| Method Hiding | Method Overriding |
|---------------|-------------------|
| Static methods | Instance methods |
| Compile-time binding | Runtime binding |
| Reference type decides | Object type decides |
| No runtime polymorphism | Supports runtime polymorphism |

---

# Comparison Example

```java
class Parent {

    static void display() {
        System.out.println("Parent Static");
    }

    void show() {
        System.out.println("Parent Instance");
    }
}

class Child extends Parent {

    static void display() {
        System.out.println("Child Static");
    }

    @Override
    void show() {
        System.out.println("Child Instance");
    }
}

public class Main {

    public static void main(String[] args) {

        Parent obj = new Child();

        obj.display();
        obj.show();
    }
}
```

### Output

```text
Parent Static
Child Instance
```

### Why?

#### Static Method

```java
obj.display();
```

Reference type decides.

Output:

```text
Parent Static
```

---

#### Instance Method

```java
obj.show();
```

Object type decides.

Output:

```text
Child Instance
```

---

# Calling Static Methods (Recommended Way)

Although Java allows calling a static method using an object:

```java
Parent obj = new Child();

obj.display();      // ✔ Allowed but not recommended
```

The preferred approach is:

```java
Parent.display();
Child.display();
```

This clearly indicates that the method belongs to the class.

---

# Real-Life Example 🏫

Imagine a school.

Both the **School** and the **Computer Department** have a notice called:

```text
displayNotice()
```

The notice you see depends on **which office you ask**:

- Ask the School → School notice.
- Ask the Department → Department notice.

The department's notice does **not replace** the school's notice.

Similarly, the child's static method **hides** the parent's static method.

---

# Quick Interview Revision

- Static methods are **not overridden**.
- Static methods are **hidden**.
- Static methods use **compile-time binding**.
- The **reference type** determines which static method is called.

---

# Summary Table

| Member | Decided By | Runtime Polymorphism |
|---------|------------|----------------------|
| Instance Variable | Reference Type | ❌ No |
| Static Variable | Reference Type | ❌ No |
| Static Method | Reference Type | ❌ No (Method Hiding) |
| Overridden Instance Method | Object Type | ✅ Yes |

---

#  Explain Dynamic Method Dispatch in Java.

## Definition

**Dynamic Method Dispatch (DMD)** is the mechanism by which Java determines **which overridden method to execute at runtime** based on the **actual object type**, not the reference type.

It is the foundation of **Runtime Polymorphism** in Java.

> **One-line Definition (Interview)**
>
> **Dynamic Method Dispatch is the process of resolving an overridden method call at runtime based on the actual object type.**

---

# How Does It Work?

Suppose:

```java
Parent obj = new Child();
```

Here:

- **Reference Type** → `Parent`
- **Object Type** → `Child`

When an overridden method is called:

```java
obj.show();
```

Java ignores the reference type and checks the **actual object type**.

Since the object is `Child`, Java executes:

```java
Child.show();
```

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

# How Java Resolves the Method

```java
Animal obj = new Dog();
```

Compile Time

```text
Reference Type = Animal

Compiler checks:

Does Animal have sound()?

✔ Yes
```

Runtime

```text
Actual Object = Dog

Dog overrides sound()

↓

Dog.sound() executes
```

---

# Memory Representation

```text
Stack

Animal obj
      │
      ▼

Heap

Dog Object
```

The reference is `Animal`, but the object in memory is `Dog`.

---

# Dynamic Method Dispatch Flow

```text
Method Call

obj.sound()

      │
      ▼

Compiler

Checks Reference Type

      │
      ▼

Runtime

Checks Object Type

      │
      ▼

Calls Child's Overridden Method
```

---

# Important Points

Dynamic Method Dispatch applies **only to overridden instance methods**.

It **does not apply** to:

- Variables
- Static methods
- Constructors

---

# Real-Life Example 🚗

```java
Vehicle v = new Car();
```

When:

```java
v.start();
```

Java checks the object.

If the object is `Car`, then:

```text
Car.start()
```

is executed.

If tomorrow:

```java
v = new Bike();
```

Then:

```text
Bike.start()
```

is executed.

The same reference behaves differently based on the object.

---

# Advantages

- Supports Runtime Polymorphism.
- Makes applications flexible.
- Reduces code duplication.
- Promotes loose coupling.

---

# Quick Interview Revision

- Runtime feature.
- Based on object type.
- Works only for overridden instance methods.
- Foundation of Runtime Polymorphism.

---

# 61. ⭐ What is Upcasting?

## Definition

**Upcasting** is the process of converting a **child class reference into a parent class reference**.

It happens **automatically (implicitly)** and is completely safe.

```java
Parent obj = new Child();
```

Here:

- `Parent` → Reference Type
- `Child` → Object Type

> **One-line Definition (Interview)**
>
> **Upcasting is assigning a child class object to a parent class reference.**

---

# Example

```java
class Animal {

    void sound() {
        System.out.println("Animal");
    }
}

class Dog extends Animal {

    @Override
    void sound() {
        System.out.println("Dog");
    }

    void bark() {
        System.out.println("Bark");
    }
}

public class Main {

    public static void main(String[] args) {

        Animal obj = new Dog();

        obj.sound();

        // obj.bark(); ❌
    }
}
```

### Output

```text
Dog
```

---

# Why Use Upcasting?

- Achieves Runtime Polymorphism.
- Allows generic programming.
- Promotes loose coupling.

---

# Characteristics

- ✔ Implicit (automatic)
- ✔ Safe
- ✔ No cast required
- ✔ Parent reference → Child object

---

# Interview Tip

```java
Animal obj = new Dog();
```

This single line is the most common example of **Upcasting**.

---

# Easy Trick

```text
Child

↓

Parent

= Upcasting
```

# 62. ⭐ What is Downcasting?

## Definition

**Downcasting** is the process of converting a **parent class reference back to a child class reference**.

It is **explicit** and requires a type cast.

```java
Child obj = (Child) parentRef;
```

> **One-line Definition (Interview)**
>
> **Downcasting is converting a parent reference into a child reference using explicit casting.**

---

# Example

```java
class Animal {

    void sound() {
        System.out.println("Animal");
    }
}

class Dog extends Animal {

    void bark() {
        System.out.println("Dog Barks");
    }
}

public class Main {

    public static void main(String[] args) {

        Animal obj = new Dog();     // Upcasting

        Dog d = (Dog) obj;          // Downcasting

        d.bark();
    }
}
```

### Output

```text
Dog Barks
```

---

# Why Do We Need Downcasting?

A parent reference cannot directly access child-specific members.

```java
Animal obj = new Dog();

// obj.bark(); ❌
```

Downcasting gives the reference its child type back.

```java
Dog d = (Dog) obj;

d.bark();
```

---

# Characteristics

- Explicit cast required.
- Used to access child-specific methods.
- Safe only if the object is actually of the child type.

---

# Interview Tip

Always verify the object's type before downcasting.

```java
if (obj instanceof Dog) {

    Dog d = (Dog) obj;

    d.bark();
}
```

---

# Easy Trick

```text
Parent

↓

Child

= Downcasting
```

# 63. When Can Downcasting Cause `ClassCastException`?

## Answer

A **`ClassCastException`** occurs when you try to **downcast a parent reference to a child type that the actual object is not**.

In other words, the cast is valid only if the object was originally created as that child class (or one of its subclasses).

> **One-line Answer (Interview)**
>
> **Downcasting throws `ClassCastException` when the actual object is not an instance of the target child class.**

---

# Correct Downcasting

```java
class Animal { }

class Dog extends Animal {

    void bark() {
        System.out.println("Bark");
    }
}

public class Main {

    public static void main(String[] args) {

        Animal obj = new Dog();

        Dog d = (Dog) obj;

        d.bark();
    }
}
```

### Output

```text
Bark
```

✔ Safe because the object is actually a `Dog`.

---

# Incorrect Downcasting

```java
class Animal { }

class Dog extends Animal { }

class Cat extends Animal { }

public class Main {

    public static void main(String[] args) {

        Animal obj = new Cat();

        Dog d = (Dog) obj;     // ❌ Runtime Exception
    }
}
```

### Runtime Exception

```text
Exception in thread "main"
java.lang.ClassCastException
```

---

# Why Does This Happen?

```java
Animal obj = new Cat();
```

The actual object is:

```text
Cat
```

Trying to convert it into:

```text
Dog
```

is invalid because a `Cat` is **not** a `Dog`.

---

# Safe Way: Using `instanceof`

```java
Animal obj = new Cat();

if (obj instanceof Dog) {

    Dog d = (Dog) obj;

} else {

    System.out.println("Cannot Cast");
}
```

### Output

```text
Cannot Cast
```

Using `instanceof` prevents `ClassCastException`.

---

# Memory Representation

### Safe

```text
Animal obj

      │
      ▼

Dog Object

↓

Dog d = (Dog) obj

✔ Valid
```

---

### Unsafe

```text
Animal obj

      │
      ▼

Cat Object

↓

Dog d = (Dog) obj

❌ ClassCastException
```

---

# Quick Interview Revision

- Downcasting is explicit.
- Safe only if the object is actually of the target child class.
- Invalid downcasting causes `ClassCastException`.
- Use `instanceof` before downcasting.

---

# Interview Follow-up Questions

## Does upcasting throw `ClassCastException`?

**No.**

Upcasting is always safe.

---

## How can we avoid `ClassCastException`?

Use:

```java
instanceof
```

before downcasting.

---

## Is `ClassCastException` a compile-time error?

**No.**

It is a **runtime exception**.

---

# Easy Trick to Remember

```text
Upcasting

✔ Safe

Downcasting

✔ Explicit

❌ Wrong Object → ClassCastException
```

### Mnemonic

> **"Cast Only If the Object Really Is That Child."**
