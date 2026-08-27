# Java `static` Keyword — Interview Notes

## 1. What is `static`?

In Java, `static` means that a member belongs to the **class rather than to a particular object**.

### Simple idea

```text
Non-static
    ↓
Each object has its own copy

Static
    ↓
One shared copy belongs to the class
```

The main idea is:

> **Static = Class level**
>
> **Non-static = Object level**

---

# 2. Static Variable

A variable declared using `static` belongs to the class.

```java
class Student {
    String name;
    static String college = "Galgotias University";
}
```

Suppose:

```java
Student s1 = new Student();
Student s2 = new Student();

s1.name = "A";
s2.name = "B";
```

Here:

```text
s1.name → A
s2.name → B
```

Each object has its own `name`.

But:

```text
Student.college → Galgotias University
```

`college` is shared by all Student objects.

If we write:

```java
Student.college = "ABC University";
```

then both students will see:

```text
s1.college → ABC University
s2.college → ABC University
```

### Why?

Because `college` is `static` and belongs to the `Student` class rather than to individual objects.

---

# 3. When Should We Use a Static Variable?

Use a static variable when a value should be **common to all objects**.

Example:

```java
class Student {
    String name;
    static String college = "Galgotias University";
}
```

Here:

- `name` → different for every student
- `college` → common for all students

Another common example is counting objects:

```java
class Student {

    static int count = 0;

    Student() {
        count++;
    }
}
```

Every time a Student object is created, the same `count` variable is increased.

For example:

```java
Student s1 = new Student();
Student s2 = new Student();
Student s3 = new Student();
```

Then:

```text
Student.count = 3
```

because all objects share the same static variable.

---

# 4. Static Method

A method declared using `static` belongs to the class.

Example:

```java
class Calculator {

    static int add(int a, int b) {
        return a + b;
    }
}
```

We can call it using the class name:

```java
int result = Calculator.add(10, 20);
```

We don't need to create an object first.

### Why?

Because the method belongs to the class and does not depend on a particular object.

---

# 5. Static Method vs Non-static Method

### Static method

```java
class Calculator {

    static int add(int a, int b) {
        return a + b;
    }
}
```

Call:

```java
Calculator.add(10, 20);
```

No object is required.

### Non-static method

```java
class Calculator {

    int add(int a, int b) {
        return a + b;
    }
}
```

Call:

```java
Calculator c = new Calculator();

c.add(10, 20);
```

The main difference is:

> **Static method → belongs to class**
>
> **Non-static method → belongs to object**

---

# 6. Why Can't a Static Method Directly Access a Non-static Variable?

This is a very common interview question.

Consider:

```java
class Student {

    String name;

    static void display() {
        System.out.println(name); // ERROR
    }
}
```

This is not allowed.

Why?

```text
display()
    ↓
Static method
    ↓
Belongs to class


name
    ↓
Non-static variable
    ↓
Belongs to object
```

Suppose:

```java
Student s1 = new Student();
s1.name = "A";

Student s2 = new Student();
s2.name = "B";
```

Now:

```java
Student.display();
```

Which `name` should Java use?

```text
s1.name → A
s2.name → B
```

There is no particular object associated with the static method.

Therefore, the static method cannot directly access the instance variable.

### The main reason

A non-static variable belongs to a **specific object**, but a static method belongs to the **class**.

---

# 7. Static Access Rules

Remember this:

```text
Static → Static                  YES
Static → Non-static directly     NO

Non-static → Static              YES
Non-static → Non-static          YES
```

### Why?

A static member belongs to the class.

A non-static member belongs to an object.

---

# 8. Can a Static Method Access a Static Variable?

Yes.

```java
class Student {

    static String college = "GU";

    static void display() {
        System.out.println(college);
    }
}
```

Both belong to the class.

Therefore:

```text
Static method
      ↓
Static variable
      ↓
Both are class-level
      ↓
Allowed
```

---

# 9. Can a Non-static Method Access a Static Variable?

Yes.

```java
class Student {

    static String college = "GU";

    void display() {
        System.out.println(college);
    }
}
```

This works because an instance method can access class-level static members.

---

# 10. How Can a Static Method Access a Non-static Variable?

A static method can access a non-static variable **through an object**.

Example:

```java
class Student {

    String name;

    static void display(Student s) {
        System.out.println(s.name);
    }
}
```

Then:

```java
Student s1 = new Student();

s1.name = "Pranavi";

Student.display(s1);
```

Here, `s1` tells the static method exactly which object's `name` should be accessed.

Important:

> A static method cannot directly access an instance member, but it can access it through an object reference.

---

# 11. `this` Inside a Static Method

We cannot use `this` directly inside a static method.

Example:

```java
class Student {

    static void display() {
        System.out.println(this); // ERROR
    }
}
```

### Why?

`this` refers to the **current object**.

But a static method belongs to the class and is not associated with a particular object.

Therefore:

```text
this
 ↓
Current object

static
 ↓
Class level
```

There is no particular current object for `this` to refer to.

### Interview answer

> "`this` cannot be used directly inside a static context because `this` refers to the current object, while static members belong to the class."

---

# 12. Static Block

A static block is used for **static/class-level initialization**.

Example:

```java
class Test {

    static int a = 4;
    static int b;

    static {

        System.out.println("Static block");

        b = a * 5;
    }

    public static void main(String[] args) {

        System.out.println(b);
    }
}
```

Output:

```text
Static block
20
```

The static block runs when the class is initialized.

### Important point

A static block runs **once during class initialization**, not once for every object.

For example:

```java
Test obj1 = new Test();
Test obj2 = new Test();
```

The static block does not run separately for `obj1` and `obj2`.

---

# 13. Why is `main()` Static?

The standard Java entry point is:

```java
public static void main(String[] args)
```

The JVM needs to invoke `main()` as the entry point without first creating an object of the class.

Because `main()` is static, it can be called at the class level.

### Interview answer

> "`main()` is static because the JVM needs to invoke it without creating an object of the class first."

---

# 14. Static Initialization

Example:

```java
class Test {

    static int a = 4;
    static int b;

    static {

        b = a * 5;
    }
}
```

Here:

```text
a → static variable
b → static variable
static block → initializes b
```

Static initialization is associated with the class rather than individual objects.

Remember:

> **Static initialization is associated with the class, not individual objects.**

---

# 15. Can a Static Method Be Overridden?

Static methods are **not overridden in the normal runtime-polymorphism sense**.

If a child class declares a static method with the same signature, it is called **method hiding**.

Example:

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

This is called method hiding.

Compare this with normal overriding:

```java
class Parent {

    void display() {
        System.out.println("Parent");
    }
}

class Child extends Parent {

    @Override
    void display() {
        System.out.println("Child");
    }
}
```

The second example is normal method overriding.

### Remember

```text
Instance method
      ↓
Overriding


Static method
      ↓
Method hiding
```

---

# 16. Static and Object Creation

A static method does not require an object to be called.

Example:

```java
class Calculator {

    static int add(int a, int b) {
        return a + b;
    }
}
```

Call:

```java
Calculator.add(10, 20);
```

No object is required.

However, a static method CAN create an object.

Example:

```java
class Test {

    static void createObject() {

        Test obj = new Test();

        System.out.println("Object created");
    }
}
```

So remember:

> "Static methods don't require an object to be called."

This does NOT mean:

> "Static methods cannot create or use objects."

They can use objects when an object reference is available.

---

# 17. Static Nested Class

Java also allows a nested class to be static.

```java
class Outer {

    static class Inner {

        void display() {
            System.out.println("Hello");
        }
    }
}
```

It can be used as:

```java
Outer.Inner obj = new Outer.Inner();

obj.display();
```

This is a lower-priority topic for a fresher interview compared with static variables, methods, blocks, and `main()`.

---

# 18. Static vs Non-static

| Static | Non-static |
|---|---|
| Belongs to the class | Belongs to an object |
| Shared at class level | Each object has its own copy |
| Can be accessed using class name | Usually accessed using object |
| Does not require an object for direct access | Requires an object for instance access |
| Static method cannot directly access instance members | Instance method can access instance members |

---

# 19. Real-world Example

Imagine a Student class:

```java
class Student {

    String name;
    int age;

    static String college = "Galgotias University";
}
```

Suppose:

```java
Student s1 = new Student();
Student s2 = new Student();
```

The students have different:

```text
s1.name
s2.name

s1.age
s2.age
```

But they share:

```text
Student.college
```

Therefore:

```text
Individual information
        ↓
name, age
        ↓
Non-static


Common information
        ↓
college
        ↓
Static
```

---

# 20. How to Decide Whether Something Should Be Static

Ask yourself:

> "Does this need to belong to one particular object, or should it be common to the whole class?"

### If it is common → static

```java
static String college;
static int population;
```

### If it is specific to an object → non-static

```java
String name;
int age;
```

---

# 21. Common Interview Questions

### Q1. What is `static` in Java?

> "`static` is a keyword used to make a variable, method, or block belong to the class rather than individual objects."

### Q2. What is a static variable?

> "A static variable belongs to the class and is shared among the objects of that class."

### Q3. What is a static method?

> "A static method belongs to the class and can be called without creating an object."

### Q4. Can a static method directly access a non-static variable?

> "No. A static method belongs to the class, while a non-static variable belongs to a specific object."

### Q5. Can a static method access a static variable?

> "Yes."

### Q6. Can a non-static method access a static variable?

> "Yes."

### Q7. Can we use `this` inside a static method?

> "No, because `this` refers to the current object, while a static method belongs to the class."

### Q8. Why is `main()` static?

> "Because the JVM needs to invoke the main method without creating an object first."

### Q9. What is a static block?

> "A static block is used for static/class-level initialization and executes when the class is initialized."

### Q10. Can a static method be overridden?

> "Static methods are not overridden in the normal runtime-polymorphism sense. A same-signature static method in a child class is method hiding."

---

# 22. Quick Revision

Remember these five points:

1. **static → class-level**
2. **Static variable → shared among objects**
3. **Static method → can be called without creating an object**
4. **Static method cannot directly access instance members**
5. **main() is static because JVM invokes it without creating the class object first**

### One-line definition

> **`static` makes a member belong to the class rather than to individual objects.**

---

# 23. Self-Test

Try answering these without looking at the notes:

1. What does `static` mean?
2. What is the difference between a static and instance variable?
3. Why do we use static variables?
4. Can a static method access a non-static variable directly? Why?
5. Can a non-static method access a static variable?
6. Why is `main()` static?
7. What is a static block?
8. Can a static method use `this`?
9. Can a static method create an object?
10. Can a static method be overridden?
11. What is method hiding?
12. When should you use `static`?

## Final Memory Trick

```text
STATIC
  ↓
CLASS LEVEL
  ↓
Shared / does not depend on one particular object

NON-STATIC
  ↓
OBJECT LEVEL
  ↓
Belongs to a particular object
```

> **Static = Class**
>
> **Non-static = Object**
