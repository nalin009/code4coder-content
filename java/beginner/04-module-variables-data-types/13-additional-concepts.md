## 13. Additional Concepts

---

#### 13.1. Literal Suffixes
**Definition:** Characters appended to literals to specify their type.

|**Suffix**|**Type**|**Example**|
|----------|--------|-----------|
| **`L`** | long | 100L |
| **`f`** | float | 3.14f |
| **`d`** | double | 3.14d |
| **None** | int | 100 |
| **None** | double | 3.14 |

**Example:**

```java
long distance = 123456789012345L; // Must use 'L'
float price = 19.99f;             // Must use 'f'
double pi = 3.14;                 // 'd' is optional
```

**Common Mistake:** Forgetting L or f suffix.

```java
// long x = 123456789012345; // Error: integer number too large
long x = 123456789012345L;    // Correct
```

---

#### 13.2. Underscore in Numeric Literals (Java 7+)
**Feature:** Use underscores to improve readability of large numbers.

**Example:**

```java
int million = 1_000_000;
long creditCard = 1234_5678_9012_3456L;
double pi = 3.141_592_653_589_793;
```

###### Rules:
- Cannot start or end with _
- Cannot be adjacent to a decimal point

**Invalid Examples:**

```java
int x = _100;     // Error
int y = 100_;     // Error
double z = 3._14; // Error
```

**Other Example :**

```java
// Binary literals (Java 7+)
int binary = 0b1010; // 10 in decimal

// Hexadecimal
int hex = 0xFF; // 255 in decimal

// Octal (rarely used)
int octal = 077; // 63 in decimal
```

---

#### 13.3. Default Values of Variables
**Instance and Static Variables:** Auto-initialized by the JVM.

|**Type**|**Default Value**|
|--------|-----------------|
| **`byte`** | 0 |
| **`short`** | 0 |
| **`int`** | 0 |
| **`long`** | 0L |
| **`float`** | 0.0f |
| **`double`** | 0.0d |
| **`char`** | '\u0000' |
| **`boolena`** | false |
| **reference** | **`null`** |

**Local Variables: No default value—must initialize before use**

---

#### 13.4. Type Promotion in Expressions
**Rule:** In mixed-type expressions, smaller types are promoted to larger types.

**Example:**

```java
byte a = 10;
byte b = 20;
// byte c = a + b; // Error: a + b is promoted to int
int c = a + b;     // Correct
```

**Why?** The JVM internally promotes byte, short, and char to int for arithmetic operations.

**Interview Insight:** This is a common source of confusion.

---

#### 13.5. Overflow and Underflow
**Overflow:** When a value exceeds the maximum range, it wraps around to the minimum.

**Example:**

```java
int max = Integer.MAX_VALUE; // 2,147,483,647
int overflow = max + 1;
System.out.println(overflow); // Output: -2,147,483,648 (wraps to MIN_VALUE)
```

**Underflow:** Similar behavior when going below the minimum.

**Interview Insight:** Java does not throw exceptions for overflow—it silently wraps. Use `Math.addExact`, `Math.multiplyExact` (Java 8+) for overflow-safe arithmetic, these methods were introduced in Java 8.

```java
int result = Math.addExact(Integer.MAX_VALUE, 1); // Throws ArithmeticException
```

---

#### 13.6. Immutability of Wrapper Classes
**Key Insight:** All wrapper classes are immutable.

**Example:**

```java
Integer x = 10;
x = x + 5; // Creates a NEW Integer object with value 15
```

##### Why Immutable?
- **Thread-safety:** Immutable objects are inherently thread-safe
- **Security:** Prevents unintended modifications
- **Caching:** Enables efficient caching (e.g., Integer cache)

**Interview Insight:** Modifying a wrapper in a loop creates many short-lived objects, causing GC overhead.