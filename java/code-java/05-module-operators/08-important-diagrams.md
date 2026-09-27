## 8. Important Diagrams (Described in Words)

---

#### Diagram 1: Operator Precedence and Associativity

**Title:** "Java Operator Precedence Chart (Highest to Lowest)"

**Description:** A vertical chart showing operator precedence from highest (top) to lowest (bottom), with associativity noted:
1. **Postfix:** expr++, expr-- (Left-to-right)
2. **Unary:** ++expr, --expr, +, -, !, ~ (Right-to-left)
3. **Multiplicative:** *, /, % (Left-to-right)
4. **Additive:** +, - (Left-to-right)
5. **Shift:** <<, >>, >>> (Left-to-right)
6. **Relational:** <, >, <=, >=, instanceof (Left-to-right)
7. **Equality:** ==, != (Left-to-right)
8. **Bitwise AND:** & (Left-to-right)
9. **Bitwise XOR:** ^ (Left-to-right)
10. **Bitwise OR:** | (Left-to-right)
11. **Logical AND**: && (Left-to-right)
12. **Logical OR:** || (Left-to-right)
13. **Ternary:** ? : (Right-to-left)
14. **Assignment:** =, +=, -=, *=, /=, %=, &=, ^=, |=, <<=, >>=, >>>= (Right-to-left)

**Key Insight:** Parentheses () override precedence and have the highest priority.

---

#### Diagram 2: Expression Evaluation Flow

**Title:** "How Java Evaluates: result = a + b * c"

**Description:** A flowchart showing:
1. **Parse:** Identify operators and operands
2. **Precedence Check:** * has higher precedence than +
3. **Evaluate b * c first:** Compute and push result to stack
4. **Evaluate a + (result of b*c):** Compute and push final result
5. **Assignment:** Pop result and assign to result

**Visual:** Show stack state at each step with values being pushed/popped.

---

#### Diagram 3: Pre-Increment vs Post-Increment

**Title:** "Execution Order: ++x vs x++"

**Description:** Two parallel timelines showing:

**Pre-Increment (++x):**
1. Increment x
2. Use new value of x

**Post-Increment (x++):**
1. Use current value of x
2. Increment x

**Example Code:**

```java
int x = 5;
int a = ++x;  // a = 6, x = 6
int b = x++;  // b = 6, x = 7
```

---

#### Diagram 4: Short-Circuit Evaluation

**Title:** "Logical Operators: Full Evaluation vs Short-Circuit"

**Description:** Two side-by-side flowcharts:

**Bitwise & (Full Evaluation):**
- Evaluate operand 1
- Evaluate operand 2
- Perform AND operation
- Return result

**Logical && (Short-Circuit):**
- Evaluate operand 1
- If false → Return false immediately
- If true → Evaluate operand 2
- Return result

**Visual:** Show decision diamond where && has early exit path.

---

#### Diagram 5: Type Promotion Hierarchy

A pyramid diagram showing Java's automatic type promotion during operations:

```java
                    double (widest)
                   /
                float
               /
             long
            /
          int  ← byte, short, char all promote to int first
         /
    byte, short, char (narrowest)
```

**Rule:** In mixed-type operations, the narrower type is automatically promoted to the wider type. Result type = widest type in the expression.

**Example:** byte + short → both promoted to int, result is int
         int + long → int promoted to long, result is long
         long + float → long promoted to float, result is float