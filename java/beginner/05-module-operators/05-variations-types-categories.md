## 5. Variations / Types / Categories
Java operators can be classified in three ways:

---

#### 5.1. Based on Number of Operands
##### A. Unary Operators (1 operand)
Operators that work on a single operand.

###### Types:
- **Unary Plus:** + (indicates positive value, rarely used)
- **Unary Minus:** - (negates the value)
- **Increment:** ++ (pre-increment and post-increment)
- **Decrement:** -- (pre-decrement and post-decrement)
- **Logical Complement:** ! (inverts boolean value)
- **Bitwise Complement:** ~ (inverts all bits)

**Examples:**

```java
int a = 5;
int b = -a;      // b = -5 (unary minus)
int c = +a;      // c = 5 (unary plus, redundant)

int x = 10;
int y = ++x;     // x = 11, y = 11 (pre-increment)
int z = x++;     // z = 11, x = 12 (post-increment)

boolean flag = true;
boolean result = !flag;  // result = false

int bits = 5;    // Binary: 00000000 00000000 00000000 00000101
int inv = ~bits; // Binary: 11111111 11111111 11111111 11111010 = -6
```

**JVM Behavior:** Pre/post increment/decrement are compiled differently:
  - ++x → load, increment, store, use new value
  - x++ → load, use old value, increment, store

##### B. Binary Operators (2 operands)
Operators that work on two operands. Most operators in Java are binary.

**Examples:**

```java
int sum = 10 + 5;           // Addition
int diff = 10 - 5;          // Subtraction
boolean isEqual = (a == b); // Comparison
int bitAnd = 5 & 3;         // Bitwise AND
```

##### C. Ternary Operator (3 operands) or Conditional (Ternary) Operator
Java has only one ternary operator: the conditional operator ? :.

**Syntax:** `condition ? valueIfTrue : valueIfFalse`

**Example:**

```java
int age = 20;
String status = (age >= 18) ? "Adult" : "Minor";
// status = "Adult"
```

**JVM Behavior:** Compiles to conditional branch instructions (ifeq, goto).

**Why it exists:** Provides a concise way to express simple conditional assignments, improving code readability for single-line decisions.

---

#### 5.2. Based on Nature of Operation
##### A. Arithmetic Operators
Perform mathematical operations.

|**Operator**|**Name**|**Example**|**Result**|
|------------|--------|-----------|----------|
| **`+`** | Addition | **`5 + 3`** | **`8`** |
| **`-`** | Subtraction | **`5 - 3`** | **`2`** |
| **`*`** | Multiplication | **`5 * 3`** | **`15`** |
| **`/`** | Division | **`5 / 3`** | **`2`** |
| **`%`** | Modulus | **`5 % 3`** | **`1`** |

###### Key Behaviors:
1. **Integer Division Truncates:**

```java
int result = 7 / 2;  // result = 3 (not 3.5)
```

2. **Division by Zero:**

```java
int x = 5 / 0;        // ArithmeticException at runtime
double y = 5.0 / 0.0; // y = Infinity (no exception)
```

3. **Modulus with Negative Numbers:**

```java
int a = -7 % 3;  // a = -1 (sign follows dividend)
int b = 7 % -3;  // b = 1
```

4. **Overflow Behavior** (unchanged till Java 25):

```java
int max = Integer.MAX_VALUE;  // 2147483647
int overflow = max + 1;        // -2147483648 (wraps around, no exception)
```

###### JVM Translation:
- iadd, isub, imul, idiv, irem for int
- ladd, lsub, lmul, ldiv, lrem for long
- fadd, fsub, fmul, fdiv, frem for float
- dadd, dsub, dmul, ddiv, drem for double

##### B. Relational (Comparison) Operators
Compare two values and return a `boolean` result.

|**Operator**|**Name**|**Example**|**Result**|
|------------|--------|-----------|----------|
| **`==`** | Equal to | **`5 == 5`** | **`true`** |
| **`!=`** | Not equal to | **`5 != 3`** | **`true`** |
| **`>`** | Greater than | **`5 > 3`** | **`true`** |
| **`<`** | Less than | **`5 < 3`** | **`false`** |
| **`>=`** | Greater than or equal to | **`5 >= 3`** | **`true`** |
| **`<=`** | Less than or equal to | **`5 <= 3`** | **`false`** |

**Critical Distinction:** Primitives vs References:

