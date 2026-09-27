## 14. Interview-Oriented Key Points (Quick Revision)

---

- **if vs switch:** `Switch` is faster for 5+ discrete values (O(1) vs O(n))

- **Switch supports:** `int`, `char`, `String`, `enum`, `byte`, `short` (NOT long, float, double, boolean)

- **Fallthrough:** Missing break causes execution to continue to next case

- **Default case:** Always include for safety and handling unexpected values

- **Switch expressions (Java 14+):** Return values, no break needed, arrow syntax

- **Ternary operator:** Compact if-else for simple assignments

- **Short-circuit evaluation:** && and || don't evaluate second operand if unnecessary

- **== vs equals():** == compares references, equals() compares content

- **Null safety:** Always check null before method calls or use short-circuit

- **Best practices:** Always use braces, prefer switch expressions, extract complex conditions

- **Pattern matching (Java 21+):** Type checking and casting in switch

- **Exhaustiveness:** Switch expressions must handle all possible values

---

#### 14.1. One-Line Exam / Interview Answer
"Decision-making statements in Java control program flow through conditional execution using if-else for ranges and complex conditions, switch for discrete values with O(1) lookup, ternary operator for inline assignments, and modern switch expressions (Java 14+) that return values without fallthrough."