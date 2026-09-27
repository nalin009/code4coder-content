## Control Statements - Decision Making

---
---

### Summary
Decision-making statements are fundamental to programming logic, enabling programs to make intelligent choices based on conditions. Java provides multiple constructs—if-else for flexibility, switch for efficiency with discrete values, and ternary for concise assignments. Modern Java (14+) introduces switch expressions with cleaner syntax and no fallthrough, while Java 21+ adds pattern matching for type-safe switching.

##### Key Takeaways:
- Use if-else for ranges and complex conditions
- Use switch for 5+ discrete values (faster with lookup tables)
- Use ternary operator for simple inline assignments
- Always use braces and include default in switch
- Leverage short-circuit evaluation for safety and performance
- Adopt modern switch expressions (Java 14+) for cleaner code
- Extract complex conditions into named methods for readability

---
---

### 1. Introduction
#### Why This Topic Exists
In the real world, decisions are made based on conditions. If it rains, you carry an umbrella. If you're hungry, you eat. Similarly, programs need the ability to make decisions based on conditions. Without decision-making statements, every program would execute sequentially from top to bottom—no choices, no intelligence, no flexibility.

##### Decision-making statements give programs the power to:
- Make choices based on conditions (if-else, switch)
- Execute different code paths based on input
- Validate data before processing
- Handle multiple scenarios dynamically

#### What Problem Java Is Solving
##### Java provides decision-making statements to:
- Avoid writing redundant code for different scenarios
- Execute code conditionally based on runtime values
- Handle different user inputs dynamically
- Build logic-driven, intelligent applications

Without decision-making statements, you'd need separate programs for every possible scenario—no branching, no flexibility, just rigid execution.

#### Why Beginners Struggle With This Topic
1. Confusion between = (assignment) and == (comparison)
2. Understanding operator precedence in complex conditions
3. Nested if statements become hard to visualize and debug
4. Switch statement fallthrough behavior—forgetting break leads to unexpected execution
5. Not knowing when to use if-else vs switch vs ternary
6. Complex boolean expressions with AND, OR, NOT operators
7. Understanding short-circuit evaluation in logical operators

#### Why Interviewers Ask This (Especially 3–5+ YOE)
- **Foundational knowledge:** Tests basic programming logic and problem-solving
- **Code quality:** Senior developers must write clean, maintainable decision logic
- **Performance awareness:** Knowing when switch is faster than if-else
- **Modern Java features:** Switch expressions (Java 14+), pattern matching (Java 21+)
- **Real-world scenarios:** Input validation, business logic, state machines
- **Debugging skills:** Tracing through complex conditional logic

#### Senior developers are expected to:
- Choose the right decision-making construct for the task
- Write clean, optimized, and readable conditional code
- Avoid common pitfalls (nested if complexity, missing break in switch)
- Know modern Java features (switch expressions)

### 2. Clear Definitions
#### Decision-Making Statement
A decision-making statement is a construct in Java that executes different blocks of code based on whether conditions evaluate to true or false.

#### Conditional Expression
A boolean expression that evaluates to either true or false, used to control program flow.

#### Branch
A separate path of execution in a program, determined by a decision-making statement.

#### Ternary Operator
A shorthand conditional operator (? :) that returns one of two values based on a boolean condition.

#### Interview-Safe Definition:
"Decision-making statements in Java control program flow by executing different code blocks based on boolean conditions. They include if, if-else, else-if ladder, nested if, switch statement, and the ternary operator, enabling programs to make intelligent choices at runtime."

---
---

### 3. Core Concept Explanation
#### How Decision-Making Works at the Language Level
Java's decision-making statements are compiled into bytecode instructions that the JVM executes. The JVM doesn't "understand" if-else or switch—it understands conditional jump instructions, comparisons, and stack operations.

##### Compiler's Role:
- Converts high-level decision statements into conditional jumps (ifeq, ifne, goto)
- Optimizes dead code (unreachable statements after return or guaranteed branches)
- Validates syntax, type checking, and boolean expressions
- For switch statements, generates tableswitch or lookupswitch bytecode

##### JVM's Role:
- Executes bytecode sequentially unless a jump instruction is encountered
- Evaluates conditions at runtime by popping values from the operand stack
- Manages the program counter (PC register) to control which instruction executes next
- Uses branch prediction to optimize frequently executed paths

#### WHY Java Designed Decision-Making This Way
- **Readability:** Borrowed from C/C++ for familiarity and industry standardization
- **Simplicity:** Minimal keywords with clear, unambiguous semantics
- **Flexibility:** Multiple ways to express decisions (if-else, switch, ternary)
- **Performance:** Allows JVM to optimize branches, inline code, and eliminate dead paths
- **Type Safety:** Boolean conditions prevent common C errors (using integers as booleans)

