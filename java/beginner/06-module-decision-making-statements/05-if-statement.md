## 5 if Statement

---

#### 5.1 Syntax:

```java
if (condition) {
    // code to execute if condition is true
}
```

##### How It Works:
- Evaluates the `boolean` condition
- If true, `executes` the block
- If false, `skips` the block
- Control continues to the next statement after the if block

**Example:**
```java
int age = 18;
if (age >= 18) {
    System.out.println("Eligible to vote");
}
System.out.println("Program continues");
```

**Output:**
```java
Eligible to vote
Program continues
```

---

##### Bytecode Behavior:
- The compiler generates an ifeq (if equal to zero) or ifne (if not equal to zero) instruction
- If the condition is `false`, the JVM uses a goto instruction to jump past the if block
- The boolean condition is evaluated by comparing stack values

---

##### Key Point: 
- Single statements don't require `braces`, but always use them for `clarity` and `safety`.
- The condition must be a boolean expression (cannot use integers like in C)
- Can be used standalone without else

##### Common Mistake:

```java
int x = 10;
if (x = 5) {  // Compilation error: cannot assign in condition
    System.out.println("Test");
}
```

##### Correct:

```java
if (x == 5) {  // Comparison operator
    System.out.println("Test");
}
```

---

#### 5.2 if-else Statement

##### Syntax:

```java
if (condition) {
    // executes if condition is true
} else {
    // executes if condition is false
}
```

##### How It Works:
- Evaluates the `boolean` condition
- If true, `executes` the if block and `skips` the else block
- If false, `skips` the if block and `executes` the else block
- Exactly `one block` executes—never `both`, never `neither`

**Example:**
```java
int number = 10;
if (number % 2 == 0) {
    System.out.println("Even number");
} else {
    System.out.println("Odd number");
}
```

**Output:**
```java
Even number
```

##### Bytecode Behavior:
- Two branches are created in `bytecode`
- JVM evaluates the condition and uses conditional jumps to `select` the branch
- Only `one branch` executes, improving performance by avoiding unnecessary checks
- Modern JVMs use branch prediction to optimize frequently taken paths

##### Real-World Use Case:

```java
// User authentication
if (password.equals(correctPassword)) {
    System.out.println("Login successful");
    grantAccess();
} else {
    System.out.println("Login failed");
    logFailedAttempt();
}
```

---

#### 5.3 else-if Ladder

##### Syntax:

```java
if (condition1) {
    // block 1
} else if (condition2) {
    // block 2
} else if (condition3) {
    // block 3
} else {
    // default block
}
```

##### How It Works:
- Conditions are evaluated sequentially from `top` to `bottom`
- The `first` condition that evaluates to true executes its block
- Once a condition is `true`, all remaining conditions are skipped
- If no condition is `true`, the else block executes (if present)

**Example:**
```java
int marks = 85;
if (marks >= 90) {
    System.out.println("Grade A");
} else if (marks >= 75) {
    System.out.println("Grade B");
} else if (marks >= 60) {
    System.out.println("Grade C");
} else {
    System.out.println("Fail");
}
```

**Output:**
```java
Grade B
```

##### Performance Consideration:
- `Order` matters for performance
- Place the most `common` condition first to reduce unnecessary checks
- For 5+ conditions on the same variable, consider using `switch`

**Example with Optimization:**

```java
// If most students score between 75-89 (Grade B)
if (marks >= 75 && marks < 90) {  // Most common case first
    System.out.println("Grade B");
} else if (marks >= 90) {
    System.out.println("Grade A");
} else if (marks >= 60) {
    System.out.println("Grade C");
} else {
    System.out.println("Fail");
}
```

**Real-World Use Case:**

```java
// HTTP status code handling
if (statusCode == 200) {
    System.out.println("Success");
} else if (statusCode >= 400 && statusCode < 500) {
    System.out.println("Client error");
} else if (statusCode >= 500) {
    System.out.println("Server error");
} else {
    System.out.println("Informational or redirect");
}
```

---

#### 5.4 Nested if

##### Syntax:

```java
if (condition1) {
    if (condition2) {
        // executes if both condition1 and condition2 are true
    }
}
```

##### How It Works:
- An if statement inside another if statement
- `Inner if` is evaluated only if outer if is true
- Can be nested multiple levels deep (avoid going beyond 3 levels)

**Example:**
```java
int age = 20;
boolean hasLicense = true;

if (age >= 18) {
    if (hasLicense) {
        System.out.println("Can drive");
    } else {
        System.out.println("Need license");
    }
} else {
    System.out.println("Too young to drive");
}
```

**Alternative Using Logical AND:**

```java
if (age >= 18 && hasLicense) {
    System.out.println("Can drive");
}
```

##### When to Use Nested vs Logical Operators:
###### Use Nested if when:
- You need different `messages/actions` for each condition
- Inner logic is `complex` and benefits from separation
- Early validation saves computation

##### Use Logical AND (&&) when:
- You just need to `check` if all conditions are true
- `Simpler`, more `readable` code
- No `intermediate` actions needed

**Deep Nesting Problem:**

```java
// Avoid this - hard to read and maintain
if (condition1) {
    if (condition2) {
        if (condition3) {
            if (condition4) {
                // code
            }
        }
    }
}
```

**Better Approach:**

```java
// Use early returns or extract to methods
if (!condition1) return;
if (!condition2) return;
if (!condition3) return;
if (!condition4) return;
// code
```

**Real-World Use Case:**

```java
// Form validation
if (username != null) {
    if (username.length() >= 3) {
        if (username.matches("[a-zA-Z0-9]+")) {
            System.out.println("Valid username");
        } else {
            System.out.println("Username must be alphanumeric");
        }
    } else {
        System.out.println("Username too short");
    }
} else {
    System.out.println("Username cannot be null");
}
```