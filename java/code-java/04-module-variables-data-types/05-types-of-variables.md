## 5. Types of Variables
Java has three types of variables based on **scope** and **lifetime**:

---

#### 5.1. Local Variables
**Definition:** Variables declared inside a **method**, **constructor**, or **block**.

###### Characteristics:
- **Scope:** Only accessible within the declaring block
- **Lifetime:** Created when the block executes, destroyed when it exits
- **Storage:** Stack memory
- **Initialization:** No default value—must initialize before use
- **Access modifiers:** Not allowed (no public, private, etc.)

**Example:**

```java
public void calculate() {
    int result; // Local variable
    result = 10 + 5; // Must initialize before use
    System.out.println(result);
} // 'result' is destroyed here
```

**Interview Insight:** Local variables are **thread-safe** by **default** because each thread has its own stack.

---

#### 5.2. Instance Variables (Non-Static Fields)
**Definition:** Variables declared inside a **class** but outside methods, without the static keyword.

###### Characteristics:
- **Scope:** Accessible throughout the class (respecting access modifiers)
- **Lifetime:** Created when the object is instantiated, destroyed when the object is garbage collected
- **Storage:** Heap memory (part of the object)
- **Initialization:** Auto-initialized to **default values** (0, null, false)
- **Access modifiers:** Can use `public`, `private`, `protected`, `default`

**Example:**

```java
public class Employee {
    private String name; // Instance variable (default: null)
    private int age;     // Instance variable (default: 0)
}
```

**Why "Instance"?:** Each object (instance) has its own copy of instance variables.

**Interview Insight:** Instance variables are not **thread-safe**—multiple threads accessing the same object can cause race conditions.

---

#### 5.3. Static Variables (Class Variables)
**Definition:** Variables declared with the `static` keyword, shared across all instances.

###### Characteristics:
- **Scope:** Accessible to all instances of the class
- **Lifetime:** Created when the class is loaded, destroyed when the JVM shuts down
- **Storage:** Method Area (Metaspace) in JVM—not on the heap or stack
- **Initialization:** Auto-initialized to default values
- **Access:** Can be accessed without creating an `object` (ClassName.variableName)

**Example:**

```java
public class Counter {
    static int count = 0; // Shared by all Counter objects
    
    public Counter() {
        count++; // All instances increment the same 'count'
    }
}
```

**Real-World Use Case:** Configuration settings, connection pools, counters.

###### Interview Insight:
- Static variables are not thread-safe by default—use synchronized or volatile if needed
- They can cause memory leaks if not managed carefully (e.g., storing large collections in static variables)