```java
// Primitives: compares values
int a = 5, b = 5;
boolean result = (a == b);  // true

// References: compares memory addresses
String s1 = new String("Hello");
String s2 = new String("Hello");
boolean sameRef = (s1 == s2);        // false (different objects)
boolean sameContent = s1.equals(s2); // true (same content)
```

###### JVM Behavior:
  - Primitive comparisons use if_icmpgt, if_icmple, etc.
  - Reference comparisons use if_acmpeq, if_acmpne

##### C. Logical Operators
Perform boolean logic operations.

|**Operator**|**Name**|**Description**|
|------------|--------|---------------|
| **&&** | Logical AND | True if both operands are true (short-circuit) |
| **!** | Logical NOT | Inverts the boolean value |

**Short-Circuit Evaluation:**

```java
int x = 5;
boolean result = (x > 0) && (x / 0 == 1);  // No exception!
// (x > 0) is true, but (x / 0) is never evaluated because
// the first condition being true means we check the second.
// Wait, that's wrong. Let me reconsider.

// Actually:
boolean result = (x < 0) && (x / 0 == 1);  // No exception!
// (x < 0) is false, so (x / 0) is never evaluated.
// Short-circuit: && stops if first operand is false.

boolean result2 = (x > 0) || (x / 0 == 1);  // No exception!
// (x > 0) is true, so (x / 0) is never evaluated.
// Short-circuit: || stops if first operand is true.
```

###### Why Short-Circuit Exists:
- **Performance:** Avoids unnecessary evaluation
- **Safety:** Prevents null pointer or division by zero errors
- **Side-Effect Control:** Allows conditional execution of expressions with side effects

###### Truth Tables:

|**A**|**B**|**A && B**| **`A\|\|B`** |**!A**|
|-----|-----|----------|--------------|------|
| true | true | true | true | false |
| true | false | false | true | false |
| false | true | false | true | true |
| false | false | false | false | true |

##### D. Bitwise Operators
Perform operations on individual bits of integer types.

