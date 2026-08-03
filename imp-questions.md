# 78. What is the Difference Between `==` and `equals()`?

## Definition

Both `==` and `equals()` are used to compare values in Java, but they compare **different things**.

- `==` compares **references** (memory addresses) for objects.
- `equals()` compares the **contents (logical equality)** of objects.

> **One-line Answer (Interview)**
>
> **`==` checks whether two references point to the same object, whereas `equals()` checks whether two objects are logically equal based on their contents.**

---

# Difference Between `==` and `equals()`

| `==` | `equals()` |
|------|------------|
| Operator | Method |
| Compares references for objects | Compares object contents (logical equality) |
| Cannot be overridden | Can be overridden |
| Used for primitives and object references | Used only for objects |
| Faster | May involve custom comparison logic |

---

# Example 1: Primitive Types

```java
int a = 10;
int b = 10;

System.out.println(a == b);
```

### Output

```text
true
```

### Why?

For primitive types, `==` compares the **actual values**.

---

# Example 2: Objects

```java
String s1 = new String("Java");
String s2 = new String("Java");

System.out.println(s1 == s2);

System.out.println(s1.equals(s2));
```

### Output

```text
false
true
```

### Explanation

```java
s1 == s2
```

Compares memory addresses.

Since `new` creates two different objects:

```text
false
```

---

```java
s1.equals(s2)
```

`String` overrides `equals()` to compare the text inside the strings.

Both contain `"Java"`.

```text
true
```

---

# Memory Representation

```java
String s1 = new String("Java");
String s2 = new String("Java");
```

```text
Stack

s1 ───────► Object1 ("Java")

s2 ───────► Object2 ("Java")
```

Different objects:

```java
s1 == s2
```

↓

```text
false
```

Same contents:

```java
s1.equals(s2)
```

↓

```text
true
```

---

# Example 3: Custom Class

```java
class Student {

    int id;

    Student(int id) {
        this.id = id;
    }
}

public class Main {

    public static void main(String[] args) {

        Student s1 = new Student(1);
        Student s2 = new Student(1);

        System.out.println(s1 == s2);

        System.out.println(s1.equals(s2));
    }
}
```

### Output

```text
false
false
```

### Why?

The `Student` class does **not** override `equals()`.

So it inherits `Object.equals()`, which behaves like `==` (reference comparison).

---

# Overriding `equals()`

```java
class Student {

    int id;

    Student(int id) {
        this.id = id;
    }

    @Override
    public boolean equals(Object obj) {

        Student s = (Student) obj;

        return this.id == s.id;
    }
}
```

Now:

```java
Student s1 = new Student(1);
Student s2 = new Student(1);

System.out.println(s1.equals(s2));
```

### Output

```text
true
```

Because the comparison is based on `id`.

---

# String Pool Example

```java
String s1 = "Java";
String s2 = "Java";

System.out.println(s1 == s2);
```

### Output

```text
true
```

Both references point to the **same object** in the String Pool.

---

# Real-Life Example 🆔

Imagine two people.

Both have:

- Same Name
- Same Age

But different Aadhaar numbers.

`==` asks:

> Are they the **same person**?

`equals()` asks:

> Do they have the **same details** according to the comparison logic?

---

# Advantages of `equals()`

- Enables logical comparison.
- Used by collections such as `HashSet` and `HashMap`.
- Can be customized by overriding.

---

# Quick Interview Revision

- `==` compares references (or primitive values).
- `equals()` compares object contents.
- `String` overrides `equals()`.
- `Object.equals()` behaves like `==`.

---

# Interview Follow-up Questions

## Can `equals()` be overridden?

**Yes.**

---

## Can `==` be overridden?

**No.**

It is an operator.

---

## Which one compares memory addresses?

`==`

---

## Which one compares object contents?

`equals()`

---

# Easy Trick to Remember

```text
==

↓

Same Object?

equals()

↓

Same Content?
```

### Mnemonic

> **"`==` Checks Identity, `equals()` Checks Equality."**

# 79. ⭐ What is the Contract Between `equals()` and `hashCode()`?

## Definition

The **`equals()` and `hashCode()` contract** is a rule defined by Java that ensures objects behave correctly in hash-based collections such as `HashMap`, `HashSet`, and `Hashtable`.

> **One-line Answer (Interview)**
>
> **If two objects are equal according to `equals()`, they must return the same `hashCode()`.**

---

# The Contract

