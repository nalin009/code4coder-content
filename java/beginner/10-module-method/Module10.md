## Methods

---
---

### Summary
Methods are the fundamental building blocks of Java programs. They enable code reusability, modularity, and maintainability — principles essential to professional software development.

**Key Takeaways:**

1. Methods encapsulate behavior and are invoked using the call stack mechanism
2. Java uses pass-by-value for both primitives and object references
3. Method overloading provides flexibility through compile-time polymorphism
4. Recursion is powerful but comes with memory overhead and StackOverflowError risk
5. The main() method serves as the JVM entry point with a specific signature
6. Understanding stack frames, memory allocation, and method resolution is crucial for advanced interviews

**For Beginners:**  
Master the basics: declaration, calling, parameters vs arguments, return types.

**For Interview Preparation:**  
Focus on pass-by-value, method overloading resolution, recursion depth, and main() method variations.

**For Experienced Developers:**  
Apply best practices: single responsibility, fail-fast validation, small methods, proper exception handling, and performance considerations.

---
---

### 1. Introduction
#### Why This Topic Exists
In real-world software development, you cannot write all logic in a single place. Imagine writing a 10,000-line program inside the main() method — it would be unmaintainable, unreadable, and impossible to debug. Methods exist to break down complex problems into smaller, reusable, and testable units of code.
Java is an object-oriented language, and methods represent the behavior of objects. Without methods, Java would lose its ability to model real-world entities effectively.

#### What Problem Java Is Solving
##### Methods solve three critical problems:
- Code Reusability — Write once, use multiple times
- Modularity — Break complex logic into smaller pieces
- Maintainability — Update logic in one place, reflected everywhere

#### Why Beginners Struggle With This Topic
##### Beginners often confuse:
- Method declaration vs calling
- Parameters vs arguments
- Pass-by-value vs pass-by-reference (Java does NOT have pass-by-reference)
- Return type vs void
- When to use method overloading vs different method names

These concepts require understanding how the call stack and memory allocation work, which is not immediately visible in code.

#### Why Interviewers Ask This (Especially 3–5+ YOE)
##### For experienced developers, interviewers focus on:
- Memory implications of method calls (stack frames, recursion limits)
- Method overloading resolution at compile-time
- main() method variations and JVM internals
- Recursion optimization and stack overflow scenarios
- Pass-by-value behavior with objects (reference passing, not object passing)

This topic separates candidates who merely write code from those who understand how code executes at runtime.

---
---

### 2. Clear Definitions
#### What is a Method?

##### Simple Definition:
A method is a block of code that performs a specific task and can be reused multiple times by calling its name.

##### Interview-Safe Definition:
A method is a named block of statements defined inside a class that encapsulates a unit of functionality. It can accept inputs (parameters), perform operations, and optionally return a result. Methods are invoked using the call stack mechanism, and each invocation creates a new stack frame in memory.

##### Technical Definition:
In Java, a method is a member of a class consisting of a method signature (name, parameters, return type) and a method body. Methods are resolved at compile-time (for static binding) or runtime (for dynamic binding via polymorphism). Each method call pushes a new frame onto the JVM call stack containing local variables and the program counter.

---
---

### 3. Core Concept Explanation
#### Step-by-Step Explanation
##### 3.1 Method Declaration
A method declaration defines the method's structure. Syntax:

```java
<access-modifier> <non-access-modifier> <return-type> <method-name>(<parameters>) {
    // method body
}
```

**Example:**

```java
public static int add(int a, int b) {
    return a + b;
}
```

###### Breakdown:
- public — Access modifier (who can call this method)
- static — Non-access modifier (belongs to class, not instance)
- int — Return type (what this method gives back)
- add — Method name (identifier)
- (int a, int b) — Parameter list (inputs)
- return a + b; — Method body (logic)

##### 3.2 Method Calling
Calling a method transfers control to that method's code block.

###### Syntax:

```java
<method-name>(<arguments>);
```

**Example:**

```java
int result = add(5, 10);
System.out.println(result); // Output: 15
```

###### What Happens at Runtime:
1. JVM pushes a new stack frame for add() onto the call stack
2. Parameters a=5 and b=10 are copied into this frame
3. Method executes: a + b = 15
4. Result 15 is returned to the caller
5. Stack frame for add() is popped and destroyed
6. Control returns to the caller