---

#### 3.1. if Statement

##### Syntax:

```java
if (condition) {
    // code to execute if condition is true
}
```

##### How It Works:
- Evaluates the boolean condition
- If true, executes the block
- If false, skips the block
- Control continues to the next statement after the if block

##### Example:

```java
int age = 18;
if (age >= 18) {
    System.out.println("Eligible to vote");
}
System.out.println("Program continues");
```

##### Output:

```java
Eligible to vote
Program continues
```

##### Bytecode Behavior:
- The compiler generates an ifeq (if equal to zero) or ifne (if not equal to zero) instruction
- If the condition is false, the JVM uses a goto instruction to jump past the if block
- The boolean condition is evaluated by comparing stack values

##### Key Point: 
- Single statements don't require braces, but always use them for clarity and safety
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

#### 3.2. if-else Statement

##### Syntax:

```java
if (condition) {
    // executes if condition is true
} else {
    // executes if condition is false
}
```

##### How It Works:
- Evaluates the boolean condition
- If true, executes the if block and skips the else block
- If false, skips the if block and executes the else block
- Exactly one block executes—never both, never neither

##### Example:

```java
int number = 10;
if (number % 2 == 0) {
    System.out.println("Even number");
} else {
    System.out.println("Odd number");
}
```

##### Output:

```java
Even number
```

###### Bytecode Behavior:
- Two branches are created in bytecode
- JVM evaluates the condition and uses conditional jumps to select the branch
- Only one branch executes, improving performance by avoiding unnecessary checks
- Modern JVMs use branch prediction to optimize frequently taken paths

###### Real-World Use Case:

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

#### 3.3. else-if Ladder

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
- Conditions are evaluated sequentially from top to bottom
- The first condition that evaluates to true executes its block
- Once a condition is true, all remaining conditions are skipped
- If no condition is true, the else block executes (if present)

##### Example:

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

##### Output:

```java
Grade B
```

##### Performance Consideration:
- Order matters for performance
- Place the most common condition first to reduce unnecessary checks
- For 5+ conditions on the same variable, consider using switch

##### Example with Optimization:

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

##### Real-World Use Case:

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

#### 3.4. Nested if

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
- Inner if is evaluated only if outer if is true
- Can be nested multiple levels deep (avoid going beyond 3 levels)

##### Example:

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

##### Alternative Using Logical AND:

```java
if (age >= 18 && hasLicense) {
    System.out.println("Can drive");
}
```

##### When to Use Nested vs Logical Operators:
###### Use Nested if when:
- You need different messages/actions for each condition
- Inner logic is complex and benefits from separation
- Early validation saves computation

##### Use Logical AND (&&) when:
- You just need to check if all conditions are true
- Simpler, more readable code
- No intermediate actions needed

##### Deep Nesting Problem:

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

##### Better Approach:

```java
// Use early returns or extract to methods
if (!condition1) return;
if (!condition2) return;
if (!condition3) return;
if (!condition4) return;
// code
```

##### Real-World Use Case:

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

#### 3.5. switch Statement

##### Syntax:

```java
switch (expression) {
    case value1:
        // code
        break;
    case value2:
        // code
        break;
    default:
        // default code
}
```

##### How It Works:
1. Expression is evaluated once
2. Result is compared against each case value
3. When a match is found, execution starts from that case
4. Execution continues until break, return, or end of switch
5. If no case matches, the default block executes (if present)

##### Example:

```java
int day = 3;
switch (day) {
    switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    case 3:
        System.out.println("Wednesday");
        break;
    case 4:
        System.out.println("Thursday");
        break;
    case 5:
        System.out.println("Friday");
        break;
    case 6:
        System.out.println("Saturday");
        break;
    case 7:
        System.out.println("Sunday");
        break;
    default:
        System.out.println("Invalid day");
}
```

##### Output:

```java
Wednesday
```

###### How switch Works Internally (Bytecode Level):
1. **Compiler Role:** The compiler analyzes the case values and chooses an optimization strategy:
  a) **tableswitch (Dense Cases):**
    - Used when case values are closely packed (few gaps)
    - Creates an array-based lookup table
    - Direct O(1) jump to the matching case
    - **Example:** cases 1, 2, 3, 4, 5

  b) **lookupswitch (Sparse Cases):**
    - Used when case values are scattered (many gaps)
    - Performs binary search on sorted case values
    - O(log n) lookup time
    - **Example:** cases 1, 100, 1000, 10000

2. **JVM Role:**
  - Evaluates the expression once and stores the result
  - Uses the bytecode instruction (tableswitch/lookupswitch) to jump directly
  - Much faster than multiple if-else comparisons for 5+ cases

##### Performance Comparison:

|**Number of Cases**|**if-else Time Complexity**|**switch Time Complexity**|
|-------------------|---------------------------|--------------------------|
| 1-3 cases | O(n) - similar performance | O(1) or O(log n) - similar |
| 5+ cases | O(n) - slower | O(1) or O(log n) - faster |
| 10+ cases | O(n) - significantly slower | O(1) or O(log n) - significantly faster |

##### Supported Types in Switch
- **Primitive Types:** byte, short, int, char
- **Wrapper Classes:** Byte, Short, Integer, Character
- **Reference Types:**
  - String (Java 7+)
  - enum (Java 5+)
- **NOT Supported:** long, float, double, boolean

##### Why These Limitations?
1. **long not supported:** Historical design decision from C/C++, kept for consistency
2. **float/double not supported:** Floating-point comparisons are imprecise due to rounding errors
3. **boolean not supported:** Only two values (true/false) make if-else more natural and readable

###### Example of Floating-Point Precision Issue:

```java
double x = 0.1 + 0.2;  // Result: 0.30000000000000004
// Cannot reliably use in switch due to precision
```

#### 3.6. Fallthrough Behavior in Switch:
##### What is Fallthrough?
When a case block doesn't end with break, execution "falls through" to the next case without checking its condition.

##### Example Without Break:

```java
int x = 2;
switch (x) {
    case 1:
        System.out.println("One");
    case 2:
        System.out.println("Two");  // Executes
    case 3:
        System.out.println("Three");  // Also executes (fallthrough)
    default:
        System.out.println("Default");  // Also executes (fallthrough)
}
```

##### Output:

```java
Two
Three
Default
```

##### Intentional Fallthrough (Multiple Cases, Same Logic):

```java
int month = 2;
switch (month) {
    case 12:
    case 1:
    case 2:
        System.out.println("Winter");
        break;
    case 3:
    case 4:
    case 5:
        System.out.println("Spring");
        break;
    case 6:
    case 7:
    case 8:
        System.out.println("Summer");
        break;
    case 9:
    case 10:
    case 11:
        System.out.println("Fall");
        break;
    default:
        System.out.println("Invalid month");
}
```

##### Best Practice:
- Always use break unless fallthrough is intentional
- Document intentional fallthrough with a comment

```java
case 1:
    // Fallthrough intentional - shared logic for cases 1 and 2
case 2:
    System.out.println("Case 1 or 2");
    break;
```

#### 3.7. break Statement in switch
**Purpose:** Exits the switch block immediately and transfers control to the next statement after the switch.

##### Syntax:

```java
break;
```

##### Example:

```java
int option = 2;
switch (option) {
    case 1:
        System.out.println("Option 1");
        break;  // Exits switch
    case 2:
        System.out.println("Option 2");
        break;  // Exits switch
    case 3:
        System.out.println("Option 3");
        break;  // Exits switch
    default:
        System.out.println("Invalid option");
}
System.out.println("After switch");
```

###### Output: 
Option 2
After switch

##### What Happens Without Break:

```java
int option = 2;
switch (option) {
    case 1:
        System.out.println("Option 1");
    case 2:
        System.out.println("Option 2");
    case 3:
        System.out.println("Option 3");
    default:
        System.out.println("Invalid option");
}
}
```

###### Output:

```java
Option 2
Option 3
Invalid option
```

**Best Practice:** Always use break unless intentional fallthrough is needed.

#### 3.8. default Case in switch
**Purpose:** Handles values not explicitly covered by any case; acts as a catch-all.

##### Syntax:

```java
default:
    // code for unmatched values
```


##### Example:

```java
int option = 10;
switch (option) {
    case 1:
        System.out.println("Option 1");
        break;
    case 2:
        System.out.println("Option 2");
        break;
    default:
        System.out.println("Invalid option");
}
```

###### Output: 
```java
Invalid choice: 10
```

##### Important Points:
- default is optional but strongly recommended
- Can be placed anywhere in the switch (conventionally at the end)
- Executes if no case matches
- Should include break if not at the end (to prevent fallthrough)

##### Default Not at the End:

```java
switch (x) {
    case 1:
        System.out.println("One");
        break;
    default:
        System.out.println("Default");
        break;  // Important: prevents fallthrough to case 2
    case 2:
        System.out.println("Two");
        break;
}
```

##### Best Practice:  
- Always include a default case for defensive programming
- Use it to handle unexpected values or log errors
- Even if you think all values are covered, requirements change

#### 3.9. Switch Expressions (Java 14+) [MODERN JAVA]
##### What Are Switch Expressions?
Switch expressions are an enhanced version of the traditional switch statement introduced in Java 14. They can return values directly and use arrow syntax (->) to eliminate the need for break statements.

