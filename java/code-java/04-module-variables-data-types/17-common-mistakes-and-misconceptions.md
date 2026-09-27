## 17. Common Mistakes & Misconceptions

---

#### Mistake 1: Confusing Declaration and Initialization

```java
int x; // Declaration
System.out.println(x); // Error: variable might not have been initialized
```

**Fix**: Always initialize local variables before use.

---

#### Mistake 2: Using `==` for Wrapper Comparison

```java
Integer a = 200;
Integer b = 200;
if (a == b) { } // Bug: compares references, not values
```

**Fix**: Use `.equals()`.

```java
if (a.equals(b)) { } // Correct
```

---

#### Mistake 3: Forgetting Literal Suffixes

```java
long big = 123456789012345; // Error: integer too large
```
**Fix**:

```java
long big = 123456789012345L;
```

---

#### Mistake 4: Autoboxing in Loops

```java
Integer sum = 0;
for (int i = 0; i < 1_000_000; i++) {
    sum += i; // Creates 1 million Integer objects
}
```

**Fix**: Use primitive `int`.

---

#### Mistake 5: Unboxing Null

```java
Integer num = null;
int value = num; // NullPointerException
```

**Fix**: Null-check before unboxing.

---

#### Mistake 6: Assuming `byte` is 8 Bits for `boolean`

**Misconception**: "`boolean` is 1 bit."
**Reality**: JVM-dependent. Often 1 byte in arrays, 4 bytes standalone.

---

#### Mistake 7: Type Promotion Confusion

```java
byte a = 10;
byte b = 20;
byte c = a + b; // Error: a + b is int
```

**Fix**: Cast or use `int`.

---

#### Mistake 8: Ignoring Overflow

```java
int max = Integer.MAX_VALUE;
int overflow = max + 1; // Wraps to Integer.MIN_VALUE (no exception)
```

**Fix**: Use `Math.addExact()` or switch to `long`.