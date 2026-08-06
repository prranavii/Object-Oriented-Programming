#  What is a Constructor in Java?

## Definition

A **constructor** is a special member of a class that is **automatically called when an object is created**. It is used to **initialize the object's state (instance variables)**.

Unlike methods, a constructor:

- Has the **same name as the class**.
- **Does not have a return type**, not even `void`.
- Is invoked automatically when an object is created using the `new` keyword.

> **One-line Definition (Interview)**
>
> **A constructor is a special member of a class used to initialize objects. It is automatically invoked when an object is created.**
 
---

## Why Do We Need Constructors?

- Initialize object data.
- Assign default or custom values to instance variables.
- Reduce repetitive initialization code.
- Ensure every object starts in a valid state.

---

## Syntax

```java
class ClassName {

    ClassName() {
        // Constructor
    }
}
```

---

# Example

```java
class Student {

    String name;
    int age;

    // Constructor
    Student() {
        name = "John";
        age = 20;
    }

    void display() {
        System.out.println(name);
        System.out.println(age);
    }
}

public class Main {

    public static void main(String[] args) {

        Student s = new Student();

        s.display();
    }
}
```

### Output

```text
John
20
```

---

# Explanation

### Step 1: Constructor Declaration

```java
Student() {
    name = "John";
    age = 20;
}
```

- The constructor has the **same name as the class** (`Student`).
- It initializes the object's instance variables.

---

### Step 2: Object Creation

```java
Student s = new Student();
```

When `new Student()` is executed:

1. Memory is allocated for the object.
2. The constructor is automatically called.
3. The instance variables are initialized.

---

### Step 3: Access the Object

```java
s.display();
```

Displays the initialized values.

---

# Characteristics of a Constructor

- Same name as the class.
- No return type.
- Called automatically during object creation.
- Can be overloaded.
- Cannot be overridden.
- Can have access modifiers (`public`, `private`, `protected`, or package-private).

---

# Types of Constructors

## 1. Default Constructor

A constructor **provided automatically by the Java compiler** if you do not write any constructor.

```java
class Student {

    String name;
    int age;
}
```

The compiler internally creates:

```java
Student() { }
```

---

## 2. No-Argument Constructor

A constructor written by the programmer that takes **no parameters**.

```java
class Student {

    Student() {
        System.out.println("Constructor Called");
    }
}
```

---

## 3. Parameterized Constructor

A constructor that accepts parameters to initialize an object with different values.

```java
class Student {

    String name;
    int age;

    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

public class Main {

    public static void main(String[] args) {

        Student s = new Student("Alice", 22);

        System.out.println(s.name);
        System.out.println(s.age);
    }
}
```

### Output

```text
Alice
22
```

---

# Real-Life Example 🏠

Imagine buying a new house.

When the house is built, it already has:

- Rooms
- Doors
- Windows

These initial settings are done **automatically before you move in**.

Similarly, when an object is created in Java, the **constructor initializes it automatically** before you use it.

---

# Constructor vs Method

| Constructor | Method |
|-------------|--------|
| Initializes an object | Performs an operation |
| Same name as the class | Can have any valid name |
| No return type | Must have a return type (or `void`) |
| Called automatically | Called explicitly |
| Executes once per object creation | Can be called multiple times |
| Cannot be overridden | Can be overridden |

---

# Advantages of Constructors

- Initializes objects automatically.
- Improves code readability.
- Avoids repetitive initialization code.
- Ensures objects are created in a valid state.

---

# Quick Interview Revision

- Constructor initializes an object.
- Same name as the class.
- No return type.
- Called automatically with `new`.
- Can be overloaded.
- Cannot be overridden.

---

# 16. What is the `super` Keyword in Java?

## Definition

The **`super`** keyword is a **reference variable** that refers to the **immediate parent class object**.

It is used to:
- Access the parent class variables.
- Invoke the parent class methods.
- Call the parent class constructor.