###### Key Differences from Traditional Switch:
- Returns a value (can be assigned to a variable)
- Arrow syntax (->) prevents fallthrough
- No need for break statements
- Must be exhaustive (all possible values must be handled)
- Cleaner, more concise syntax

##### Traditional Switch vs Switch Expression
###### Traditional Switch:

```java
int day = 2;
String dayType;
switch (day) {
    case 1:
    case 2:
    case 3:
    case 4:
    case 5:
        dayType = "Weekday";
        break;
    case 6:
    case 7:
        dayType = "Weekend";
        break;
    default:
        dayType = "Invalid";
}
System.out.println(dayType);
```

###### Modern Switch Expression:

```java
int day = 2;
String dayType = switch (day) {
    case 1, 2, 3, 4, 5 -> "Weekday";
    case 6, 7 -> "Weekend";
    default -> "Invalid";
};
System.out.println(dayType);
```

###### Benefits:
- 8 lines reduced to 5 lines
- No break needed
- Cannot forget break (no fallthrough bugs)
- Value is returned directly
- More functional programming style

##### Syntax Variants of Switch Expressions
###### 1. Single Expression (Arrow Syntax):

```java
int month = 3;
String season = switch (month) {
    case 12, 1, 2 -> "Winter";
    case 3, 4, 5 -> "Spring";
    case 6, 7, 8 -> "Summer";
    case 9, 10, 11 -> "Fall";
    default -> "Invalid month";
};
```

###### 2. Block with yield Keyword: Use yield when you need multiple statements in a case block.

```java
int score = 85;
String grade = switch (score / 10) {
    case 10, 9 -> "A";
    case 8 -> "B";
    case 7 -> "C";
    case 6 -> "D";
    default -> {
        System.out.println("Score is below 60");
        yield "F";  // yield returns the value
    }
};
System.out.println("Grade: " + grade);
```

**Output:**

```java
Grade: B
```

###### 3. Using yield for Complex Logic:

```java
int number = 15;
String result = switch (number) {
    case 1, 2, 3 -> "Small";
    case 4, 5, 6 -> "Medium";
    default -> {
        if (number < 0) {
            yield "Negative";
        } else if (number > 100) {
            yield "Very Large";
        } else {
            yield "Large";
        }
    }
};
System.out.println(result);
```

**Output:**

```java
Large
```

##### Exhaustiveness in Switch Expressions
###### What Does Exhaustive Mean?
A switch expression must handle all possible values of the expression type. If any value is not covered, the code won't compile.

###### Example with Enum (Exhaustive Check):

```java
enum Day { MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY }

Day day = Day.MONDAY;

// This will NOT compile without default or all cases covered
String dayType = switch (day) {
    case MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY -> "Weekday";
    case SATURDAY, SUNDAY -> "Weekend";
    // No default needed - all enum values covered
};
```

###### If You Miss a Case:

```java
// Compilation error: the switch expression does not cover all possible input values
String dayType = switch (day) {
    case MONDAY -> "Weekday";
    // Error: TUESDAY, WEDNESDAY, etc. not covered
};
```

###### For int, String, etc., default is Required:

```java
int x = 5;
String result = switch (x) {
    case 1 -> "One";
    case 2 -> "Two";
    // Must have default for exhaustiveness
    default -> "Other";
};
```

##### Real-World Example: HTTP Status Code Handling
###### Traditional Switch:

```java
int statusCode = 404;
String message;
switch (statusCode) {
    case 200:
        message = "OK";
        break;
    case 201:
        message = "Created";
        break;
    case 400:
        message = "Bad Request";
        break;
    case 401:
        message = "Unauthorized";
        break;
    case 404:
        message = "Not Found";
        break;
    case 500:
        message = "Internal Server Error";
        break;
    default:
        message = "Unknown Status";
}
System.out.println(message);
```

###### Modern Switch Expression:

```java
int statusCode = 404;
String message = switch (statusCode) {
    case 200 -> "OK";
    case 201 -> "Created";
    case 400 -> "Bad Request";
    case 401 -> "Unauthorized";
    case 404 -> "Not Found";
    case 500 -> "Internal Server Error";
    default -> "Unknown Status";
};
System.out.println(message);
```

##### When to Use Switch Expressions
##### Use Switch Expressions When:
- You need to assign a value based on multiple cases
- You want cleaner, more functional code
- You're using Java 14+
- You want to avoid fallthrough bugs
- Exhaustiveness checking adds safety (enums)

##### Use Traditional Switch When:
- You're on Java 13 or earlier
- You don't need to return a value
- You need intentional fallthrough behavior
- You have complex side effects in each case

##### Pattern Matching for Switch (Java 21+) [PREVIEW/FUTURE]
Java 21 introduced pattern matching in switch expressions, allowing type checking and casting in one step.

