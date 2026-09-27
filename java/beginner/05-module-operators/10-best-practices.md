## 10. Best Practices (5+ Years Experience Expectation)

---

#### Practice 1: Prefer Readability Over Cleverness

**Avoid:**

```java
int result = x++ + ++x + x--;  // Hard to understand, error-prone
```

**Prefer:**

```java
int temp1 = x;
x++;
x++;
int temp2 = x;
x--;
int result = temp1 + temp2 + x;
```

###### Why: Code is read 10x more than written. Clarity trumps brevity.

---

#### Practice 2: Use Parentheses for Complex Expressions

**Avoid:**

```java
boolean flag = a > 5 && b < 10 || c == 0 && d != 5;  // Ambiguous
```

**Prefer:**

```java
boolean flag = ((a > 5) && (b < 10)) || ((c == 0) && (d != 5));  // Clear
```

###### Why: Relying on precedence rules increases cognitive load. Parentheses make intent explicit.

---

#### Practice 3: Avoid Bitwise Operators for Booleans

**Avoid:**

```java
if (isValid & isActive) {  // Works, but confusing
    // ...
}
```

**Prefer:**

```java
if (isValid && isActive) {  // Clear intent: logical operation
    // ...
}
```

###### Why: Bitwise operators on booleans work but don't short-circuit. Use logical operators for boolean logic, bitwise for bit manipulation.

---

#### Practice 4: Minimize Side Effects in Expressions

**Avoid:**

```java
arr[i++] = arr[i];  // Confusing: which 'i' is used where?
```

**Prefer:**

```java
arr[i] = arr[i];
i++;
```

###### Why: Side effects within expressions are hard to reason about and lead to bugs.

---

#### Practice 5: Use Explicit Type Conversion for Division

**Avoid:**

```java
double ratio = total / count;  // May truncate if both are ints
```

**Prefer:**

```java
double ratio = (double) total / count;  // Explicit intent
```

###### Why: Makes intent clear and prevents silent truncation bugs.

---

#### Practice 6: Leverage Short-Circuit for Performance

**Prefer:**

```java
if (cheapCheck() && expensiveCheck()) {  // expensiveCheck() only runs if cheapCheck() is true
    // ...
}
```

###### Why: Put fast/cheap conditions first to avoid unnecessary expensive operations.

---

#### Practice 7: Use Bitwise Operators Only When Needed
##### Use Bitwise When:
- Manipulating individual bits (flags, permissions)
- Low-level I/O (network protocols, file formats)
- Performance-critical bit manipulation

##### Avoid Bitwise For:
- General-purpose logic (use logical operators)
- Showing off (readability suffers)

---

#### Practice 8: Understand Autoboxing Overhead

**Avoid in Tight Loops:**

```java
Integer sum = 0;
for (int i = 0; i < 1000000; i++) {
    sum += i;  // Unboxing, adding, boxing on every iteration
}
```

**Prefer:**

```java
int sum = 0;
for (int i = 0; i < 1000000; i++) {
    sum += i;  // Pure primitive operation
}
Integer result = sum;  // Box once at the end
```

###### Why: Each iteration in the first example creates heap allocation and GC pressure.

---

#### Practice 9: Be Careful with Overflow

**Risky:**

```java
int large = Integer.MAX_VALUE;
int overflow = large + 1;  // Silent overflow: becomes Integer.MIN_VALUE
```

**Safe:**

```java
long large = Integer.MAX_VALUE;
long result = large + 1;  // No overflow: uses long
```

**Or Use Math Methods (Java 8+):**

```java
int result = Math.addExact(large, 1);  // Throws ArithmeticException on overflow
```

###### Why: Silent overflow bugs are hard to detect. Use larger types or explicit overflow checks for critical calculations.

---

#### Practice 10: Document Operator Choices in Complex Code

**Example:**

```java
// Using bitwise XOR to swap without temp variable
// More efficient in memory-constrained environments
a = a ^ b;
b = a ^ b;
a = a ^ b;
```

###### Why: Non-obvious operator usage should be documented so future maintainers understand the reasoning. 