> **One-line Definition (Interview)**
>
> **`super` is a reference keyword that refers to the immediate parent class object. It is used to access parent class members and constructors.**

---

# Why Do We Need the `super` Keyword?

- To access parent class variables hidden by child class variables.
- To call overridden methods of the parent class.
- To invoke the parent class constructor.
- To avoid ambiguity between parent and child class members.

---

# 1. Accessing Parent Class Variables

```java
class Animal {

    String color = "White";
}

class Dog extends Animal {

    String color = "Black";

    void display() {
        System.out.println("Child Color : " + color);
        System.out.println("Parent Color: " + super.color);
    }
}

public class Main {

    public static void main(String[] args) {

        Dog d = new Dog();
        d.display();
    }
}
```

### Output

```text
Child Color : Black
Parent Color: White
```

### Explanation

- `color` → Refers to the child class variable.
- `super.color` → Refers to the parent class variable.

---

# 2. Calling Parent Class Methods

```java
class Animal {

    void sound() {
        System.out.println("Animal makes a sound.");
    }
}

class Dog extends Animal {

    @Override
    void sound() {
        System.out.println("Dog barks.");
    }

    void display() {
        super.sound();
        sound();
    }
}

public class Main {

    public static void main(String[] args) {

        Dog d = new Dog();
        d.display();
    }
}
```

### Output

```text
Animal makes a sound.
Dog barks.
```

### Explanation

- `super.sound()` calls the **parent class** method.
- `sound()` calls the **child class** overridden method.

---

# 3. Calling Parent Class Constructor

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
}

public class Main {

    public static void main(String[] args) {

        Dog d = new Dog();
    }
}
```

### Output

```text
Animal Constructor
Dog Constructor
```

### Explanation

When a `Dog` object is created:

1. `super()` calls the `Animal` constructor.
2. The `Animal` constructor executes first.
3. Control returns to the `Dog` constructor.

> **Note:** If you don't explicitly write `super()`, Java inserts it automatically (provided the parent has a no-argument constructor).

---

# Real-Life Example 👨‍👦

Imagine a son asking his father for help.

- The **son** represents the **child class**.
- The **father** represents the **parent class**.

When the son wants to use something that belongs to his father, he refers to his father.

Similarly, in Java:

- `this` → Refers to the current object.
- `super` → Refers to the immediate parent object.

---

# Common Uses of `super`

| Use Case | Example |
|----------|---------|
| Access parent variable | `super.name` |
| Call parent method | `super.display()` |
| Call parent constructor | `super()` |

---

# `this` vs `super`

| `this` | `super` |
|---------|---------|
| Refers to the current object | Refers to the immediate parent object |
| Accesses current class members | Accesses parent class members |
| Calls current class constructor using `this()` | Calls parent constructor using `super()` |

---

# Advantages of `super`

- Accesses hidden parent variables.
- Calls overridden parent methods.
- Invokes parent constructors.
- Helps resolve ambiguity between parent and child members.
- Supports constructor chaining.

---

# Quick Interview Revision

- `super` refers to the **immediate parent class**.
- Used to:
  - Access parent variables.
  - Call parent methods.
  - Call parent constructors.

---

# Interview Follow-up Questions

## Can we use `super` inside a static method?

**No.**

`super` is associated with objects, whereas static methods belong to the class.

```java
class Child extends Parent {