**Example:**

```java
Object obj = "Hello";

String result = switch (obj) {
    case String s -> "String of length " + s.length();
    case Integer i -> "Integer: " + i;
    case Long l -> "Long: " + l;
    case null -> "Null value";
    default -> "Unknown type";
};

System.out.println(result);
```

```java
String of length 5
```

###### Benefits:
- No need for instanceof checks and casting
- More readable and concise
- Type-safe at compile time

This feature is in preview/finalized in Java 21+ and represents the future direction of Java.

#### 3.10. Ternary Operator (? :)
##### What is the Ternary Operator?
The ternary operator is a compact, inline way to write simple if-else logic. It's the only operator in Java that takes three operands, hence "ternary."

**Syntax:**

```java
condition ? expression1 : expression2;
```

##### How It Works:
- If condition is true, returns expression1
- If condition is false, returns expression2
- Both expressions must be compatible types

###### Example:

```java
int age = 20;
String result = (age >= 18) ? "Adult" : "Minor";
System.out.println(result);
```

###### Output:

```java
Adult
```

##### Equivalent if-else:

```java
int age = 20;
String result;
if (age >= 18) {
    result = "Adult";
} else {
    result = "Minor";
}
System.out.println(result);
```

##### When to Use Ternary Operator
###### Use Ternary When:
- Simple condition with two outcomes
- Assigning a value based on a condition
- Compact code is preferred (but still readable)
- Initializing variables conditionally

###### Examples:
1. Finding Maximum:

```java
int a = 10, b = 20;
int max = (a > b) ? a : b;
System.out.println("Max: " + max);
```

2. Setting Default Value:

```java
String username = getUserInput();
String displayName = (username != null) ? username : "Guest";
```

3. Conditional Calculation:

```java
int quantity = 50;
double price = (quantity > 100) ? 9.99 : 12.99;
```

4. Display Message:

```java
int score = 75;
System.out.println(score >= 50 ? "Pass" : "Fail");
```

##### Nested Ternary Operator
You can nest ternary operators, but avoid deep nesting as it hurts readability.

###### Example:

```java
int marks = 85;
String grade = (marks >= 90) ? "A" :
               (marks >= 75) ? "B" :
               (marks >= 60) ? "C" : "F";
System.out.println("Grade: " + grade);
```

###### Output:

```java
Grade: B
```

###### Better Approach for Complex Logic:
Use if-else ladder or switch for better readability:

```java
String grade;
if (marks >= 90) {
    grade = "A";
} else if (marks >= 75) {
    grade = "B";
} else if (marks >= 60) {
    grade = "C";
} else {
    grade = "F";
}
```

##### Ternary Operator vs if-else

|**Feature**|**Ternary Operator**|**if-else**|
|-----------|--------------------|-----------|
| Compactness | More compact | More verbose |
| Readability | Good for simple conditions | Better for complex logic |
| Returns a value | Yes (expression) | No (statement) |
| Multiple statements | Not supported | Supported |
| Best for | Assignment, simple choice | Complex logic, multiple actions |

##### When NOT to Use Ternary:

```java
// BAD: Complex logic, hard to read
String result = (user != null && user.isActive() && user.hasPermission("read")) 
                ? "Access granted" 
                : "Access denied";

// BETTER: Use if-else
String result;
if (user != null && user.isActive() && user.hasPermission("read")) {
    result = "Access granted";
} else {
    result = "Access denied";
}
```

##### Common Mistakes with Ternary Operator
###### 1. Type Mismatch:

```java
// Error: incompatible types
String result = (true) ? 1 : "Hello";  // int vs String
```

###### 2. Using Ternary for Side Effects:

```java
// BAD: Ternary is for returning values, not side effects
(score > 50) ? System.out.println("Pass") : System.out.println("Fail");

// GOOD: Use if-else for side effects
if (score > 50) {
    System.out.println("Pass");
} else {
    System.out.println("Fail");
}
```

###### 3. Excessive Nesting:

```java
// BAD: Hard to read
String grade = (m >= 90) ? "A" : (m >= 80) ? "B" : (m >= 70) ? "C" : (m >= 60) ? "D" : "F";

// GOOD: Use if-else or switch
```

##### Real-World Use Cases
###### 1. Setting Configuration:

```java
boolean isProduction = true;
String apiUrl = isProduction ? "https://api.prod.com" : "https://api.dev.com";
```

###### 2. Null Safety:

```java
String name = user.getName();
String displayName = (name != null && !name.isEmpty()) ? name : "Anonymous";
```

###### 3. Conditional CSS Class:

```java
String cssClass = isActive ? "btn-primary" : "btn-disabled";
```

###### 4. Math Operations:

```java
int abs = (number >= 0) ? number : -number;  // Absolute value
```

