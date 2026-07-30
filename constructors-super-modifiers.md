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


# 19. What are Access Modifiers in Java?

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

# Quick Interview Revision

- **private** → Same Class
- **default** → Same Package
- **protected** → Same Package + Subclass
- **public** → Everywhere