###### Compiler vs JVM Behavior:
- Compile-time: Compiler checks method signature, return type compatibility, access permissions
- Runtime: JVM allocates stack memory, executes bytecode, manages stack frames

##### 3.3 Return Type
The return type specifies what kind of data the method will return.

###### Types:
1. Primitive types: int, double, boolean, etc.
2. Reference types: String, Object, custom classes
3. void: Method does not return anything

**Example:**

```java
public int getAge() {
    return 25;
}

public void printMessage() {
    System.out.println("Hello");
    // no return statement needed
}
```

###### Key Rule:
If return type is NOT void, the method MUST return a value of that type on all code paths. Failing to do so causes a compile-time error.

###### Example of Compile Error:

```java
public int getNumber() {
    if (Math.random() > 0.5) {
        return 10;
    }
    // Compiler error: missing return statement
}
```
###### Fix:

```java
public int getNumber() {
    if (Math.random() > 0.5) {
        return 10;
    }
    return 0; // All paths covered
}
```

##### 3.4 Parameters vs Arguments
Parameters: Variables declared in the method signature (placeholders)

Arguments: Actual values passed when calling the method

**Example:**

```java
// a and b are PARAMETERS
public static int multiply(int a, int b) {
    return a * b;
}

// 5 and 10 are ARGUMENTS
int result = multiply(5, 10);
```

###### Memory Perspective:
- Parameters are local variables created in the method's stack frame
- Arguments are copied into these parameters (pass-by-value)

##### 3.5 Pass-by-Value in Java (CRITICAL CONCEPT)
Java is STRICTLY pass-by-value. Always. No exceptions.

###### What does this mean?
When you pass a variable to a method, Java copies the value of that variable into the method's parameter.

###### For Primitives:

```java
public static void modifyPrimitive(int x) {
    x = 100; // Only modifies the COPY
}

public static void main(String[] args) {
    int num = 50;
    modifyPrimitive(num);
    System.out.println(num); // Output: 50 (unchanged)
}
```

Why?
The value 50 is copied into parameter x. Changing x does NOT affect num.

###### For Objects (Tricky Part):

```java
class Person {
    String name;
}

public static void modifyObject(Person p) {
    p.name = "Alice"; // Modifies the object
}

public static void main(String[] args) {
    Person person = new Person();
    person.name = "Bob";
    modifyObject(person);
    System.out.println(person.name); // Output: Alice
}
```

###### What happened here?
- The reference value (memory address) is copied
- Both person and p point to the SAME object in heap memory
- Changing the object via p affects the original object
- BUT you cannot reassign p and affect person:

```java
public static void reassignObject(Person p) {
    p = new Person(); // Only reassigns the COPY
    p.name = "Charlie";
}

public static void main(String[] args) {
    Person person = new Person();
    person.name = "Bob";
    reassignObject(person);
    System.out.println(person.name); // Output: Bob (unchanged)
}
```

###### Interview Key Point:
Java does NOT have pass-by-reference. It passes references by value. The reference itself is copied, not the object.

##### 3.6 Method Overloading
Method overloading allows multiple methods with the same name but different parameter lists in the same class.

###### Rules:
1. Method name must be identical
2. Parameter list must differ (number, type, or order)
3. Return type alone does NOT determine overloading
4. Access modifiers can be different

**Example:**

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
    
    public double add(double a, double b) {
        return a + b;
    }
    
    public int add(int a, int b, int c) {
        return a + b + c;
    }
}
```

###### Compile-Time Resolution:
The compiler selects the correct method based on:
1. Number of arguments
2. Type of arguments
3. Order of arguments

**Example:**

```java
Calculator calc = new Calculator();
calc.add(5, 10);        // Calls add(int, int)
calc.add(5.5, 10.5);    // Calls add(double, double)
calc.add(5, 10, 15);    // Calls add(int, int, int)
```

###### Common Mistake:

```java
// This does NOT compile
public int getValue() { return 10; }
public double getValue() { return 10.5; }
// Error: Method already defined with same signature
```

Why?
Overloading is determined by parameters, NOT return type.
Type Promotion in Overloading:
If an exact match is not found, Java promotes types:

```java
public void print(int x) {
    System.out.println("int: " + x);
}

public void print(long x) {
    System.out.println("long: " + x);
}

