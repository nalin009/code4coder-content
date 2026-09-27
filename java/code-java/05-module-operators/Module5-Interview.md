## MODULE 5: OPERATORS

---
---

Interview Question 1
Q: Explain the difference between == and .equals() in Java. When should you use each?
Answer:
The == operator compares references (memory addresses) for objects and values for primitive types. For objects, it checks if both references point to the same memory location. The .equals() method compares the actual content of objects if it has been properly overridden (e.g., in String, Integer). Use == for primitives and reference equality checks. Use .equals() for content-based comparison of objects. For example, new String("Hi") == new String("Hi") returns false, but new String("Hi").equals(new String("Hi")) returns true.

Interview Question 2
Q: What is short-circuit evaluation? Explain with an example and discuss its benefits.
Answer:
Short-circuit evaluation means that the second operand of a logical operator (&& or ||) is not evaluated if the result is already determined by the first operand. For &&, if the first operand is false, the second is skipped. For ||, if the first operand is true, the second is skipped. Example: if (obj != null && obj.getName().equals("John")) — if obj is null, obj.getName() is never called, preventing a NullPointerException. Benefits include performance optimization (avoiding unnecessary evaluations) and safety (preventing errors like null pointer exceptions or division by zero in the second operand).

Interview Question 3
Q: Explain the difference between pre-increment (++x) and post-increment (x++). Provide an example.
Answer:
Pre-increment (++x) increments the variable first and then returns the new value. Post-increment (x++) returns the current value first and then increments the variable. Example: int x = 5; int a = ++x; results in a = 6, x = 6. But int x = 5; int b = x++; results in b = 5, x = 6. At the bytecode level, pre-increment loads the value, increments it, stores it, and uses the new value, while post-increment loads the value, uses it, then increments and stores. This distinction is important for understanding side effects in expressions and is a common interview question for 3–5+ year experience roles.

Interview Question 4
Q: Why does integer division in Java truncate the result? How can you get a decimal result?
Answer:
Integer division in Java truncates because the / operator, when applied to two integer operands, performs integer arithmetic following Java's type rules, which discard the fractional part to produce an integer result. This is by design to maintain type consistency — dividing two int values yields an int. To get a decimal result, cast at least one operand to a floating-point type: double result = (double) 5 / 2; produces 2.5. Alternatively, use floating-point literals: double result = 5.0 / 2;. This behavior is unchanged since Java 1.0 and remains consistent till Java 25.

Interview Question 5
Q: What happens when you perform arithmetic operations on byte or short variables? Explain with an example.
Answer:
When performing arithmetic operations on byte or short variables, Java applies binary numeric promotion and converts them to int before the operation. This means the result is an int, not byte or short. Example: byte a = 10, b = 20; byte c = a + b; causes a compilation error because a + b is an int (value 30), which cannot be implicitly converted back to byte. You must explicitly cast: byte c = (byte)(a + b);. Compound operators like += include an implicit cast, so a += b compiles without error. This promotion rule is fundamental to Java's type safety and has been unchanged till Java 25.

Interview Question 6
Q: Explain the difference between >> and >>> operators in Java. When would you use each?
Answer:
Both >> (signed right shift) and >>> (unsigned right shift) shift bits to the right, but they differ in how they handle the sign bit. The >> operator preserves the sign by filling the leftmost bits with the sign bit (1 for negative numbers, 0 for positive), making it an arithmetic shift. The >>> operator always fills with 0, making it a logical shift. For example, -5 >> 1 results in -3 (sign preserved), while -5 >>> 1 produces a large positive number (2147483645). Use >> for arithmetic operations where you want to maintain the sign. Use >>> when treating the number as an unsigned bit pattern, common in cryptography, hashing, and low-level bit manipulation.

Interview Question 7
Q: What is the precedence of operators in Java? Why is understanding precedence important?
Answer:
Operator precedence determines the order in which operators are evaluated in an expression. For example, * and / have higher precedence than + and -, so 5 + 3 * 2 evaluates as 5 + (3 * 2) = 11, not (5 + 3) * 2 = 16. Understanding precedence is critical for writing correct code, avoiding bugs, and interpreting existing code accurately. In interviews, especially for experienced roles, candidates are expected to explain precedence without hesitation. To avoid ambiguity, best practice is to use parentheses to make intent explicit: (5 + 3) * 2 is clearer than relying on precedence rules. The full precedence hierarchy (from highest to lowest) includes postfix operators, unary operators, multiplicative, additive, shift, relational, equality, bitwise, logical, ternary, and assignment operators. This hierarchy has been consistent since Java 1.0 and remains unchanged till Java 25.

