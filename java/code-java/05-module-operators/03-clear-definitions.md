## 3. Clear Definitions

---

#### 3.1. What is an Operator?

**Simple Definition:** An operator is a special symbol or keyword that performs a specific operation on one, two, or three operands and produces a result.

**Interview-Safe Definition:** "An operator in Java is a symbol that tells the compiler to perform specific mathematical, logical, relational, or bitwise operations on operands. Operators work on primitive types and, in limited cases, on object references, and are translated by the compiler into corresponding JVM bytecode instructions."

---

#### 3.2. What is an Operand?

**Simple Definition:** An operand is the data on which an operator performs its operation. It can be a variable, constant, or expression.

**Example:**

```java
int result = a + b;  // 'a' and 'b' are operands, '+' is the operator
```

---

#### 3.3. What Are Expressions in Java?
An expression is a construct made up of variables, operators, and method calls that evaluates to a single value. Every expression has a type and a result.

**Examples:**
- **Literal:** 5 (type: int, value: 5)
- **Variable:** x (type: depends on x, value: current value of x)
- **Arithmetic:** a + b * c (type: int/double/etc., value: computed result)
- **Relational:** x > 5 (type: boolean, value: true/false)
- **Method call:** Math.sqrt(16) (type: double, value: 4.0)
- **Ternary:** (x > 0) ? "positive" : "negative" (type: String, value: depends on x)

###### **Expressions vs Statements:**
- **Expression:** produces a value → can be assigned: int x = 5 + 3;
- **Statement:** complete unit of execution → int x = 5; (includes the semicolon)
- **Some expressions are also statements:** x++; (standalone expression statement)

###### **Compound Expressions:**
- Multiple operators create compound expressions: int result = a + b * c / d - e;
- Understanding precedence, associativity, and evaluation order is critical for reading and writing compound expressions correctly.

###### **Key Terms:**
- **Precedence:** The priority order in which operators are evaluated in an expression
- **Associativity:** The direction (left-to-right or right-to-left) in which operators of the same precedence are evaluated
- **Side Effect:** When an operator modifies the state of an operand (like ++ or --)
- **Short-Circuit Evaluation:** When the second operand of a logical operator is not evaluated if the result is already determined