    static void show() {
        super.display();    // ❌ Compile-time Error
    }
}
```

---

## Is `super()` called automatically?

**Yes.**

If you do not explicitly write `super()`, the compiler automatically inserts it as the first statement in the child class constructor, **provided the parent class has a no-argument constructor**.

---

## Can `super()` and `this()` be used together?

**No.**

Both must be the **first statement** in a constructor, so only one can be used.

```java
Child() {
    super();   // ✔
    this();    // ❌ Not Allowed
}
```

---

## Can we use `super` to access private members of the parent class?

**No.**

Private members are **not inherited**, so they cannot be accessed using `super`.

---

# Easy Mnemonic

```text
this  → My Current Object
super → My Parent Object
```

### Remember

- **`this`** → Current object
- **`super`** → Immediate parent object
- **`this()`** → Calls current class constructor
- **`super()`** → Calls parent class constructor


# What are Access Modifiers in Java?

## Definition

**Access Modifiers** are keywords in Java that **control the visibility (accessibility)** of classes, variables, methods, and constructors.

They determine **where a member can be accessed from**.

> **One-line Definition (Interview)**
>
> **Access modifiers are keywords that control the accessibility of classes, methods, variables, and constructors in Java.**

---

# Why Do We Need Access Modifiers?

- Protect data from unauthorized access.
- Support encapsulation.
- Control visibility of class members.
- Improve security and maintainability.

---

# Types of Access Modifiers

Java provides **four access modifiers**:

| Access Modifier | Same Class | Same Package | Subclass (Different Package) | Different Package |
|----------------|:----------:|:------------:|:----------------------------:|:-----------------:|
| **private** | ✅ | ❌ | ❌ | ❌ |
| **default** *(no modifier)* | ✅ | ✅ | ❌ | ❌ |
| **protected** | ✅ | ✅ | ✅ | ❌ |
| **public** | ✅ | ✅ | ✅ | ✅ |

> **Interview Tip:** This table is one of the most frequently asked concepts in Java interviews.

---

# 1. Private

The `private` modifier makes members accessible **only within the same class**.

```java
class Student {

    private String name = "Alice";

    void display() {
        System.out.println(name);   // ✔ Accessible
    }
}
```

❌ Outside the class:

```java
Student s = new Student();
System.out.println(s.name);    // Compile-time Error
```

### Use Case

Use `private` to implement **Encapsulation**.

---

# 2. Default (Package-Private)

When no access modifier is specified, Java uses the **default** access modifier.

Members are accessible **only within the same package**.

```java
class Student {

    String name = "Alice";   // Default access
}
```

✔ Accessible from classes in the **same package**.

❌ Not accessible from a **different package**.

---

# 3. Protected

A `protected` member is accessible:

- Within the same class.
- Within the same package.
- In subclasses, even if they are in different packages.

```java
class Animal {

    protected void sound() {
        System.out.println("Animal Sound");
    }
}

class Dog extends Animal {

    void display() {
        sound();      // ✔ Accessible
    }
}
```

---

# 4. Public

A `public` member is accessible **from anywhere**.

```java
class Student {

    public void display() {
        System.out.println("Hello");
    }
}
```

```java
Student s = new Student();
s.display();     // ✔ Accessible Everywhere
```

---

# Real-Life Example 🏫

Imagine a **school**.

- **Private** → Your personal diary. Only **you** can read it.
- **Default** → Classroom notice board. Only students of that class can see it.
- **Protected** → Family property. Family members (parent/child) can access it.
- **Public** → School website. Everyone can access it.

---

# Advantages of Access Modifiers

- Data Security
- Encapsulation
- Controlled Access
- Better Maintainability
- Better Code Organization

---

## Quick Interview Revision

- **private** → Same Class
- **default** → Same Package
- **protected** → Same Package + Subclass
- **public** → Everywhere

# What is the `static` Keyword in Java?

## Definition

The **`static`** keyword in Java is used to declare members (variables, methods, blocks, and nested classes) that **belong to the class rather than to any specific object**.

This means a static member is **shared by all objects** of the class.

> **One-line Definition (Interview)**
>
> **The `static` keyword is used to create class-level members that are shared among all objects of a class.**

---

# Why Do We Need `static`?

- To share common data among all objects.
- To reduce memory usage.
- To access members without creating an object.
- To define utility methods.

---

# Why is `static` Needed?

Consider the following example:

```java
class Student {