---
---

### 4. Variations / Types / Categories
#### Decision-Making Constructs:
1. **Simple if -** Single condition check
2. **if-else -** Binary choice (two outcomes)
3. **else-if ladder -** Multiple conditions (sequential checking)
4. **Nested if -** Conditions within conditions
5. **switch statement -** Multiple discrete values (traditional)
6. **Switch expressions -** Modern switch with return value (Java 14+)
7. **Ternary operator -** Inline conditional expression

---
---

### 5. Memory & Performance Impact
#### Stack Memory:
- Boolean expressions are evaluated on the operand stack
- Local variables in if-else blocks are stored on the stack frame
- Each branch may have its own stack frame for local variables
- Variables declared inside if blocks are destroyed when the block exits

###### Example:

```java
if (condition) {
    int x = 10;  // Stored on stack
}  // x is destroyed here
// System.out.println(x);  // Error: x out of scope
```

##### Performance Considerations:
###### 1. Short-Circuit Evaluation:
Java uses short-circuit evaluation for logical operators (&&, ||).

```java
if (obj != null && obj.getName().equals("Test")) {
    // obj.getName() is NOT called if obj is null
    // Prevents NullPointerException
}
```

**How It Works:**
- && (AND): If first condition is false, second is not evaluated
- || (OR): If first condition is true, second is not evaluated
- Saves computation and prevents errors

###### 2. if-else vs switch Performance:

|**Number of Conditions**|**if-else**|**switch (traditional)**|**switch expression**|
|------------------------|-----------|------------------------|---------------------|
| 1-3 conditions | Fast (similar) | Fast (similar) | Fast (similar) |
| 5-10 conditions | O(n) slower | O(1) or O(log n) faster | O(1) or O(log n) faster |
| 10+ conditions | Significantly slower | Significantly faster | Significantly faster |

**Why switch is Faster:**
- Uses tableswitch (O(1) array lookup) for dense cases
- Uses lookupswitch (O(log n) binary search) for sparse cases
- if-else checks conditions sequentially (O(n))

###### 3. Branch Prediction (JVM Optimization):
Modern JVMs use branch prediction to optimize frequently executed paths.

```java
// If condition is usually true, JVM learns this pattern
if (mostlyTrue) {
    // Optimized path
} else {
    // Less optimized
}
```

###### 4. Dead Code Elimination:
Compiler removes unreachable code.

```java
if (true) {
    System.out.println("Always executed");
} else {
    System.out.println("Never executed");  // Removed by compiler
}
```

#### Heap Memory:
##### Objects created in conditional blocks:
```java
if (condition) {
    String s = new String("Hello");  // Allocated on heap
}  // s goes out of scope, but object remains until GC
```

##### Best Practice:

```java
String s;  // Declare outside
if (condition) {
    s = "Hello";  // Use string literal (interned in pool)
} else {
    s = "World";
}
```

---
---

### 6. Real-World Use Cases
#### Beginner Level:
##### Age Verification:

```java
int age = 16;
if (age >= 18) {
    System.out.println("Can vote");
} else {
    System.out.println("Cannot vote");
}
```

##### Grade Calculator:

```java
int marks = 75;
String grade;
if (marks >= 90) {
    grade = "A";
} else if (marks >= 75) {
    grade = "B";
} else if (marks >= 60) {
    grade = "C";
} else {
    grade = "F";
}
```

##### Day of Week:

```java
int day = 3;
switch (day) {
    case 1 -> System.out.println("Monday");
    case 2 -> System.out.println("Tuesday");
    case 3 -> System.out.println("Wednesday");
    default -> System.out.println("Other day");
}
```

#### Interview Level:
##### Leap Year Check:

```java
int year = 2024;
if ((year % 4 == 0 && year % 100 != 0) || (year % 400 == 0)) {
    System.out.println("Leap year");
} else {
    System.out.println("Not a leap year");
}
```

##### Largest of Three Numbers:

```java
int a = 10, b = 20, c = 15;
int largest = (a > b) ? ((a > c) ? a : c) : ((b > c) ? b : c);
System.out.println("Largest: " + largest);
```

##### Character Type Check:

```java
char ch = 'A';
if (ch >= 'a' && ch <= 'z') {
    System.out.println("Lowercase");
} else if (ch >= 'A' && ch <= 'Z') {
    System.out.println("Uppercase");
} else if (ch >= '0' && ch <= '9') {
    System.out.println("Digit");
} else {
    System.out.println("Special character");
}
```

#### Production Level:
##### HTTP Status Code Handling:

```java
String handleResponse(int statusCode) {
    return switch (statusCode) {
        case 200, 201, 204 -> "Success";
        case 400, 401, 403, 404 -> "Client error";
        case 500, 502, 503 -> "Server error";
        default -> "Unknown status: " + statusCode;
    };
}
```

