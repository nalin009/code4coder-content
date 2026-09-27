## 12. Autoboxing & Unboxing

---

#### 12.1. Autoboxing
**Definition:** Automatic conversion from `primitive` to `wrapper` object.

**Example:**

```java
int primitive = 10;
Integer wrapper = primitive; // Autoboxing (compiler adds Integer.valueOf(primitive))
```

###### Behind the Scenes:
**The compiler converts this to:**

```java
Integer wrapper = Integer.valueOf(primitive);
```

---

#### 12.2. Unboxing
**Definition:** Automatic conversion from `wrapper` object to `primitive`.

**Example:**

```java
Integer wrapper = 20;
int primitive = wrapper; // Unboxing (compiler adds wrapper.intValue())
```

###### Behind the Scenes:

```java
int primitive = wrapper.intValue();
```

---

#### 12.3. Autoboxing in Collections

**Example:**

```java
ArrayList<Integer> list = new ArrayList<>();
list.add(10); // Autoboxing: int → Integer
int value = list.get(0); // Unboxing: Integer → int
```

---

#### 12.4. Performance Overhead of Autoboxing
###### Problem: Autoboxing creates objects, which adds overhead.

**Example:**

```java
// Bad: Creates 1 million Integer objects
Integer sum = 0;
for (int i = 0; i < 1_000_000; i++) {
    sum += i; // Unboxing + autoboxing in every iteration
}

// Good: No object creation
int sum = 0;
for (int i = 0; i < 1_000_000; i++) {
    sum += i; // Pure primitive arithmetic
}
```

**Interview Insight:** In performance-critical code, prefer primitives over wrappers. 

**Autoboxing can cause:**
- Garbage collection pressure (millions of short-lived objects)
- CPU overhead (object creation and method calls)

---

#### 12.5. NullPointerException with Unboxing
**Critical Pitfall:** If a wrapper object is null, unboxing throws NullPointerException.

**Example:**

```java
Integer num = null;
int value = num; // NullPointerException at runtime
```

**Why? The compiler translates this to:**

```java
int value = num.intValue(); // null.intValue() → NullPointerException
```

**Interview Insight:** This is a common source of bugs when using wrappers in collections or database results (which can return null).

**Best Practice:** Always null-check before unboxing.

```java
Integer num = getValueFromDatabase();
int value = (num != null) ? num : 0; // Safe
```

---

#### 12.6. Autoboxing with Method Overloading
Autoboxing can lead to ambiguity in method overloading.

**Example:**

```java
public void process(int x) { System.out.println("int"); }
public void process(Integer x) { System.out.println("Integer"); }

process(10); // Calls process(int), not process(Integer)
```

**Why? The compiler prefers exact match over autoboxing.**