    String name;
    String college = "ABC University";
}
```

Now create three objects:

```java
Student s1 = new Student();
Student s2 = new Student();
Student s3 = new Student();
```

Memory representation:

```text
s1
 ├── name
 └── college = "ABC University"

s2
 ├── name
 └── college = "ABC University"

s3
 ├── name
 └── college = "ABC University"
```

The value `"ABC University"` is stored **three times**, even though it is the same for every student.

This wastes memory.

---

## Using `static`

```java
class Student {

    String name;
    static String college = "ABC University";
}
```

Now the memory looks like this:

```text
             Student Class
        -------------------------
        college = "ABC University"
        -------------------------
               ▲
         ┌─────┼─────┐
         │     │     │
        s1    s2    s3
         │     │     │
       name  name  name
```

The `college` variable is stored **only once** and shared by all objects.

This saves memory.

---

# Static Variable

A **static variable** belongs to the class, not to individual objects.

## Example

```java
class Student {

    String name;
    static String college = "ABC University";

    Student(String name) {
        this.name = name;
    }

    void display() {
        System.out.println(name + " - " + college);
    }

    public static void main(String[] args) {

        Student s1 = new Student("Alice");
        Student s2 = new Student("Bob");

        s1.display();
        s2.display();
    }
}
```

### Output

```text
Alice - ABC University
Bob - ABC University
```

Both objects share the same `college` variable.

---

# Static Method

A **static method** belongs to the class and can be called **without creating an object**.

## Example

```java
class MathUtil {

    static int square(int n) {
        return n * n;
    }

    public static void main(String[] args) {

        System.out.println(MathUtil.square(5));
    }
}
```

### Output

```text
25
```

Notice that we call the method using the class name:

```java
MathUtil.square(5);
```

No object is required.

---

# Why Can't a Static Method Access Non-Static Members?

```java
class Demo {

    int x = 10;

    static void display() {
        System.out.println(x);     // ❌ Compile-time Error
    }
}
```

### Reason

A static method belongs to the **class**, whereas `x` belongs to an **object**.

Since no object exists when the static method is called, Java does not know which object's `x` to access.

---

## Correct Way

```java
class Demo {

    int x = 10;

    static void display() {

        Demo d = new Demo();

        System.out.println(d.x);
    }
}
```

---

# Static Block

A **static block** is executed **only once**, when the class is loaded into memory.

## Example

```java
class Demo {

    static {
        System.out.println("Static Block Executed");
    }

    public static void main(String[] args) {

        System.out.println("Main Method");
    }
}
```

### Output

```text
Static Block Executed
Main Method
```

---

# Static Nested Class

A **static nested class** is a class declared inside another class using the `static` keyword.

```java
class Outer {

    static class Inner {

        void display() {
            System.out.println("Static Nested Class");
        }
    }

    public static void main(String[] args) {

        Outer.Inner obj = new Outer.Inner();

        obj.display();
    }
}
```

---

# Real-Life Example 🏫

Imagine a college.

Every student has:

- Name
- Roll Number

These are **different** for every student.

But all students belong to the **same college**.

Instead of storing the college name in every student object, we store it **once** using `static`.

```text
Student 1 → ABC University
Student 2 → ABC University
Student 3 → ABC University