### Rule 1

If:

```java
a.equals(b)
```

is

```text
true
```

then:

```java
a.hashCode() == b.hashCode()
```

**must also be true.**

---

### Rule 2

If two objects have the same hash code:

```java
a.hashCode() == b.hashCode()
```

they **may or may not** be equal.

Same hash code **does not guarantee** equality because of **hash collisions**.

---

### Rule 3

If:

```java
a.equals(b)
```

is

```text
false
```

their hash codes **can** be different or even the same.

---

# Why Is This Contract Important?

Hash-based collections first use `hashCode()` to locate the bucket, then use `equals()` to verify whether two objects are actually equal.

If the contract is violated, collections like `HashMap` and `HashSet` may behave incorrectly.

---

# Example Without Overriding

```java
class Student {

    int id;

    Student(int id) {
        this.id = id;
    }
}

public class Main {

    public static void main(String[] args) {

        Student s1 = new Student(1);
        Student s2 = new Student(1);

        System.out.println(s1.equals(s2));
        System.out.println(s1.hashCode());
        System.out.println(s2.hashCode());
    }
}
```

### Output (Example)

```text
false
12345678
87654321
```

Since `Student` inherits `Object`'s implementations:

- `equals()` compares references.
- `hashCode()` is based on object identity.

---

# Correct Implementation

```java
import java.util.Objects;

class Student {

    int id;

    Student(int id) {
        this.id = id;
    }

    @Override
    public boolean equals(Object obj) {

        if (this == obj)
            return true;

        if (!(obj instanceof Student))
            return false;

        Student s = (Student) obj;

        return id == s.id;
    }

    @Override
    public int hashCode() {
        return Objects.hash(id);
    }
}
```

Now:

```java
Student s1 = new Student(1);
Student s2 = new Student(1);

System.out.println(s1.equals(s2));
System.out.println(s1.hashCode());
System.out.println(s2.hashCode());
```

### Output

```text
true
32
32
```

Both objects are logically equal and produce the same hash code.

---

# How `HashSet` Uses Them

When adding an object:

```text
Step 1

hashCode()

↓

Find Bucket

↓

Step 2

equals()

↓

Check Duplicate

↓

Insert or Reject
```

Both methods work together.

---

# Memory Representation

```text
Student(1)

↓

hashCode()

↓

Bucket #5

↓

equals()

↓

Duplicate?

↓

Yes → Don't Add

No → Add
```

---

# Real-Life Example 📬

Imagine postal delivery.

- **Hash Code** → Postal code (helps locate the correct area quickly).
- **equals()** → House number (confirms the exact destination).

Two people may share the same postal code but still live in different houses.

Similarly, two objects can have the same hash code but not be equal.

---

# Advantages

- Ensures correct behavior in `HashMap` and `HashSet`.
- Improves search performance.
- Prevents duplicate logical objects.

---

# Quick Interview Revision

- Equal objects **must** have equal hash codes.
- Same hash code **does not necessarily** mean equal objects.
- Always override `hashCode()` when overriding `equals()`.

---

# Interview Follow-up Questions

## Why should `hashCode()` be overridden with `equals()`?

To maintain the Java contract and ensure correct behavior in hash-based collections.

---

## Can two unequal objects have the same hash code?

**Yes.**

This is called a **hash collision**.

---

## Can two equal objects have different hash codes?

**No.**

That violates the contract.

---

## Which collections depend on this contract?

- `HashMap`
- `HashSet`
- `Hashtable`
- `LinkedHashMap`
- `ConcurrentHashMap`

---

# Easy Trick to Remember

```text
equals() == true

↓

hashCode() MUST be same

Same hashCode()

↓

equals()

May be true or false
```

### Mnemonic

> **"Equal Objects → Equal Hash Codes, But Equal Hash Codes ≠ Equal Objects."**

# 80. What Happens if You Override `equals()` but Not `hashCode()`?

## Answer

If you **override `equals()` but do not override `hashCode()`**, you **break the Java contract between `equals()` and `hashCode()`**.

As a result, hash-based collections such as **`HashMap`**, **`HashSet`**, and **`Hashtable`** may behave incorrectly.

> **One-line Answer (Interview)**
>
> **Overriding `equals()` without overriding `hashCode()` violates the Java contract, causing hash-based collections to fail in identifying logically equal objects.**

---

# Why Does This Happen?

According to Java's contract:

> **If two objects are equal according to `equals()`, they must return the same `hashCode()`.**

If you override only `equals()`, two logically equal objects may still have different hash codes because they inherit the default `hashCode()` implementation from the `Object` class.

---

# Example

```java
class Student {

    int id;

    Student(int id) {
        this.id = id;
    }

    @Override
    public boolean equals(Object obj) {

        if (this == obj)
            return true;

        if (!(obj instanceof Student))
            return false;

        Student s = (Student) obj;

        return this.id == s.id;
    }

    // hashCode() NOT overridden
}
```

```java
import java.util.HashSet;

public class Main {

    public static void main(String[] args) {

        HashSet<Student> set = new HashSet<>();

        Student s1 = new Student(101);
        Student s2 = new Student(101);

        set.add(s1);
        set.add(s2);

        System.out.println(set.size());
    }
}
```

### Output

```text
2
```

---

# Why?

Although:

```java
s1.equals(s2)
```

returns

```text
true
```

their hash codes are different because `hashCode()` is inherited from `Object`.

```text
s1.hashCode() = 12345

s2.hashCode() = 67890
```

HashSet places them in different buckets.

Since they are never compared using `equals()`, both objects are stored.

---

# Correct Implementation

```java
import java.util.Objects;

class Student {

    int id;

    Student(int id) {
        this.id = id;
    }

    @Override
    public boolean equals(Object obj) {

        if (this == obj)
            return true;

        if (!(obj instanceof Student))
            return false;

        Student s = (Student) obj;

        return id == s.id;
    }

    @Override
    public int hashCode() {
        return Objects.hash(id);
    }
}
```

Now:

```java
HashSet<Student> set = new HashSet<>();

set.add(new Student(101));
set.add(new Student(101));

System.out.println(set.size());
```

### Output

```text
1
```

Both objects have the same hash code and are considered duplicates.

---

# Why is This a Problem?

Collections like `HashSet` and `HashMap` first use:

```text
hashCode()

↓

Find Bucket

↓

equals()

↓

Check Equality
```

If equal objects have different hash codes, they end up in different buckets.

`equals()` is never called.

---

# Memory Representation

### Without Overriding `hashCode()`

```text
Student(101)

↓

hashCode() = 123

↓

Bucket 3
```

```text
Student(101)

↓

hashCode() = 890

↓

Bucket 8
```

Different buckets.

Duplicate objects are stored.

---

### With Proper `hashCode()`

```text
Student(101)

↓

hashCode() = 50

↓

Bucket 5
```

```text
Student(101)

↓

hashCode() = 50

↓

Bucket 5

↓

equals()

↓

Duplicate Found

↓

Not Added
```

---

# Real-Life Example 📬

Imagine two houses have the **same address** (`equals()` returns `true`), but the postal system assigns them **different PIN codes** (`hashCode()`).

The mail carrier will deliver them to different locations.

Similarly, `HashMap` and `HashSet` cannot locate equal objects correctly.

---

# Best Practice

✅ Whenever you override `equals()`, **always override `hashCode()`**.

---

# Quick Interview Revision

- Overriding only `equals()` breaks the Java contract.
- Equal objects may have different hash codes.
- Hash-based collections behave incorrectly.
- Always override both methods together.

---

# Interview Follow-up Questions

## Can equal objects have different hash codes?

**No.**

This violates the Java contract.

---

## What happens in a `HashSet` if `hashCode()` isn't overridden?

Duplicate logical objects may be stored.

---

## Should `equals()` and `hashCode()` always be overridden together?

**Yes.**

---

# Easy Trick to Remember

```text
Override equals()

↓

Also Override hashCode()

↓

Otherwise

HashMap / HashSet Problems
```

### Mnemonic

> **"Override One, Override the Other."**

# 81. Why are `equals()` and `hashCode()` Important for `HashMap` and `HashSet`?

## Answer

`HashMap` and `HashSet` use **both `hashCode()` and `equals()`** to store, search, and remove objects efficiently.

- **`hashCode()`** determines the **bucket** where an object should be stored.
- **`equals()`** checks whether two objects in the same bucket are logically equal.

> **One-line Answer (Interview)**
>
> **`hashCode()` finds the correct bucket, and `equals()` checks whether the objects are logically equal. Both are essential for the correct functioning of `HashMap` and `HashSet`.**

---

# How `HashSet` Works

Suppose:

```java
HashSet<Student> set = new HashSet<>();

set.add(student);
```