print(10);   // Exact match: calls print(int)
byte b = 5;
print(b);    // Promotion: byte → int
```

Promotion Order:
byte → short → int → long → float → double

###### Ambiguity:

```java
public void show(int a, double b) { }
public void show(double a, int b) { }

show(5, 10); // Compile error: Ambiguous method call
```

##### 3.7 Recursion Deep Dive
Recursion is when a method calls itself.

###### Structure:
  1. Base case — Stops recursion
  2. Recursive case — Method calls itself with modified input

**Example: Factorial**

```java
public static int factorial(int n) {
    // Base case
    if (n == 0 || n == 1) {
        return 1;
    }
    // Recursive case
    return n * factorial(n - 1);
}
```

**Call Stack Visualization for factorial(3):**

```java
factorial(3)
  → 3 * factorial(2)
       → 2 * factorial(1)
            → returns 1
       → returns 2 * 1 = 2
  → returns 3 * 2 = 6
```

###### Memory Impact:
Each recursive call creates a new stack frame. Deep recursion can cause StackOverflowError.

**Example:**

```java
public static void infiniteRecursion() {
    infiniteRecursion(); // No base case
}
```

**Result:** `StackOverflowError` because JVM stack memory is exhausted.

**JVM Stack Size:**  
Default stack size varies (typically 1MB per thread). You can adjust it:

```java
java -Xss2m MyClass
```

###### Recursion vs Iteration:

|**Aspect**|**Recursion**|**Iteration**|
|----------|-------------|-------------|
| Memory | Higher (stack frames) | Lower (loop variables) |
| Readability | Often clearer for tree/graph problems | Better for simple loops |
| Performance | Function call overhead | Faster |
| Risk | StackOverflowError | Infinite loop (still fixable) |

###### When to Use Recursion:
- Tree traversal (preorder, inorder, postorder)
- Divide-and-conquer algorithms (merge sort, quicksort)
- Backtracking problems (N-Queens, Sudoku solver)
- Mathematical sequences (Fibonacci, factorial)

###### Tail Recursion:
A special form where the recursive call is the LAST operation.

```java
// Not tail-recursive
public static int factorial(int n) {
    if (n == 1) return 1;
    return n * factorial(n - 1); // Multiplication AFTER recursive call
}

// Tail-recursive
public static int factorialTail(int n, int accumulator) {
    if (n == 1) return accumulator;
    return factorialTail(n - 1, n * accumulator); // Recursive call is LAST
}
```

Note: Java does NOT optimize tail recursion (unlike Scala, Kotlin with tailrec). The JVM does not eliminate tail calls. This behavior is unchanged till Java 25.

##### 3.8 main() Method Variations Deep Dive
The main() method is the entry point of a Java application.
###### Standard Declaration:

```java
public static void main(String[] args) { }
```

###### Why each keyword?
1. public — JVM must access it from outside the class
2. static — JVM calls it WITHOUT creating an instance
3. void — Does not return anything to the JVM
4. main — Standard name recognized by JVM
5. String[] args — Command-line arguments

###### Valid Variations (All Compile Successfully):

```java
// 1. Array notation variations
public static void main(String args[]) { }      // Valid
public static void main(String[] args) { }      // Valid (preferred)

// 2. Varargs (Java 5+)
public static void main(String... args) { }     // Valid

// 3. Different array names
public static void main(String[] xyz) { }       // Valid (parameter name doesn't matter)

// 4. Final modifier
public static final void main(String[] args) { } // Valid

// 5. Strictfp modifier (till Java 16, implicit after Java 17)
public static strictfp void main(String[] args) { } // Valid (but unnecessary after Java 17)

// 6. Synchronized modifier
public static synchronized void main(String[] args) { } // Valid (but pointless)
```

###### Invalid Variations:

```java
// 1. Missing static
public void main(String[] args) { }
// Error: Main method is not static

// 2. Missing public
static void main(String[] args) { }
// Error: Main method is not public (JVM cannot access it)

// 3. Wrong return type
public static int main(String[] args) { return 0; }
// Error: Main method must return void

// 4. Wrong parameter type
public static void main(int[] args) { }
// Error: Main method must have String[] parameter