One Shared Copy ✔
```

---

# Static vs Non-Static

| Static | Non-Static |
|--------|------------|
| Belongs to the class | Belongs to an object |
| Shared by all objects | Separate copy for each object |
| Access using class name | Access using object |
| Loaded when class is loaded | Created when object is created |
| Saves memory | Uses more memory |

---

# Advantages of `static`

- Saves memory.
- Common data is shared.
- No need to create an object for utility methods.
- Improves performance for shared members.

---

# Quick Interview Revision

- `static` belongs to the **class**, not the object.
- Shared among all objects.
- Can be applied to:
  - Variables
  - Methods
  - Blocks
  - Nested Classes
- Access static members using the **class name**.

---

# Interview Follow-up Questions

## Can a static method access non-static variables?

**No.**

A static method belongs to the class, while non-static variables belong to objects.

---

## Can we override static methods?

**No.**

Static methods are **hidden**, not overridden.

---

## Can constructors be static?

**No.**

Constructors are used to initialize objects, whereas `static` belongs to the class.

---

## Can we access a static variable using an object?

**Yes**, but it is **not recommended**.

```java
Student s = new Student();
System.out.println(s.college);    // ✔ Allowed
```

Preferred way:

```java
System.out.println(Student.college);
```

---

## Can a static method call another static method?

**Yes.**

```java
class Demo {

    static void method1() {
        System.out.println("Method 1");
    }

    static void method2() {
        method1();
    }
}
```

---

# Easy Mnemonic

```text
static = Shared by All Objects
```

### Remember

- **Static Variable** → One copy for the entire class.
- **Static Method** → Called using the class name.
- **Static Block** → Executes once when the class is loaded.
- **Static Nested Class** → Nested class that belongs to the outer class.

# What is the Difference Between Static and Instance Methods?

## Definition

### Static Method

A **static method** belongs to the **class**, not to individual objects. It can be called **without creating an object**.

### Instance Method

An **instance method** belongs to an **object** of the class. It can only be called after creating an object.

---

# Example

```java
class Student {

    String name = "Alice";                 // Instance Variable
    static String college = "ABC University"; // Static Variable

    // Instance Method
    void displayName() {
        System.out.println(name);
    }

    // Static Method
    static void displayCollege() {
        System.out.println(college);
    }

    public static void main(String[] args) {

        Student s = new Student();

        s.displayName();          // Instance Method

        Student.displayCollege(); // Static Method
    }
}
```

### Output

```text
Alice
ABC University
```

---

# Explanation

### Instance Method

```java
void displayName()
```

- Belongs to an object.
- Can access both **instance** and **static** members.
- Requires an object to call.

```java
Student s = new Student();
s.displayName();
```

---

### Static Method

```java
static void displayCollege()
```

- Belongs to the class.
- Can directly access only **static** members.
- Can be called using the class name.

```java
Student.displayCollege();
```

---

# Can a Static Method Access Instance Variables?

```java
class Demo {

    int x = 10;

    static void display() {
        System.out.println(x);    // ❌ Compile-time Error
    }
}
```

**Reason:** Static methods belong to the class, while instance variables belong to objects.

---

# Static vs Instance Methods

| Feature | Static Method | Instance Method |
|---------|---------------|-----------------|
| Belongs To | Class | Object |
| Object Required | ❌ No | ✅ Yes |
| Access | `ClassName.method()` | `object.method()` |
| Can Access Static Members | ✅ Yes | ✅ Yes |
| Can Access Instance Members | ❌ Directly No | ✅ Yes |
| Can Use `this` | ❌ No | ✅ Yes |
| Can Be Overridden | ❌ No (Hidden) | ✅ Yes |

---

# Real-Life Example 🏫

- **College Name** → Same for all students → Static Method
- **Student Details** → Different for each student → Instance Method

---

# Quick Interview Revision

- **Static Method** → Class level, no object required.
- **Instance Method** → Object level, object required.
- Static methods cannot directly access instance members.

---

# Interview Questions

### Can a static method call an instance method?

**No**, not directly. An object must be created first.

### Can an instance method call a static method?

**Yes.**

---

## Easy Mnemonic

- **Static Method** → Class
- **Instance Method** → Object

# What is the `final` Keyword in Java?

## Definition

The **`final`** keyword is used to **restrict modification** in Java.

It can be applied to:

- Variables
- Methods
- Classes

> **One-line Definition (Interview)**
>
> **The `final` keyword is used to prevent modification, overriding, or inheritance depending on where it is applied.**

---

# 1. Final Variable

A **final variable** can be assigned a value **only once**.

```java
class Demo {