##### User Role Authorization:

```java
boolean hasAccess(String role, String resource) {
    return switch (role) {
        case "ADMIN" -> true;
        case "USER" -> resource.equals("read") || resource.equals("write");
        case "GUEST" -> resource.equals("read");
        default -> false;
    };
}
```

##### Payment Method Selection:

```java
void processPayment(String method, double amount) {
    switch (method.toUpperCase()) {
        case "CREDIT_CARD":
            processCreditCard(amount);
            break;
        case "DEBIT_CARD":
            processDebitCard(amount);
            break;
        case "UPI":
            processUPI(amount);
            break;
        case "NET_BANKING":
            processNetBanking(amount);
            break;
        default:
            throw new IllegalArgumentException("Invalid payment method: " + method);
    }
}
```

---
---

### 7. Important Diagrams (Described in Words)
#### Diagram 1: If Statement Flow

```java
Start → Evaluate Condition → True? → Execute Block → Continue
                           → False? → Skip Block → Continue
```

#### Diagram 2: If-Else Flow

```java
Start → Evaluate Condition → True? → Execute If Block → End
                           → False? → Execute Else Block → End
```

#### Diagram 3: Else-If Ladder Flow

```java
Start → Condition1? → True → Block1 → End
                    → False → Condition2? → True → Block2 → End
                                         → False → Condition3? → True → Block3 → End
                                                              → False → Default Block → End
```

#### Diagram 4: Switch Statement Flow (Traditional)

```java
Start → Evaluate Expression → 
        Case 1 Match? → Execute → Break → End
        Case 2 Match? → Execute → Break → End
        Case 3 Match? → Execute → Break → End
        No Match? → Default → End
```

#### Diagram 5: Switch Expression Flow (Java 14+)

```java
Start → Evaluate Expression → 
        Case 1 Match? → Return Value1 → End
        Case 2 Match? → Return Value2 → End
        Case 3 Match? → Return Value3 → End
        No Match? → Return Default → End
```

#### Diagram 6: Ternary Operator Flow

```java
Start → Evaluate Condition → True? → Return Expression1 → End
                            → False? → Return Expression2 → End
```

---
---

### 8. Common Mistakes & Misconceptions
#### 1. Using = Instead of ==

```java
int x = 10;
if (x = 5) {  // Compilation error: incompatible types
    System.out.println("Test");
}
```

###### Correct:

```java
if (x == 5) {  // Comparison operator
    System.out.println("Test");
}
```

###### Why This Happens:
In C/C++, assignment returns the assigned value, allowing if (x = 5). Java prevents this by requiring boolean expressions.

#### 2. Forgetting break in Switch

```java
int x = 2;
switch (x) {
    case 1:
        System.out.println("One");
    case 2:
        System.out.println("Two");  // Executes
    case 3:
        System.out.println("Three");  // Also executes (fallthrough)
}
```

###### Output:

```java
Two
Three
```

**Fix:** Always add break or use switch expressions (Java 14+).

#### 3. Comparing Strings with ==

```java
String s1 = new String("Hello");
String s2 = new String("Hello");
if (s1 == s2) {  // False - compares references, not content
    System.out.println("Equal");
}
```

###### Correct:

```java
if (s1.equals(s2)) {  // True - compares content
    System.out.println("Equal");
}
```

#### 4. Not Checking for null Before Method Calls

```java
String name = null;
if (name.equals("John")) {  // NullPointerException
    System.out.println("Match");
}
```

###### Correct:

```java
if (name != null && name.equals("John")) {  // Short-circuit prevents NPE
    System.out.println("Match");
}
```

###### Better (Yoda Conditions):

```java
if ("John".equals(name)) {  // Safe even if name is null
    System.out.println("Match");
}
```

#### 5. Using Float/Double in Switch

```java
double x = 3.14;
switch (x) {  // Compilation error: incompatible types
    case 3.14:
        System.out.println("Pi");
}
```

**Fix:** Use if-else for floating-point comparisons.

#### 6. Scope Confusion

```java
if (true) {
    int x = 10;
}
System.out.println(x);  // Error: x out of scope
```

Fix: Declare variable outside if block if needed later.

#### 7. Missing default in Switch

```java
int x = 10;
switch (x) {
    case 1:
        System.out.println("One");
        break;
    case 2:
        System.out.println("Two");
        break;
    // No default - if x is 10, nothing happens
}
```

Best Practice: Always include default for safety.


#### 8. Complex Boolean Expressions Without Parentheses

```java
if (a > 5 && b < 10 || c == 20) {  // Confusing precedence
    // Code
}
```

###### Better:

```java
if ((a > 5 && b < 10) || c == 20) {  // Clear intent
    // Code
}
```

