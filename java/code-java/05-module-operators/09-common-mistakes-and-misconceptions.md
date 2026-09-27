## 9. Common Mistakes & Misconceptions

---

#### Mistake 1: Using == to Compare Objects

**Wrong:**

```java
String s1 = new String("Hello");
String s2 = new String("Hello");
if (s1 == s2) {  // false — compares references, not content
    System.out.println("Equal");
}
```

**Correct:**

```java
if (s1.equals(s2)) {  // true — compares content
    System.out.println("Equal");
}
```

##### Why: == compares memory addresses for objects. Use .equals() for content comparison.

---

#### Mistake 2: Ignoring Integer Division Truncation

**Wrong:**

```java
double average = 5 / 2;  // average = 2.0 (not 2.5!)
```

**Correct:**

```java
double average = 5.0 / 2;  // average = 2.5
// OR
double average = (double) 5 / 2;  // average = 2.5
```

##### Why: 5 / 2 is integer division (result = 2), then 2 is promoted to 2.0. The division must involve at least one double to get a double result.

---

#### Mistake 3: Misunderstanding Operator Precedence

**Wrong Assumption:**

```java
int result = 5 + 3 * 2;  // User thinks: (5 + 3) * 2 = 16
// Actual result: 5 + (3 * 2) = 11
```

**Solution: Use parentheses for clarity:**

```java
int result = (5 + 3) * 2;  // Explicit: result = 16
```

---

#### Mistake 4: Confusing && with &

**Wrong:**

```java
if (obj != null & obj.getName().equals("John")) {  // NullPointerException if obj is null
    // ...
}
```

**Correct:**

```java
if (obj != null && obj.getName().equals("John")) {  // Safe: short-circuits if obj is null
    // ...
}
```

###### Why: & evaluates both operands, && short-circuits.

---

#### Mistake 5: Side Effects in Expressions

**Confusing:**

```java
int x = 5;
int result = x++ + ++x;
// x is incremented twice, but when?
// Step 1: x++ → use 5, then x becomes 6
// Step 2: ++x → x becomes 7, use 7
// result = 5 + 7 = 12, x = 7
```

**Best Practice: Avoid multiple side effects in one expression:**

```java
int x = 5;
int temp1 = x++;  // temp1 = 5, x = 6
int temp2 = ++x;  // x = 7, temp2 = 7
int result = temp1 + temp2;  // result = 12
```

---

#### Mistake 6: Forgetting Compound Assignment Includes Cast

**Wrong Understanding:**

```java
byte b = 100;
b = b + 1;  // Compilation error: int cannot be converted to byte
```

**Correct:**

```java
byte b = 100;
b += 1;  // Compiles: equivalent to b = (byte)(b + 1)
```

##### Why: Compound operators include an implicit cast to the target type.

---

#### Mistake 7: Bitwise Right Shift on Negative Numbers

**Unexpected:**

```java
int x = -5;
int result = x >> 1;  // result = -3 (not -2!)
// Binary: 11111111 11111111 11111111 11111011 >> 1
//       = 11111111 11111111 11111111 11111101 (sign extended)
```

###### Why: >> preserves sign (arithmetic shift). Use >>> for logical shift (zero-fill):

```java
int result = x >>> 1;  // result = 2147483645 (positive)
```