    final int AGE = 21;

    void display() {
        // AGE = 22;   ❌ Compile-time Error
        System.out.println(AGE);
    }
}
```

---

# 2. Final Method

A **final method** cannot be overridden by a child class.

```java
class Animal {

    final void sound() {
        System.out.println("Animal Sound");
    }
}

class Dog extends Animal {

    // void sound() { }   ❌ Compile-time Error
}
```

---

# 3. Final Class

A **final class** cannot be inherited.

```java
final class Animal { }

// class Dog extends Animal { }   ❌ Compile-time Error
```

---

# Uses of `final`

| Applied To | Meaning |
|------------|---------|
| Variable | Value cannot be changed |
| Method | Cannot be overridden |
| Class | Cannot be inherited |

---

# Real-Life Example 📝

Think of a **government-issued Aadhaar number**.

- Once assigned, it **cannot be changed**.

Similarly, a `final` variable is assigned only once.

---

# Advantages

- Provides immutability.
- Improves security.
- Prevents accidental modification.
- Useful for constants.

---

# Quick Interview Revision

- **Final Variable** → Cannot be reassigned.
- **Final Method** → Cannot be overridden.
- **Final Class** → Cannot be inherited.

---

# Interview Questions

### Can a final variable be initialized later?

**Yes.**

A blank final variable can be initialized in a constructor.

### Can constructors be final?

**No.**

Constructors cannot be declared `final`.

# 25. What is the Difference Between `final`, `finally`, and `finalize()`?

These three terms sound similar but have completely different purposes.

---

# Difference Table

| Feature | `final` | `finally` | `finalize()` |
|---------|---------|-----------|--------------|
| Type | Keyword | Block | Method |
| Purpose | Prevent modification | Executes cleanup code | Invoked by the Garbage Collector before object destruction |
| Used With | Variables, Methods, Classes | `try-catch` | `Object` class |
| Mandatory | No | No | No |
| Called By | Programmer | JVM | Garbage Collector (if invoked) |

---

# 1. `final`

Used to restrict changes.

```java
final int x = 10;

// x = 20;   ❌ Error
```

---

# 2. `finally`

The `finally` block executes **whether an exception occurs or not**.

```java
try {

    int x = 10 / 0;

} catch (Exception e) {

    System.out.println("Exception");

} finally {

    System.out.println("Always Executes");
}
```

### Output

```text
Exception
Always Executes
```

---

# 3. `finalize()`

`finalize()` is a method of the `Object` class that was intended to perform cleanup before an object is garbage collected.

```java
class Demo {

    @Override
    protected void finalize() {

        System.out.println("Finalize Called");
    }
}
```

> **Important:** `finalize()` is **deprecated** and should **not** be used in modern Java. Prefer `try-with-resources` or explicit resource management instead.

---

# Real-Life Example

- **final** → A permanent rule (cannot change).
- **finally** → Cleaning your desk after finishing work, whether work was successful or not.
- **finalize()** → A cleanup service called automatically before disposing of an object (deprecated).

---

# Quick Interview Revision

| Keyword/Method | Meaning |
|---------------|---------|
| `final` | Restricts modification |
| `finally` | Always executes after `try`/`catch` |
| `finalize()` | Deprecated cleanup method called by the Garbage Collector |

---

# Interview Questions

### Does the `finally` block always execute?

**Yes**, except in rare cases such as:
- Calling `System.exit()`
- JVM crash
- Power failure

---

### Can a final method be overloaded?

**Yes.**

A `final` method **cannot be overridden**, but it **can be overloaded**.

---

### Is `finalize()` still recommended?

**No.**

`finalize()` is **deprecated** because its execution is unpredictable. Modern Java recommends **try-with-resources** or explicit cleanup.
