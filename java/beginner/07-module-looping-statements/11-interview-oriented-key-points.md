### 10. Interview-Oriented Key Points (Quick Revision)
- for vs while: Use for when iterations are known, while when unknown
- do-while: Executes at least once, checks condition after
- Enhanced for loop: Cannot modify collection, no index access, uses iterator internally
- break: Exits loop immediately
- continue: Skips current iteration, moves to next
- return: Exits entire method
- Labeled break/continue: Control flow in nested loops
- Nested loops: Time complexity multiplies (O(n × m))
- Infinite loops: Condition never becomes false; use break or return to exit
- ConcurrentModificationException: Thrown when modifying collection during enhanced for loop
- Loop optimization: JIT performs unrolling, hoisting, fusion
- Performance: Cache collection size, avoid object creation in loops, use enhanced for when possible

---
---

### 11. One-Line Exam / Interview Answer
"Looping statements in Java enable repeated execution of code blocks: for loops for known iterations with compact syntax, while loops for unknown iterations with pre-checking, do-while loops guaranteeing at least one execution with post-checking, enhanced for loops for simplified collection iteration, and control statements (break, continue, return) for altering loop flow."

---
---