Java performs these steps:

```text
Step 1

Call hashCode()

↓

Find Bucket

↓

Step 2

Call equals()

↓

Duplicate?

↓

Yes → Don't Add

No → Add Object
```

---

# Example

```java
import java.util.HashSet;
import java.util.Objects;

class Student {

    int id;

    Student(int id) {
        this.id = id;
    }

    @Override
    public boolean equals(Object obj) {

        if (this == obj)
            return true;

        if (!(obj instanceof Student))
            return false;

        Student s = (Student) obj;

        return id == s.id;
    }

    @Override
    public int hashCode() {
        return Objects.hash(id);
    }
}

public class Main {

    public static void main(String[] args) {

        HashSet<Student> set = new HashSet<>();

        set.add(new Student(101));
        set.add(new Student(101));

        System.out.println(set.size());
    }
}
```

### Output

```text
1
```

---

# How `HashMap` Works

Suppose:

```java
HashMap<Student, String> map = new HashMap<>();

map.put(student, "Pranavi");
```

Java performs:

```text
hashCode()

↓

Find Bucket

↓

equals()

↓

Existing Key?

↓

Yes → Replace Value

No → Insert New Entry
```

---

# Search Operation

When searching:

```java
map.get(student);
```

Java again performs:

```text
hashCode()

↓

Locate Bucket

↓

equals()

↓

Find Exact Key

↓

Return Value
```

---

# Memory Representation

```text
hashCode()

↓

Bucket 5

↓

Student(101)

↓

equals()

↓

Same Student?

↓

Return Value
```

---

# What if `hashCode()` is Wrong?

```text
Different Hash Codes

↓

Different Buckets

↓

equals() Never Called

↓

Duplicate Objects
```

This causes incorrect behavior in `HashMap` and `HashSet`.

---

# Real-Life Example 📬

Think of a postal system.

- **PIN Code** → `hashCode()` (quickly identifies the delivery area)
- **House Number** → `equals()` (identifies the exact house)

Without the correct PIN code, the delivery person may never reach the correct neighborhood.

Similarly, without a proper `hashCode()`, Java may never compare equal objects using `equals()`.

---

# Advantages

- Fast searching.
- Efficient insertion.
- Efficient deletion.
- Prevents duplicate keys in `HashMap`.
- Prevents duplicate elements in `HashSet`.

---

# Quick Interview Revision

- `hashCode()` → Finds the bucket.
- `equals()` → Confirms logical equality.
- Both methods work together.
- Essential for all hash-based collections.

---

# Interview Follow-up Questions

## Which method is called first?

**`hashCode()`**

---

## When is `equals()` called?

Only if two objects are in the **same bucket** (same hash code).

---

## What happens if two objects have different hash codes?

They go into different buckets.

`equals()` is usually not called between them.

---

## Which collections depend on these methods?

- `HashMap`
- `HashSet`
- `Hashtable`
- `LinkedHashMap`
- `ConcurrentHashMap`

---

# Easy Trick to Remember

```text
HashMap / HashSet

hashCode()

↓

Bucket

↓

equals()

↓

Exact Object
```

### Mnemonic

> **"`hashCode()` Finds, `equals()` Confirms."**

# 88. What is the Difference Between Shallow Copy and Deep Copy?

## Definition

Copying an object means creating another object with the same data.

There are two types of object copying in Java:

1. **Shallow Copy**
2. **Deep Copy**

The main difference is **how reference-type (non-primitive) fields are copied**.

> **One-line Answer (Interview)**
>
> **A shallow copy copies object references, so both objects share the same referenced objects. A deep copy creates copies of the referenced objects as well, making the two objects completely independent.**

---

# Shallow Copy

## Definition

A **shallow copy** creates a new object but **copies the references** of nested objects instead of creating new copies of them.

As a result:

- Primitive fields are copied.
- Reference fields point to the **same objects**.

Changes made to a shared referenced object are visible in both copies.

---

# Example

```java
class Address {

    String city;

    Address(String city) {
        this.city = city;
    }
}

class Student {

    String name;
    Address address;

    Student(String name, Address address) {
        this.name = name;
        this.address = address;
    }
}

public class Main {

    public static void main(String[] args) {

        Address a1 = new Address("Delhi");

        Student s1 = new Student("Pranavi", a1);

        // Shallow Copy
        Student s2 = new Student(s1.name, s1.address);

        s2.address.city = "Noida";

        System.out.println(s1.address.city);
        System.out.println(s2.address.city);
    }
}
```