// 5. No parameters
public static void main() { }
// Error: Main method must have exactly one parameter
```

###### Command-Line Arguments:

```java
public static void main(String[] args) {
    for (String arg : args) {
        System.out.println(arg);
    }
}
```

###### Run:

```java
java MyClass arg1 arg2 arg3
```

**Output:**

```java
arg1
arg2
arg3
```

###### Key Points:
- Arguments are stored in a String array
- Index starts at 0
- If no arguments provided, args.length == 0 (NOT null)

###### Multiple main() Methods (Overloading):

```java
public class Test {
    // JVM entry point
    public static void main(String[] args) {
        System.out.println("JVM main");
        main(10);
    }
    
    // Overloaded main
    public static void main(int x) {
        System.out.println("Overloaded main: " + x);
    }
}
```

**Output:**

```java
JVM main
Overloaded main: 10
```

###### JVM Internals:
The JVM searches for a method with exact signature: public static void main(String[]). It does NOT recognize overloaded versions as entry points.

**Why Java Designed It This Way:**
1. Static: No object creation overhead at startup
2. Public: JVM launcher must access it
3. Void: No return value needed (exit codes handled via System.exit())
4. String[]: Flexible command-line input

---
---

### 4 Variations / Types / Categories
#### 4.1 Based on Return Type
  1. Value-returning methods — Return a value
  2. Void methods — Perform actions without returning

#### 4.2 Based on Parameters
  1. Parameterless methods — No inputs
  2. Parameterized methods — Accept inputs
  3. Varargs methods — Variable-length arguments (Java 5+)

#### 4.3 Based on Binding
  1. Static methods — Resolved at compile-time (early binding)
  2. Instance methods — Resolved at runtime (late binding, polymorphism)

#### 4.4 Based on Access
  1. Public methods — Accessible everywhere
  2. Private methods — Accessible only within the class
  3. Protected methods — Accessible within package and subclasses
  4. Default (package-private) methods — Accessible within the package

#### 4.5 Based on Inheritance Behavior
  1. Final methods — Cannot be overridden
  2. Abstract methods — Must be overridden
  3. Native methods — Implemented in native code (C/C++)

---
---

### 5 Memory & Performance Impact
#### 5.1 Stack Memory
##### Each method call creates a stack frame containing:
- Local variables
- Parameters
- Return address
- Operand stack (for intermediate computations)

##### Stack Frame Lifecycle:
- Push — When method is called
- Execute — Method body runs
- Pop — When method returns

**Example:**

```java
public static void methodA() {
    int x = 10;
    methodB(x);
}

public static void methodB(int y) {
    int z = y + 5;
}
```

**Stack State:**

```java
| methodB (y=10, z=15) |  ← Top of stack
| methodA (x=10)       |
| main()               |
```

After `methodB` completes:

```java
| methodA (x=10)       |  ← Top of stack
| main()               |
```

#### 5.2 Heap Memory
Objects created inside methods are stored in the heap.

```java
public static Person createPerson() {
    Person p = new Person(); // Object in heap
    return p; // Reference returned
}
```

##### Key Point:
- Even after the method returns, if the object is still referenced, it remains in the heap until garbage collected.

#### 5.3 Method Area (Metaspace in Java 8+)
- Method bytecode is stored here
- Class metadata
- Static variables

#### 5.4 Performance Considerations
##### Method Call Overhead:
- Each call involves stack frame creation/destruction
- Not free, but modern JVMs optimize aggressively
- JIT compiler inlines small methods

##### Inlining:
JIT may replace method calls with method body for frequently called small methods.

**Example:**

```java
public static int add(int a, int b) {
    return a + b;
}

// JIT may inline as:
int result = x + y; // Direct computation, no call
```

##### Recursion Overhead:
- Deep recursion = many stack frames
- Slower than iteration
- Risk of StackOverflowError

###### Best Practice:
For performance-critical code with deep recursion, consider converting to iteration.

---
---

### 6 Real-World Use Cases
#### 6.1 Beginner Level
Use Case: Input validation

```java
public static boolean isValidAge(int age) {
    return age >= 18 && age <= 100;
}

public static void main(String[] args) {
    int userAge = 25;
    if (isValidAge(userAge)) {
        System.out.println("Valid age");
    } else {
        System.out.println("Invalid age");
    }
}
```

#### 6.2 Interview Level
Use Case: Finding maximum in array using recursion

```java
public static int findMax(int[] arr, int index) {
    // Base case
    if (index == arr.length - 1) {
        return arr[index];
    }
    // Recursive case
    int maxOfRest = findMax(arr, index + 1);
    return Math.max(arr[index], maxOfRest);
}