#### 9. Ternary Operator Type Mismatch

```java
String result = (true) ? 1 : "Hello";  // Error: incompatible types
```

Fix: Both expressions must return compatible types.

#### 10. Deep Nesting

```java
if (condition1) {
    if (condition2) {
        if (condition3) {
            if (condition4) {
                // Hard to read and maintain
            }
        }
    }
}
```

###### Better (Early Returns):

```java
if (!condition1) return;
if (!condition2) return;
if (!condition3) return;
if (!condition4) return;
// Code here
```

---
---

### 9. Best Practices (5+ YOE Expectation)
#### 1. Always Use Braces

```java
// BAD
if (condition)
    statement;

// GOOD
if (condition) {
    statement;
}
```

Why: Prevents bugs when adding more statements later.

#### 2. Prefer Switch Expressions Over Traditional Switch (Java 14+)

```java
// OLD
String day;
switch (num) {
    case 1: day = "Monday"; break;
    case 2: day = "Tuesday"; break;
    default: day = "Invalid";
}

// MODERN
String day = switch (num) {
    case 1 -> "Monday";
    case 2 -> "Tuesday";
    default -> "Invalid";
};
```

#### 3. Use Switch for 5+ Discrete Values

```java
// Less efficient
if (status == 200) { }
else if (status == 201) { }
else if (status == 400) { }
else if (status == 401) { }
else if (status == 404) { }
else if (status == 500) { }

// Better
switch (status) {
    case 200, 201 -> handleSuccess();
    case 400, 401, 404 -> handleClientError();
    case 500 -> handleServerError();
}
```

#### 4. Use Ternary for Simple Assignments Only

```java
// GOOD: Simple, readable
int max = (a > b) ? a : b;

// BAD: Too complex
String result = (user != null && user.isActive() && user.hasRole("admin")) 
                ? "Full access" 
                : (user != null && user.isActive()) 
                  ? "Limited access" 
                  : "No access";

// BETTER: Use if-else
```

#### 5. Always Include default in Switch

```java
switch (value) {
    case 1 -> handle1();
    case 2 -> handle2();
    default -> logUnexpectedValue(value);  // Defensive programming
}
```

#### 6. Use Short-Circuit Evaluation for Safety

```java
// GOOD: Prevents NullPointerException
if (obj != null && obj.isValid()) { }

// BAD: Can throw NPE
if (obj.isValid() && obj != null) { }
```


#### 7. Avoid Magic Numbers - Use Constants

```java
// BAD
if (status == 200) { }

// GOOD
private static final int HTTP_OK = 200;
if (status == HTTP_OK) { }
```


#### 8. Document Intentional Fallthrough

```java
switch (x) {
    case 1:
        // Fallthrough intentional - shared logic for 1 and 2
    case 2:
        handleBoth();
        break;
}
```


#### 9. Prefer Positive Conditions

```java
// LESS READABLE
if (!isInvalid) {
    process();
}

// MORE READABLE
if (isValid) {
    process();
}
```


#### 10. Extract Complex Conditions to Methods

```java
// BAD
if (user != null && user.getAge() >= 18 && user.hasLicense() && user.getExperience() > 2) {
    allowDriving();
}

// GOOD
if (canDrive(user)) {
    allowDriving();
}

private boolean canDrive(User user) {
    return user != null 
        && user.getAge() >= 18 
        && user.hasLicense() 
        && user.getExperience() > 2;
}
```

---
---

### 10. Interview-Oriented Key Points (Quick Revision)
- **if vs switch:** Switch is faster for 5+ discrete values (O(1) vs O(n))
- Switch supports: int, char, String, enum, byte, short (NOT long, float, double, boolean)
- Fallthrough: Missing break causes execution to continue to next case
- Default case: Always include for safety and handling unexpected values
- Switch expressions (Java 14+): Return values, no break needed, arrow syntax
- Ternary operator: Compact if-else for simple assignments
- Short-circuit evaluation: && and || don't evaluate second operand if unnecessary
- == vs equals(): == compares references, equals() compares content
- Null safety: Always check null before method calls or use short-circuit
- Best practices: Always use braces, prefer switch expressions, extract complex conditions
- Pattern matching (Java 21+): Type checking and casting in switch
- Exhaustiveness: Switch expressions must handle all possible values

---
---

### 11. One-Line Exam / Interview Answer
"Decision-making statements in Java control program flow through conditional execution using if-else for ranges and complex conditions, switch for discrete values with O(1) lookup, ternary operator for inline assignments, and modern switch expressions (Java 14+) that return values without fallthrough."

---
---

### 12. Conclusion
This knowledge is foundational and remains valid through Java 25, with continuous evolution toward more expressive and type-safe constructs.