### Output

```text
Noida
Noida
```

---

# Why?

Both objects share the **same `Address` object**.

Memory Representation:

```text
s1 ------------------┐
                     │
                     ▼
                Address("Delhi")
                     ▲
                     │
s2 ------------------┘
```

After changing:

```java
s2.address.city = "Noida";
```

Both objects see the updated value.

---

# Deep Copy

## Definition

A **deep copy** creates a **new object** and also creates **new copies of all referenced objects**.

As a result:

- Primitive fields are copied.
- Reference fields are also copied into **new objects**.

Both objects become completely independent.

---

# Example

```java
class Address {

    String city;

    Address(String city) {
        this.city = city;
    }
}

class Student {

    String name;
    Address address;

    Student(String name, Address address) {
        this.name = name;
        this.address = address;
    }
}

public class Main {

    public static void main(String[] args) {

        Address a1 = new Address("Delhi");

        Student s1 = new Student("Pranavi", a1);

        // Deep Copy
        Student s2 = new Student(
                s1.name,
                new Address(s1.address.city)
        );

        s2.address.city = "Noida";

        System.out.println(s1.address.city);
        System.out.println(s2.address.city);
    }
}
```

### Output

```text
Delhi
Noida
```

---

# Why?

A **new `Address` object** is created.

Memory Representation:

```text
s1 -------------> Address("Delhi")

s2 -------------> Address("Delhi")
```

Now both objects have different `Address` objects.

Changing one does not affect the other.

---

# Comparison

## Shallow Copy

```text
Student s1

        │
        ▼

   Address Object

        ▲
        │

Student s2
```

Both share the same nested object.

---

## Deep Copy

```text
Student s1

        │
        ▼

 Address Object 1


Student s2

        │
        ▼

 Address Object 2
```

Each object has its own copy.

---

# Shallow Copy vs Deep Copy

| Feature | Shallow Copy | Deep Copy |
|----------|--------------|-----------|
| New Object Created | ✅ Yes | ✅ Yes |
| Primitive Fields | Copied | Copied |
| Reference Fields | References are copied | New referenced objects are created |
| Shared Nested Objects | ✅ Yes | ❌ No |
| Changes Affect Original | ✅ Yes | ❌ No |
| Memory Usage | Less | More |
| Performance | Faster | Slower |

---

# Real-Life Example 📚

Imagine photocopying a notebook.

### Shallow Copy

You make a copy of the cover page, but both notebooks contain a **shared removable page**.

If someone edits that shared page, **both notebooks reflect the change**.

---

### Deep Copy

You photocopy **every page**.

Now each notebook is completely independent.

Editing one notebook does not affect the other.

---

# Advantages

## Shallow Copy

- Faster.
- Uses less memory.
- Suitable when shared objects are acceptable.

---

## Deep Copy

- Objects are completely independent.
- Prevents accidental modifications.
- Safer for mutable objects.

---

# Quick Interview Revision

- **Shallow Copy** → Copies references.
- **Deep Copy** → Copies the entire object graph.
- Shallow copy shares nested objects.
- Deep copy creates independent nested objects.

---

# Interview Follow-up Questions

## Which copy is created by `Object.clone()`?

By default, `Object.clone()` performs a **shallow copy**.

---

## Which copy is safer?

**Deep Copy**, because changes to one object do not affect the other.

---

## Which copy uses more memory?

**Deep Copy**, because it creates additional objects.

---

## When should you use Deep Copy?

When objects contain **mutable reference fields** that should not be shared.

---

# Easy Trick to Remember

```text
Shallow Copy

Object
   │
   ▼
Shared References

Deep Copy

Object
   │
   ▼
New References
```

### Mnemonic

> **"Shallow Shares, Deep Duplicates."**

# 90. What is an Immutable Class?

## Definition

An **immutable class** is a class whose **objects cannot be modified after they are created**.

Once an object is initialized, its state (data) remains **unchanged** throughout its lifetime.

If you want different values, you must create a **new object** instead of modifying the existing one.

> **One-line Definition (Interview)**
>
> **An immutable class is a class whose objects cannot be changed after creation.**

---

# Why Do We Need Immutable Classes?

Immutable objects are:

- Safe to share between multiple threads.
- Easy to use because they cannot change unexpectedly.
- More secure since data cannot be modified.
- Frequently used as keys in collections like `HashMap`.