public static void main(String[] args) {
    int[] numbers = {3, 7, 2, 9, 5};
    System.out.println("Max: " + findMax(numbers, 0)); // Output: 9
}
```

#### 6.3 Production Level
Use Case: Database connection management

```java
public class DatabaseManager {
    
    private static Connection getConnection() throws SQLException {
        String url = "jdbc:mysql://localhost:3306/mydb";
        return DriverManager.getConnection(url, "user", "password");
    }
    
    public static void executeQuery(String query) {
        Connection conn = null;
        Statement stmt = null;
        try {
            conn = getConnection();
            stmt = conn.createStatement();
            ResultSet rs = stmt.executeQuery(query);
            // Process results
        } catch (SQLException e) {
            handleException(e);
        } finally {
            closeResources(stmt, conn);
        }
    }
    
    private static void closeResources(AutoCloseable... resources) {
        for (AutoCloseable resource : resources) {
            if (resource != null) {
                try {
                    resource.close();
                } catch (Exception e) {
                    // Log exception
                }
            }
        }
    }
    
    private static void handleException(SQLException e) {
        // Centralized exception handling
        System.err.println("Database error: " + e.getMessage());
    }
}
```

**Why Methods Matter Here:**
- `getConnection()` — Reusable connection logic
- `executeQuery()` — Encapsulates query execution
- `closeResources()` — Prevents resource leaks
- `handleException()` — Centralized error handling

---
---

### 7 Important Diagrams (Described in Words)
#### Diagram 1: Method Call Stack Execution

**Scenario:** `main()` calls `methodA()`, which calls `methodB()`

**Description:**

```java
Initial State:
Stack: [main()]

After main() calls methodA():
Stack: [main()] → [methodA()]

After methodA() calls methodB():
Stack: [main()] → [methodA()] → [methodB()]

After methodB() returns:
Stack: [main()] → [methodA()]

After methodA() returns:
Stack: [main()]

After main() returns:
Stack: []
```

#### Diagram 2: Pass-by-Value with Primitives

**Description:**

```java
Code: int x = 10; modifyValue(x);

Stack State:
┌─────────────────┐
│ main()          │
│   x = 10        │ ← Original variable
└─────────────────┘
        ↓
┌─────────────────┐
│ modifyValue()   │
│   param = 10    │ ← Copy of value
│   param = 100   │ ← Modified (does not affect x)
└─────────────────┘

After method returns:
x still equals 10
```

#### Diagram 3: Pass-by-Value with Objects

**Description:**

```java
Code: Person p = new Person("Bob"); modifyPerson(p);

Heap:
┌──────────────────┐
│ Person object    │
│   name = "Bob"   │ ← Single object in heap
└──────────────────┘
         ↑
         │ (both reference same object)
         │
    ┌────┴────┐
    │         │
Stack:     Stack:
main()     modifyPerson()
p = 0x100  param = 0x100 (copy of reference)

When param modifies the object:
Heap:
┌──────────────────┐
│ Person object    │
│   name = "Alice" │ ← Modified via param
└──────────────────┘

Both p and param see the change
```

#### Diagram 4: Recursion Call Stack (Factorial)

**Description:**

```java
factorial(3) call sequence:

Stack grows DOWN as recursion deepens:

┌─────────────────────┐
│ factorial(3)        │
│   n = 3             │
│   Waiting for:      │
│   3 * factorial(2)  │
└─────────────────────┘
         ↓
┌─────────────────────┐
│ factorial(2)        │
│   n = 2             │
│   Waiting for:      │
│   2 * factorial(1)  │
└─────────────────────┘
         ↓
┌─────────────────────┐
│ factorial(1)        │
│   n = 1             │
│   Returns: 1        │ ← Base case reached
└─────────────────────┘

Stack unwinds UP as results return:

factorial(1) returns 1
factorial(2) returns 2 * 1 = 2
factorial(3) returns 3 * 2 = 6
```

#### Diagram 5: Method Overloading Resolution

**Description:**

```java
Method declarations:
1. add(int, int)
2. add(double, double)
3. add(int, int, int)

Method call: add(5, 10)

Compiler checks:
┌─────────────────────────┐
│ Number of arguments: 2  │ ← Eliminates option 3
└─────────────────────────┘
         ↓
┌─────────────────────────┐
│ Type of arguments:      │
│   arg1 = int            │
│   arg2 = int            │ ← Exact match: option 1
└─────────────────────────┘
         ↓
