## 11. Interview-Oriented Key Points (Quick Revision)

---

**a.** Operators are compile-time constructs translated to JVM bytecode instructions (e.g., + → iadd).

**b.** **Precedence determines evaluation order:** * before +, && before ||. Use parentheses to override.

**c.** **Associativity determines direction:** Most operators are left-to-right; assignment and ternary are right-to-left.

**d.** == compares references for objects, not content. Use .equals() for content comparison.

**e.** **Integer division truncates:** 5 / 2 = 2, not 2.5. Cast to double for decimal results.

**f.** Short-circuit evaluation (&&, ||) stops early, unlike bitwise operators (&, |).

**g.** ++x increments then uses; x++ uses then increments. Both have side effects.

**h.** **Compound operators include implicit cast:** byte b; b += 1; compiles, but b = b + 1; doesn't.

**i.** Bitwise operators (&, |, ^, ~, <<, >>, >>>) manipulate individual bits.

**j.** >> is signed shift (preserves sign), >>> is unsigned shift (zero-fill).

**k.** **Overflow wraps silently:** Integer.MAX_VALUE + 1 becomes Integer.MIN_VALUE, no exception.

**l.** String concatenation with + uses StringBuilder (pre-Java 9) or invokedynamic (Java 9+).

**m.** Autoboxing/unboxing with operators causes heap allocation and method call overhead.

**n.** instanceof checks runtime type and enables safe casting. Pattern matching (Java 16+) auto-casts.

**o.** Ternary operator (? :) is Java's only ternary operator, providing concise conditional expressions.

**p.** **Type promotion:** Smaller types (byte, short, char) promote to int in expressions.

**q.** **Division by zero:** Integer division throws ArithmeticException; floating-point division returns Infinity or NaN.

**r.** Operator precedence hasn't changed since Java 1.0 and remains unchanged till Java 25.

**s.** Bitwise complement (~) inverts all bits; for ~5 (binary 0101), result is -6 (two's complement).

**t.** **Best practice:** Favor readability over cleverness; avoid side effects in complex expressions.

---

### 11.1. One-Line Exam / Interview Answer

**Q:** What are operators in Java?
**A:** Operators are special symbols that perform operations on operands (variables, constants, or expressions) and produce results; they are compile-time constructs translated into JVM bytecode instructions, categorized by operand count (unary, binary, ternary), operation type (arithmetic, relational, logical, bitwise, assignment, conditional, type comparison), and side-effect behavior (pure or side-effecting).