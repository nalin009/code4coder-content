## 9. Type Casting (Type Conversion)

---

**Definition**: Converting a value from one data type to another.

Java has **two types** of casting:

#### 9.1. Implicit Casting (Widening Conversion)
**Definition**: Automatic conversion by the compiler when **no data loss** occurs.

**Direction**: Smaller type → Larger type

**Order** (safe conversions):

```java
byte → short → int → long → float → double
       char → int
```

**Example:**

```java
int x = 100;
long y = x; // Implicit: int → long (safe)

float f = y; // Implicit: long → float (may lose precision but allowed)
```

##### Why int → float Doesn't Lose Data "Officially":
Even though float has only 4 bytes vs. int's 4 bytes, float can represent a wider range (using scientific notation).
However, precision loss can occur for large integers.

**Example of Precision Loss:**

```java
int large = 123456789;
float f = large;
System.out.println(f); // Output: 1.23456792E8 (rounded)
```

**Interview Insight:** long → float is implicit but can lose precision because float has only ~7 significant digits.

---

#### 9.2. Explicit Casting (Narrowing Conversion)
**Definition:** Manual conversion by the programmer when data loss may occur.

**Direction:** Larger type → Smaller type

**Syntax:** `(targetType) value`

**Example:**

```java
double pi = 3.14159;
int approx = (int) pi; // Explicit: double → int (fractional part lost)
System.out.println(approx); // Output: 3
```

**Overflow Example:**

```java
int bigValue = 130;
byte small = (byte) bigValue; // Overflow
System.out.println(small); // Output: -126 (wraps around)
```

**Why Overflow Happens: **
byte range is -128 to 127. The value 130 exceeds this, so it wraps: 130 - 256 = -126

**Interview Insight:** Explicit casting doesn't throw exceptions for overflow—it silently wraps. This can cause bugs.

##### Casting with char
char is unsigned, so casting to byte or short (signed) can produce unexpected results.

**Example:**

```java
char c = 'A'; // 65 in Unicode
int i = c;    // Implicit: char → int (65)

char c2 = (char) 65; // Explicit: int → char ('A')
```

##### String to Primitive Conversion (Not Casting)
This is not casting—it's parsing.

**Example:**

```java
String str = "123";
int num = Integer.parseInt(str); // Parsing, not casting
```

**Interview Insight:** Casting works only between numeric types and char. For String, you must use wrapper class methods like parseInt, parseDouble, etc.