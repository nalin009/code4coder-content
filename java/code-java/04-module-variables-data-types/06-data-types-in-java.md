## 6. Data Types in Java
Java has two categories of data types:

---

#### 6.1. Primitive Data Types
**Definition:** Predefined by the language, representing simple values. They are not objects.

**Why Primitives Exist:** Performance and memory efficiency. Primitives are stored directly in memory, avoiding object overhead (no object header, no garbage collection overhead).

##### Java has 8 primitive types:

|**Type**|**Size**|**Range**|**Default Value**|**Description**|
|--------|--------|---------|-----------------|---------------|
| **`byte`** | 1 byte | -128 to 127 | 0 | Smallest integer type |
| **`short`** | 2 byte | -32,768 to 32,767 | 0 | Rarely used |
| **`int`** | 4 byte | -2³¹ to 2³¹-1 (~-2.1B to 2.1B) | 0 | Default choice for integers |
| **`long`** | 8 byte | -2⁶³ to 2⁶³-1 | 0L | For large numbers (use `L` suffix) |
| **`float`** | 4 byte | ~±3.4 × 10³⁸ (7 decimal digits precision) | 0.0f | Single-precision (use f suffix) |
| **`double`** | 8 byte | ~±1.7 × 10³⁰⁸ (15 decimal digits) | 0.0d | Default choice for decimals |
| **`char`** | 2 byte | 0 to 65,535 (Unicode characters) | '\u0000' | Single character (use single quotes) |
| **`boolean`** | 1 bit* | true or false | false | Logical values |

***Note: The JVM specification doesn't mandate boolean size—it's JVM-dependent. In practice, it's often 1 byte in arrays and 4 bytes (1 int) as a standalone variable for performance.**

###### **6.1.1 byte**
**Use Case:** When memory is critical (e.g., large arrays, file I/O, network protocols).
**Example:**

```java
byte temperature = 25; // -128 to 127
```

**Pitfall:** Overflow behavior wraps around.

```java
byte b = 127;
b++; // b becomes -128 (overflow)
```

###### **6.1.2 short**
**Use Case:** Rarely used in modern Java. Useful in legacy systems or memory-constrained environments.

**Example:**

```java
short year = 2025;
```

###### **6.1.3 int**
**Use Case:** Default choice for integers. Use unless you need a smaller or larger range.

**Example:**

```java
int population = 1400000000; // ~1.4 billion
```

**Why Default?:** Best balance of range and performance on modern CPUs.

###### **6.1.4 long**
**Use Case:** Large numbers (e.g., timestamps, file sizes, IDs).

**Example:**

```java
long distance = 9460730472580800L; // Light-year in meters
```

**Critical Rule:** Always use the `L` suffix, or the compiler treats it as int and may overflow.

**Common Interview Question:** "What happens if you omit the L?"
- The literal is treated as int, and if it exceeds int range, you get a compile-time error.

###### **6.1.5 float**
**Use Case:** When memory is more important than precision (e.g., graphics, games).

**Example:**

```java
float price = 19.99f; // Must use 'f' suffix
```

**Pitfall:** Only ~7 decimal digits of precision.

```java
float f = 1234567.89f;
System.out.println(f); // Output: 1234567.9 (precision loss)
```

**Interview Insight:** Never use float for financial calculations (use BigDecimal `java.math.BigDecimal` instead).

###### **6.1.6 double**
**Use Case:** Default choice for decimals. Scientific calculations, general-purpose floating-point.

**Example:**

```java
double pi = 3.141592653589793;

```

**Precision:** ~15 decimal digits.

**Interview Insight:** double arithmetic is not exact due to binary representation.

```java
System.out.println(0.1 + 0.2); // Output: 0.30000000000000004
```
###### **6.1.7 char**
**Use Case:** Storing single characters. Uses Unicode (2 bytes).

**Example:**

```java
char grade = 'A';
char rupee = '₹'; // Unicode character
char unicode = '\u0041'; // 'A' in Unicode
```

**Interview Insight:** char is unsigned (0 to 65,535), unlike byte or short.

###### **6.1.8 boolean**
**Use Case:** Logical conditions, flags, control flow.

**Example:**

```java
boolean isActive = true;
boolean hasAccess = false;
```

**Critical Rule:** Only true or false—no integers (unlike C/C++).

```java
// Invalid in Java:
// if (1) { } // Compile-time error
```

**Interview Insight:** Unlike C, Java doesn't convert 0/1 to boolean. This prevents subtle bugs.

---

#### 6.2. Non-Primitive (Reference) Data Types
**Definition:** Data types that refer to objects. They store memory addresses (references), not actual data.

**Examples:**
- **Strings:** `String name = "Java";`
- **Arrays:** `int[] numbers = {1, 2, 3};`
- **Classes:** `Employee emp = new Employee();`
- **Interfaces:** `List<String> list = new ArrayList<>();`
- **Enums:** `Day today = Day.MONDAY;`

##### Key Difference from Primitives:

|**Aspect**|**Primitive**|**Reference**|
|----------|-------------|-------------|
| **Storage** | Stores actual value | Stores memory address (reference) |
| **Default Value** | 0, false, '\u0000' | null |
| **Memory** | Stack (local) or heap | Reference on stack, object on heap |
| **Comparison** | == compares values | == compares references (addresses) |
| **Mutability** | Always immutable (value) | Can be mutable or immutable |