Compiler binds to: add(int, int)
```

---
---

### 8 Common Mistakes & Misconceptions
#### Mistake 1: Confusing Parameters with Arguments
Wrong Understanding:
"Parameters and arguments are the same thing."

Reality:
Parameters are declared in method signature; arguments are passed during method call.

Example:

```java
// a, b are PARAMETERS
public static void print(int a, int b) { }

// 5, 10 are ARGUMENTS
print(5, 10);
```

#### Mistake 2: Believing Java Has Pass-by-Reference
Wrong Understanding:
"Java passes objects by reference."

Reality:
Java passes references by value. The reference itself is copied.

Proof:

```java
public static void changeReference(Person p) {
    p = new Person("Alice"); // Reassigns local reference only
}

public static void main(String[] args) {
    Person person = new Person("Bob");
    changeReference(person);
    System.out.println(person.name); // Output: Bob (unchanged)
}
```

#### Mistake 3: Method Overloading Based on Return Type
Wrong Code:

```java
public int getValue() { return 1; }
public double getValue() { return 1.0; } // Compile error
```

Reality:
Return type does NOT participate in overloading. Only parameter list matters.

#### Mistake 4: Infinite Recursion Without Base Case
Wrong Code:

```java
public static int sum(int n) {
    return n + sum(n - 1); // No base case
}
```

Result:
StackOverflowError
Fix:

```java
public static int sum(int n) {
    if (n == 0) return 0; // Base case
    return n + sum(n - 1);
}
```

#### Mistake 5: Modifying Arrays in Methods
Confusing Behavior:

```java
public static void modifyArray(int[] arr) {
    arr[0] = 100; // Modifies original array
}

public static void main(String[] args) {
    int[] numbers = {1, 2, 3};
    modifyArray(numbers);
    System.out.println(numbers[0]); // Output: 100
}
```

Why?
Arrays are objects. The reference is passed by value, but the array content is in the heap. Modifications affect the original array.

#### Mistake 6: Assuming main() Can Have Any Signature
Wrong Belief:
"Any method named main will run."

Reality:
Only public static void main(String[]) is recognized by JVM as entry point.

#### Mistake 7: Not Handling Method Return Values
Bad Practice:

```java
public static int calculate() {
    return 42;
}