The best example is the **`String`** class.

---

# Characteristics of an Immutable Class

An immutable class should follow these rules:

1. Declare the class as `final`.
2. Make all fields `private` and `final`.
3. Do not provide setter methods.
4. Initialize fields using a constructor.
5. Provide only getter methods.
6. If the class contains mutable objects, return **defensive copies** instead of the original objects.

---

# Example

```java
final class Student {

    private final int id;
    private final String name;

    public Student(int id, String name) {
        this.id = id;
        this.name = name;
    }

    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }
}

public class Main {

    public static void main(String[] args) {

        Student s = new Student(101, "Pranavi");

        System.out.println(s.getId());
        System.out.println(s.getName());

        // s.setName("Riya");   // ❌ No setter available
    }
}
```

### Output

```text
101
Pranavi
```

The object's data cannot be modified after creation.

---

# Why Make the Class `final`?

```java
final class Student { }
```

This prevents inheritance.

If inheritance were allowed, a subclass could add setter methods or modify the object's behavior, breaking immutability.

---

# Why Make Fields `private final`?

```java
private final String name;
```

- **private** → Prevents direct access from outside the class.
- **final** → Ensures the field can be assigned only once.

---

# Why No Setter Methods?

Setter methods allow modification.

```java
public void setName(String name) {
    this.name = name;
}
```

❌ This would make the class mutable.

Therefore, immutable classes provide **only getter methods**.

---

# Mutable Object Example

Suppose the class contains an `Address` object.

### Incorrect Implementation

```java
class Address {

    String city;

    Address(String city) {
        this.city = city;
    }
}

final class Student {

    private final Address address;

    Student(Address address) {
        this.address = address;
    }

    public Address getAddress() {
        return address;    // ❌ Returns original object
    }
}
```

Now:

```java
Student s = new Student(new Address("Delhi"));

s.getAddress().city = "Noida";
```

The internal state changes, so the class is **not truly immutable**.

---

# Correct Implementation (Defensive Copy)

```java
class Address {

    String city;

    Address(String city) {
        this.city = city;
    }
}

final class Student {

    private final Address address;

    Student(Address address) {
        this.address = new Address(address.city);
    }

    public Address getAddress() {
        return new Address(address.city);
    }
}
```

Now the original object cannot be modified from outside.

---

# Memory Representation

```java
Student s

│

├── id = 101

└── name = "Pranavi"
```

After creation:

```text
No Changes Allowed
```

If you need different values:

```java
Student s2 = new Student(102, "Riya");
```

A **new object** is created.

---

# Real-Life Example 🛂

Think of a **passport**.

Once it is issued, details like:

- Passport Number
- Date of Birth
- Name

cannot be modified directly.

If changes are required, a **new passport** is issued.

Similarly, immutable objects are never modified—new objects are created instead.

---

# Advantages

- Thread-safe.
- Easy to cache and share.
- Prevents accidental modification.
- Reliable as keys in `HashMap`.
- Simplifies debugging.

---

# Examples of Immutable Classes in Java

- `String`
- Wrapper classes (`Integer`, `Long`, `Double`, etc.)
- `LocalDate`
- `LocalTime`
- `BigInteger`
- `BigDecimal`

---

# Immutable Class vs Mutable Class

| Immutable Class | Mutable Class |
|-----------------|---------------|
| Object cannot change | Object can change |
| No setters | Has setters |
| Fields are `final` | Fields may change |
| Thread-safe | May require synchronization |
| Example: `String` | Example: `StringBuilder` |

---

# Quick Interview Revision

- Objects cannot be modified after creation.
- Class is usually `final`.
- Fields are `private final`.
- No setter methods.
- Use defensive copies for mutable fields.

---

# Interview Follow-up Questions

## Why is `String` immutable?

To improve security, thread safety, performance (string pool), and caching.

---

## Can an immutable class contain mutable objects?

**Yes**, but it must use **defensive copying** to protect its internal state.

---

## Why should immutable classes be `final`?

To prevent subclasses from modifying their behavior or state.

---

## Can immutable objects be shared between threads?

**Yes.**

Since their state never changes, they are inherently thread-safe.

---

# Easy Trick to Remember

```text
Immutable Class

✔ final Class
✔ private final Fields
✔ No Setters
✔ Constructor Initialization
✔ Only Getters
```

### Mnemonic

> **"Create Once, Never Change."**