Interview Question 8
Q: Explain what happens when you use the + operator with String and non-String types. How does Java handle this at the compiler and JVM level?
Answer:
When the + operator is used with at least one String operand, Java performs string concatenation. Non-String operands are automatically converted to their string representation. Example: "Value: " + 5 results in "Value: 5". At the compiler level (pre-Java 9), this was translated to StringBuilder operations: new StringBuilder().append("Value: ").append(5).toString(). From Java 9 onwards, the compiler uses the invokedynamic bytecode instruction with StringConcatFactory, allowing the JVM to optimize concatenation at runtime. This optimization reduces bytecode size and improves performance. For concatenation in loops, explicitly using StringBuilder is still recommended to avoid creating multiple intermediate objects, which increases GC pressure. This behavior ensures readable syntax while maintaining performance, and the optimization strategy is unchanged till Java 25.

Interview Question 9
Q: What are bitwise operators, and when should you use them? Provide a real-world example.
Answer:
Bitwise operators (&, |, ^, ~, <<, >>, >>>) perform operations on individual bits of integer types. They are used for low-level programming tasks such as manipulating flags, optimizing performance, and implementing network protocols or encryption algorithms. A real-world example is permission management: int permissions = READ | WRITE; combines flags, if ((permissions & READ) != 0) checks if read permission is set, and permissions &= ~WRITE; revokes write permission. Bitwise operations are extremely fast (single CPU instructions) and useful in embedded systems, game development, and systems programming. However, they reduce code readability, so they should only be used when necessary. For general boolean logic, always use logical operators (&&, ||) instead.

Interview Question 10
Q: What is the difference between & and && when applied to boolean operands? Are there performance implications?
Answer:
Both & and && perform logical AND operations on boolean operands, but & always evaluates both operands, while && uses short-circuit evaluation and skips the second operand if the first is false. Example: if (x != 0 & (10 / x > 5)) will throw ArithmeticException if x = 0 because both operands are evaluated. But if (x != 0 && (10 / x > 5)) safely skips the division if x = 0. The performance implication is that && can be faster if the second operand is expensive to compute, as it avoids unnecessary work. Always use && for boolean logic to benefit from short-circuiting and prevent side effects like exceptions or null pointer errors.

Interview Question 11
Q: How does Java handle integer overflow? What are the implications for production code?
Answer:
Java handles integer overflow by wrapping around silently without throwing an exception. For example, Integer.MAX_VALUE + 1 wraps to Integer.MIN_VALUE (-2147483648). This silent overflow can cause serious bugs in production, especially in financial calculations, counters, or array indexing. To handle overflow safely, developers should use larger data types (long instead of int) or Java 8's Math.addExact(), Math.multiplyExact(), and similar methods, which throw ArithmeticException on overflow. Example: int result = Math.addExact(a, b); throws an exception if the result exceeds int range. For critical applications, always validate input ranges and use appropriate overflow detection mechanisms. This behavior is unchanged till Java 25 and is a common interview topic for experienced roles.

Interview Question 12
Q: Explain compound assignment operators. Why does byte b; b += 1; compile but b = b + 1; does not?
Answer:
Compound assignment operators (+=, -=, *=, etc.) combine an operation and an assignment in one step. Critically, they include an implicit cast to the target variable's type. When you write b = b + 1; where b is a byte, the expression b + 1 is promoted to int due to binary numeric promotion, and assigning an int to a byte requires an explicit cast, causing a compilation error. However, b += 1; is equivalent to b = (byte)(b + 1);, so the implicit cast allows it to compile. This implicit casting behavior applies to all compound assignment operators and is a subtle but important detail that demonstrates deep understanding of Java's type system. Interviewers for 3–5+ year roles frequently test this to assess attention to language fundamentals. This behavior has been consistent since Java 1.0 and remains unchanged till Java 25.