public static void main(String[] args) {
    calculate(); // Return value ignored
}
```

Better Practice:

```java
int result = calculate();
// Use result
```

#### Mistake 8: Deep Recursion Without Considering Stack Limits
Problem:

```java
public static int fibonacci(int n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

fibonacci(50); // Extremely slow and might overflow
```

Solution:
Use iteration or memoization for large values.

---
---

### 9 Best Practices (5+ YOE Expectation)
#### Practice 1: Method Naming Conventions

Good:

```java
public boolean isValid()       // Boolean methods: is/has/can
public void processData()      // Action methods: verb
public int getUserCount()      // Getter methods: get
public void setUserName()      // Setter methods: set
```

Bad: 

```java
public void xyz()              // Meaningless name
public boolean validation()    // Should be isValid()
```

#### Practice 2: Single Responsibility Principle

Each method should do ONE thing and do it well.

Bad:

```java
public void processUserDataAndSendEmail(User user) {
    // Validates user
    // Saves to database
    // Sends email
    // Logs activity
}
```

Good: 

```java
public void processUser(User user) {
    validateUser(user);
    saveUser(user);
    sendConfirmationEmail(user);
    logActivity(user);
}
```

#### Practice 3: Fail-Fast with Parameter Validation

Validate inputs at the beginning of methods.

Good:

```java
public void processOrder(Order order) {
    if (order == null) {
        throw new IllegalArgumentException("Order cannot be null");
    }
    if (order.getItems().isEmpty()) {
        throw new IllegalArgumentException("Order must contain items");
    }
    // Process order
}
```

#### Practice 4: Prefer Small Methods
Guideline:
Methods should ideally be less than 20 lines. If longer, consider breaking into smaller methods.

Why?
- Easier to test
- Easier to understand
- Easier to reuse

#### Practice 5: Use Descriptive Parameter Names
Bad:

```java
public void calculate(int a, int b, int c) { }
```

Good: 

```java
public void calculateTotalPrice(int quantity, int unitPrice, int discount) { }
```

#### Practice 6: Avoid Deep Nesting in Methods

Bad:

```java
public void process(User user) {
    if (user != null) {
        if (user.isActive()) {
            if (user.hasPermission()) {
                // Deep nesting
            }
        }
    }
}
```

Good:

```java
public void process(User user) {
    if (user == null) return;
    if (!user.isActive()) return;
    if (!user.hasPermission()) return;
    // Process user
}
```

#### Practice 7: Document Complex Methods with Javadoc

```java
/**
 * Calculates the compound interest for a given principal amount.
 *
 * @param principal The initial amount (must be positive)
 * @param rate The annual interest rate (percentage, e.g., 5.5)
 * @param time The time period in years
 * @return The compound interest amount
 * @throws IllegalArgumentException if principal is negative
*/
public double calculateCompoundInterest(double principal, double rate, int time) {
if (principal < 0) {
throw new IllegalArgumentException("Principal must be positive");
}
return principal * Math.pow(1 + rate / 100, time) - principal;
}
```

#### Practice 8: Avoid Side Effects in Pure Functions

**Bad:**
```java
public int calculate(int x) {
    globalCounter++; // Side effect
    return x * 2;
}
```

**Good:**
```java
public int calculate(int x) {
    return x * 2; // Pure function
}
```

#### Practice 9: Use Method Overloading Wisely

Don't overload if behavior differs significantly.

**Good Use:**
```java
public void print(int x) { }
public void print(String s) { }
```

**Bad Use:**
```java
public void process(String filename) { /* Reads file */ }
public void process(String data) { /* Processes data */ }
// Confusing: same parameter type, different behavior
```

#### Practice 10: Recursion — Always Have Exit Condition

Never write recursive methods without a clear base case.

**Template:**
```java
public ReturnType recursiveMethod(Parameters) {
    // Base case (exit condition)
    if (baseCondition) {
        return baseValue;
    }
    // Recursive case (progress towards base case)
    return recursiveMethod(modifiedParameters);
}
```

#### Practice 11: Prefer Iteration Over Recursion for Performance-Critical Code

In production systems where performance matters, iteration is often better.

**Recursion:**
```java
public int factorial(int n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}
```

**Iteration (Better for Production):**
```java
public int factorial(int n) {
    int result = 1;
    for (int i = 2; i <= n; i++) {
        result *= i;
    }
    return result;
}
```

#### Practice 12: Handle Exceptions Appropriately

Don't silently swallow exceptions in methods.

**Bad:**
```java
public void readFile(String filename) {
    try {
        // File reading code
    } catch (IOException e) {
        // Silent failure
    }
}
```

**Good:**
```java
public void readFile(String filename) throws IOException {
    try {
        // File reading code
    } catch (IOException e) {
        // Log the error
        logger.error("Failed to read file: " + filename, e);
        throw e; // Propagate or wrap in custom exception
    }
}
```

---
---

### 10 Interview-Oriented Key Points (Quick Revision)

1. **Java is strictly pass-by-value.** References are passed by value, not objects themselves.

2. **Method signature** = method name + parameter list (return type NOT included).

3. **Method overloading** is resolved at **compile-time** based on parameter list.

4. **Recursion** requires a base case to prevent StackOverflowError.

5. **Stack memory** stores local variables and method frames; **heap memory** stores objects.

6. **main() method** must be `public static void main(String[])` for JVM to recognize it as entry point.

7. **Varargs** can only be the last parameter: `method(int x, String... args)`.

8. **Static methods** belong to the class; **instance methods** belong to objects.

9. **Return type** must match on all code paths or compile error occurs.

10. **Method inlining** by JIT compiler optimizes small, frequently called methods.

11. **Tail recursion** is NOT optimized in Java (unlike functional languages).

12. **Command-line arguments** are accessible via `args[]` in main method.

13. **Arrays passed to methods** can be modified because arrays are objects in heap.

14. **Recursion overhead** includes stack frame creation/destruction for each call.

15. **Final methods** cannot be overridden; **abstract methods** must be overridden.

---
---

### 11. One-Line Exam / Interview Answer

**Q: What is a method in Java?**

**A:** A method is a reusable block of code with a name, optional parameters, and a return type, that encapsulates specific functionality and executes within a stack frame when invoked.

### Conclusion
Methods are not just syntax — they represent how Java models real-world behavior. Understanding them deeply separates novice programmers from professional software engineers.

---
---