|**Operator**|**Name**|**Example**|**Result (binary)**|
|------------|--------|-----------|-------------------|
| **`&`** | Bitwise AND | 5 & 3 (101 & 011) | 1 (001) |
| **`\|`** | Bitwise OR | 5 | 3 (101 & 011) | 7(111) |
| **`^`** | Bitwise XOR | 5 ^ 3 (101 ^ 011) | 6 (110) |
| **`~`** | Bitwise NOT | ~5 (~00000101) | -6 (11111010 in two's complement) |
| **`<<`** | Left shift | 5 << 1 | 10 (1010) |
| **`>>`** | Right shift (signed) | 5 >> 1 | 2 (010) |
| **`>>>`** | Right shift (unsigned) | -5 >>> 1 | Large positive number |

###### Key Behaviors:

1. Bitwise vs Logical:

```java
// Bitwise: always evaluates both operands
boolean result = (x < 0) & (x / 0 == 1);  // ArithmeticException!

// Logical: short-circuits
boolean result = (x < 0) && (x / 0 == 1);  // No exception
```

2. Shift Operators:

```java
int x = 5;        // Binary: 00000000 00000000 00000000 00000101
int left = x << 2; // Binary: 00000000 00000000 00000000 00010100 = 20

int y = -5;        // Binary: 11111111 11111111 11111111 11111011
int right = y >> 1; // Binary: 11111111 11111111 11111111 11111101 = -3 (sign extended)
int unsign = y >>> 1; // Binary: 01111111 11111111 11111111 11111101 = 2147483645
```

###### Why Bitwise Operators Exist:
- **Performance:** Direct CPU-level operations
- **Flag Management:** Setting/clearing multiple boolean flags in a single integer
- **Low-Level Programming:** Network protocols, file formats, encryption
- **Space Optimization:** Packing multiple values into one integer

**JVM Translation:** `iand`, `ior`, `ixor`, `ishl`, `ishr`, `iushr`

##### E. Assignment Operators
Assign values to variables.

|**Operator**|**Name**|**Example**|**Equivalent To**|
|------------|--------|-----------|-----------------|
| **`=`** | Simple assignment |**`x = 5`**| - |
| **`+=`** | Add and assign |**`x += 3`**|**`x = x + 3`**|
| **`-=`** | Subtract and assign |**`x -= 3`**|**`x = x - 3`**|
| **`*=`** | Multiply and assign |**`x *= 3`**|**`x = x * 3`**|
| **`/=`** | Divide and assign |**`x /= 3`**|**`x = x / 3`**|
| **`%=`** | Modulus and assign |**`x %= 3`**|**`x = x % 3`**|
| **`&=`** | Bitwise AND and assign |**`x &= 3`**|**`x = x & 3`**|
| **`\|=`** | Bitwise OR and assign |**`x \|= 3`**|**`x = x \| 3`**|
| **`^=`** | Bitwise XOR and assign |**`x ^= 3`**|**`x = x ^ 3`**|
| **`<<=`** | Left shift and assign |**`x <<= 3`**|**`x = x <<= 3`**|
| **`>>=`** | Right shift and assign |**`x >>= 3`**|**`x = x >>= 3`**|
| **`>>>=`** | Unsigned right shift and assign |**`x >>>= 3`**|**`x = x >>>= 3``**|

**Critical:** Compound Assignment Includes Implicit Cast:

```java
byte b = 10;
b = b + 1;    // Compilation error: incompatible types (int cannot be converted to byte)
b += 1;       // Compiles fine! Implicitly casts: b = (byte)(b + 1)
```
This behavior is unchanged till Java 25 and is a frequent interview question.

##### F. Type Comparison Operator 
###### The `instanceof` Operator:

Checks if an object is an instance of a specific class, subclass, or implements an interface.

**Syntax:** `object instanceof Type`

**Examples:**

```java
String s = "Hello";
boolean result = s instanceof String;  // true
boolean result2 = s instanceof Object; // true (String extends Object)
boolean result3 = s instanceof Integer; // Compilation error: incompatible types

Object obj = "Hello";
if (obj instanceof String) {
    String str = (String) obj;  // Safe cast
}
```

###### Pattern Matching (Java 16+, Enhanced in Java 21+):

```java
// Java 16+ pattern matching
if (obj instanceof String str) {
    // 'str' is automatically cast and available here
    System.out.println(str.toUpperCase());
}
```

**JVM Behavior:** Uses `instanceof` bytecode instruction, which performs runtime type checking against the class metadata.

**Why it Exists:** Enables safe runtime type checking and downcasting, essential for polymorphism.

---

#### 5.3. Based on Side-Effect Behavior
##### A. Pure (Non-Side-Effect) Operators
These operators do not modify their operands; they only produce a result.

**Examples:**
- **Arithmetic:** +, -, *, /, %
- **Relational:** ==, !=, >, <, >=, <=
- **Logical:** &&, ||, !
- **Bitwise:** &, |, ^, ~, <<, >>, >>>

```java
int a = 5;
int b = a + 3;  // 'a' remains 5, result is 8
boolean result = (a > 3);  // 'a' remains 5
```

##### B. Side-Effect Operators
These operators modify the state of their operands.

**Examples:**
- **Assignment:** =, +=, -=, *=, /=, etc.
- **Increment/Decrement:** ++, --

```java
int x = 5;
x++;        // x is now 6 (side effect)
x += 3;     // x is now 9 (side effect)
```

##### Why This Matters:
- **Debugging:** Side effects make code harder to reason about
- **Thread Safety:** Shared mutable state with side effects causes concurrency issues
- **Functional Programming:** Pure functions (no side effects) are easier to test and parallelize
- **Interview Questions:** "What's the difference between x++ and ++x?" tests understanding of side effects

---

#### 5.4. () Operator Usage in Modern Java (Java 8+)
Modern Java Features and Operators:

1. **Optional and Operators** (Java 8+):
   **Instead of:** if (obj != null && obj.getValue() > 0)
   **Use:** obj.filter(o -> o.getValue() > 0).ifPresent(...)

2. **Pattern Matching with instanceof** (Java 16+):
   **Old:** if (obj instanceof String) { String s = (String) obj; }
   **New:** if (obj instanceof String s) { // use 's' directly }

3. **Switch Expressions** (Java 14+):
   String result = switch(day) {
       case MONDAY, FRIDAY -> "Working";
       case SATURDAY, SUNDAY -> "Weekend";
       default -> "Midweek";
   };

4. **Text Blocks and Concatenation** (Java 15+):
   Reduces need for complex + operator chains with multi-line strings.

These modern features complement traditional operators, providing cleaner syntax while the underlying operator principles remain unchanged till Java 25.