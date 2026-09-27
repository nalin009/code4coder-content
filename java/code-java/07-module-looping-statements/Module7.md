## Control Statements - Looping

---
---

### Summary 
Looping statements are essential for efficient, scalable programming, enabling programs to process data, implement algorithms, and automate repetitive tasks without code duplication. Java provides multiple loop constructs optimized for different scenarios: for loops for counted iterations, while loops for condition-based repetition, do-while loops for guaranteed first execution, and enhanced for loops for clean collection iteration.

#### Key Takeaways:
- Choose for when iterations are known, while when unknown, do-while for at least one execution
- Use enhanced for loop for read-only collection iteration (cleaner, safer)
- Leverage break, continue, and return to control loop flow
- Use labeled statements to control nested loop execution
- Avoid deep nesting; extract complex logic into methods
- Be aware of performance: cache sizes, avoid object creation in tight loops
- Understand JVM optimizations (unrolling, hoisting, fusion)
- Always check for infinite loops and off-by-one errors

---
---

### 1. Introduction
#### Why This Topic Exists
Computers excel at repetitive tasks. Imagine manually writing code to print numbers from 1 to 1000, or processing each element in a collection of 10,000 items. Without loops, you'd need to copy-paste the same code thousands of times. Loops solve this by executing a block of code repeatedly until a condition is met, making programs efficient, concise, and scalable.

##### Looping statements give programs the power to:
- Repeat tasks efficiently without code duplication
- Process collections (arrays, lists, maps)
- Implement algorithms (searching, sorting, pattern matching)
- Handle user input until valid data is received
- Build iterative logic (games, simulations, servers)

#### What Problem Java Is Solving
##### Java provides looping constructs to:
- Eliminate repetitive code through iteration
- Process data structures efficiently
- Implement algorithms that require repeated steps
- Build responsive applications (event loops, polling)
- Enable infinite operations (servers, real-time systems)

Without loops, programs would be rigid, limited, and require astronomical amounts of code for simple repetitive tasks.

#### Why Beginners Struggle With This Topic
1. Infinite loops caused by incorrect loop conditions or missing updates
2. Off-by-one errors (loop runs one time too many or too few)
3. Understanding loop control flow (when break vs continue vs return)
4. Nested loop complexity (tracking multiple loop variables)
5. Choosing the right loop (for vs while vs do-while)
6. Enhanced for loop limitations (can't modify collection, no index access)
7. Loop variable scope (variable doesn't exist outside loop)

#### Why Interviewers Ask This (Especially 3–5+ YOE)
- Algorithm fundamentals: Most algorithms require loops (search, sort, traverse)
- Problem-solving ability: Pattern printing, matrix operations, string manipulation
- Performance awareness: Loop efficiency impacts application performance
- Code quality: Writing clean, optimized loops demonstrates experience
- Debugging skills: Identifying infinite loops, off-by-one errors
- Collection processing: Iterating over data structures efficiently

#### Senior developers are expected to:
- Choose the optimal loop construct for each situation
- Write performance-efficient loops (avoiding unnecessary iterations)
- Handle edge cases (empty collections, null checks, boundary conditions)
- Understand loop optimizations (JIT compiler, loop unrolling)

---
---

### 2. Clear Definitions
#### Loop
A control structure that repeatedly executes a block of code until a specified condition becomes false.

#### Iteration
A single execution of the loop body; one pass through the repeated code.

#### Loop Control Variable
A variable used to control the number of iterations, typically incremented or decremented each time through the loop.

#### Entry-Controlled Loop
A loop that checks its condition before executing the loop body (for, while).

#### Exit-Controlled Loop
A loop that checks its condition after executing the loop body, guaranteeing at least one execution (do-while).

#### Interview-Safe Definition:
"Looping statements in Java enable repeated execution of code blocks based on conditions. They include entry-controlled loops (for, while) that check conditions before execution, exit-controlled loops (do-while) that check after, and loop control statements (break, continue, return) that alter normal flow. Java also provides enhanced for loops for simplified collection iteration."

---
---

### 3. Core Concept Explanation
#### How Loops Work at the Language Level
Like decision-making statements, loops are compiled into bytecode instructions that the JVM executes using conditional jumps and labels.

##### Compiler's Role:
- Converts high-level loop constructs into labels and goto instructions
- Optimizes loop conditions and increments
- Identifies and may warn about unreachable code or infinite loops
- Performs constant folding and dead code elimination

##### JVM's Role:
- Executes loop bytecode using program counter (PC register) and conditional jumps
- Maintains loop variables on the stack
- Uses branch prediction for frequently executed loops
- JIT compiler applies advanced optimizations (loop unrolling, hoisting, vectorization)

#### WHY Java Designed Loops This Way
- Familiarity: Syntax borrowed from C/C++ for industry standardization
- Flexibility: Multiple loop types for different use cases
- Performance: Allows aggressive JVM optimizations
- Readability: Clear syntax with initialization, condition, and update in one place (for loop)
- Safety: Enhanced for loop prevents index errors

#### 3.1. for Loop

##### Syntax:

```java
for (initialization; condition; update) {
    // loop body
}
```

##### Components:
1. Initialization: Executes once before the loop starts (e.g., int i = 0)
2. Condition: Checked before each iteration; loop continues if true
3. Update: Executes after each iteration (e.g., i++)
4. Loop Body: Code to execute repeatedly

##### Execution Flow:
1. Initialization runs once
2. Condition is evaluated
3. If true, loop body executes
4. Update statement runs
5. Go back to step 2
6. If false, exit loop

###### Example:

```java
for (int i = 0; i < 5; i++) {
    System.out.println("Iteration: " + i);
}
```

###### Output:

```java
Iteration: 0
Iteration: 1
Iteration: 2
Iteration: 3
Iteration: 4
```

##### Bytecode Behavior:
###### Java Code:

```java
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}
```

**Bytecode (Simplified):**

```java
0: iconst_0           // Push 0 onto stack (initialization)
   1: istore_1           // Store in local variable i
   2: iload_1            // Load i
   3: iconst_5           // Push 5 onto stack
   4: if_icmpge 15       // If i >= 5, jump to 15 (exit loop)
   7: getstatic System.out
  10: iload_1            // Load i
  11: invokevirtual println
  14: iinc 1, 1          // Increment i by 1
  17: goto 2             // Jump back to condition check
  20: // exit
```

**Key Points:**
- Initialization is outside the loop
- Condition check uses if_icmpge (if i >= 5, exit)
- goto instruction creates the loop by jumping back
- Update (i++) happens after the loop body

##### When to Use for Loop
###### Use when:
- Number of iterations is known in advance
- Iterating over a range (0 to n, n to 0)
- Accessing array elements by index
- Counting loops (multiplication tables, patterns)

**Example: Array Iteration**

```java
int[] numbers = {10, 20, 30, 40, 50};
for (int i = 0; i < numbers.length; i++) {
    System.out.println("Element at index " + i + ": " + numbers[i]);
}
```

**Example: Reverse Iteration**

```java
for (int i = 10; i > 0; i--) {
    System.out.println(i);
}
System.out.println("Blast off!");
```

##### Variations of for Loop
###### 1. Multiple Initializations and Updates:

```java
for (int i = 0, j = 10; i < j; i++, j--) {
    System.out.println("i = " + i + ", j = " + j);
}
```

###### 2. Empty Components:

```java
int i = 0;
for (; i < 5; ) {  // Initialization and update outside
    System.out.println(i);
    i++;
}
```

###### 3. Infinite For Loop:

```java
for (;;) {  // No initialization, condition, or update
    System.out.println("Infinite loop");
    // Must have break or return to exit
}
```

##### Common Mistakes with for Loop
###### 1. Off-by-One Error:

```java
// Wrong: Runs 6 times (i = 0, 1, 2, 3, 4, 5)
for (int i = 0; i <= 5; i++) { }

// Correct: Runs 5 times (i = 0, 1, 2, 3, 4)
for (int i = 0; i < 5; i++) { }
```

###### 2. Modifying Loop Variable Inside Loop:

```java
// Unpredictable behavior
for (int i = 0; i < 10; i++) {
    if (i == 5) {
        i = 8;  // Skips iterations
    }
    System.out.println(i);
}
```

###### 3. Semicolon After for:


```java
for (int i = 0; i < 5; i++);  // Empty loop due to semicolon
    System.out.println(i);  // Error: i out of scope
```

###### 4. Floating-Point Loop Variable:


```java
// Risky due to floating-point precision
for (double d = 0.0; d < 1.0; d += 0.1) {
    System.out.println(d);  // May not reach 1.0 exactly
}
```

#### 3.2. Enhanced for Loop (for-each)
##### Syntax:

```java
for (Type variable : collection) {
    // loop body
}
```

##### How It Works:
- Iterates over all elements in an array or Iterable collection
- No manual index management
- Internal implementation uses iterator (for collections) or index (for arrays)
- Read-only access to elements

###### Example with Array:

```java
int[] numbers = {10, 20, 30, 40, 50};
for (int num : numbers) {
    System.out.println(num);
}

```

**Output:**

```java
10
20
30
40
50
```

###### Example with Collection:

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
for (String name : names) {
    System.out.println(name);
}
```

##### When to Use Enhanced for Loop
###### Use when:
- You need to iterate over all elements
- Index is not needed
- No modification of the collection during iteration
- Simple, readable iteration is preferred

###### Advantages:
- Cleaner, more readable syntax
- No off-by-one errors
- No index management
- Works with any Iterable (List, Set, Queue, etc.)

###### Limitations:
- Cannot access current index
- Cannot modify the collection during iteration
- Cannot iterate in reverse
- Cannot skip elements easily
- Cannot iterate over multiple collections simultaneously

##### Enhanced for Loop: What Happens Behind the Scenes
###### For Arrays:

```java
// Your code
int[] arr = {1, 2, 3};
for (int num : arr) {
    System.out.println(num);
}

// Compiler generates (approximately)
int[] arr = {1, 2, 3};
for (int i = 0; i < arr.length; i++) {
    int num = arr[i];
    System.out.println(num);
}
```

###### For Collections:

```java
// Your code
List<String> list = Arrays.asList("A", "B", "C");
for (String s : list) {
    System.out.println(s);
}

// Compiler generates (approximately)
List<String> list = Arrays.asList("A", "B", "C");
Iterator<String> iterator = list.iterator();
while (iterator.hasNext()) {
    String s = iterator.next();
    System.out.println(s);
}
```

##### Important Limitation: Cannot Modify Array Elements

```java
int[] numbers = {1, 2, 3, 4, 5};
for (int num : numbers) {
    num = num * 2;  // Does NOT modify the array
}
System.out.println(Arrays.toString(numbers));  // [1, 2, 3, 4, 5]
```

Why? The loop variable is a copy of the array element, not a reference to it.

###### Correct Way:

```java
int[] numbers = {1, 2, 3, 4, 5};
for (int i = 0; i < numbers.length; i++) {
    numbers[i] = numbers[i] * 2;  // Modifies the array
}
System.out.println(Arrays.toString(numbers));  // [2, 4, 6, 8, 10]
```

##### ConcurrentModificationException
###### Problem:

```java
List<Integer> numbers = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5));
for (int num : numbers) {
    if (num % 2 == 0) {
        numbers.remove(Integer.valueOf(num));  // ConcurrentModificationException
    }
} 
```

Why? The iterator used by enhanced for loop detects that the collection was modified during iteration (fail-fast mechanism).

**Solution 1: Use Iterator Explicitly**

```java
List<Integer> numbers = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5));
Iterator<Integer> iterator = numbers.iterator();
while (iterator.hasNext()) {
    int num = iterator.next();
    if (num % 2 == 0) {
        iterator.remove();  // Safe removal using iterator
    }
}
```

**Solution 2: Use removeIf (Java 8+)**


```java
List<Integer> numbers = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5));
numbers.removeIf(num -> num % 2 == 0);
```

#### 3.3. while Loop
##### Syntax:

```java
while (condition) {
    // loop body
}
```

##### How It Works:
- Checks condition before executing the loop body (entry-controlled)
- If condition is false initially, loop body never executes
- Continues until condition becomes false

##### Execution Flow:
- Evaluate condition
- If true, execute loop body
- Go back to step 1
- If false, exit loop

###### Example:

```java
int i = 0;
while (i < 5) {
    System.out.println("i = " + i);
    i++;
}
```

**Output:**

```java
i = 0
i = 1
i = 2
i = 3
i = 4
```

##### When to Use while Loop
###### Use when:
- Number of iterations is unknown
- Loop depends on a condition that may change unpredictably
- Reading input until a sentinel value
- Polling or waiting for an event
- Processing data until end-of-file

**Example: Reading Input Until Sentinel**

```java
Scanner scanner = new Scanner(System.in);
int sum = 0;
System.out.println("Enter numbers (0 to stop):");
int num = scanner.nextInt();
while (num != 0) {
    sum += num;
    num = scanner.nextInt();
}
System.out.println("Sum: " + sum);
```

**Example: Countdown**

```java
int count = 10;
while (count > 0) {
    System.out.println(count);
    count--;
}
System.out.println("Liftoff!");
```

##### Infinite while Loop
###### Syntax:

```java
while (true) {
    // Infinite loop
    // Must have break or return to exit
}
```

**Use Case: Server Applications**

```java
while (true) {
    Request request = server.accept();
    if (request == null) break;
    processRequest(request);
}
```

**Use Case: Event Loop**

```java
while (true) {
    Event event = getNextEvent();
    if (event.getType() == Event.EXIT) {
        break;
    }
    handleEvent(event);
}
```

##### Common Mistakes with while Loop
###### 1. Forgetting to Update Loop Variable:

```java
int i = 0;
while (i < 5) {
    System.out.println(i);
    // Forgot i++  → Infinite loop
}
```

###### 2. Condition Never Becomes False:

```java
int x = 10;
while (x > 0) {
    System.out.println(x);
    x++;  // x keeps increasing, never reaches 0
}
```

###### 3. Using Assignment Instead of Comparison:

```java
int i = 0;
while (i = 5) {  // Compilation error: incompatible types
    System.out.println(i);
}
```

#### 3.4. do-while Loop
##### Syntax:

```java
do {
    // loop body
} while (condition);
```

##### How It Works:
- Executes loop body first, then checks condition (exit-controlled)
- Guarantees at least one execution of the loop body
- Continues until condition becomes false

##### Execution Flow:
- Execute loop body
- Evaluate condition
- If true, go back to step 1
- If false, exit loop

###### Example:
```java
int i = 0;
do {
    System.out.println("i = " + i);
    i++;
} while (i < 5);
```

**Output:**

```java
i = 0
i = 1
i = 2
i = 3
i = 4
```

##### Key Difference: while vs do-while
Example Where Condition is Initially False:

###### Using while:

```java
int i = 10;
while (i < 5) {
    System.out.println(i);  // Never executes
}
System.out.println("After while");
```

**Output:**

```java
After while
```

###### Using do-while:

```java
int i = 10;
do {
    System.out.println(i);  // Executes once
} while (i < 5);
System.out.println("After do-while");
```

**Output:**

```java
10
After do-while
```

##### When to Use do-while Loop
###### Use when:
- Loop body must execute at least once
- Validating user input (show prompt at least once)
- Menu-driven programs
- Game loops (execute one frame, then check if game should continue)

**Example: Menu System**

```java
Scanner scanner = new Scanner(System.in);
int choice;
do {
    System.out.println("
=== MENU ===");
    System.out.println("1. Option 1");
    System.out.println("2. Option 2");
    System.out.println("3. Option 3");
    System.out.println("0. Exit");
    System.out.print("Enter choice: ");
    choice = scanner.nextInt();
    
    switch (choice) {
        case 1 -> System.out.println("Option 1 selected");
        case 2 -> System.out.println("Option 2 selected");
        case 3 -> System.out.println("Option 3 selected");
        case 0 -> System.out.println("Exiting...");
        default -> System.out.println("Invalid choice");
    }
} while (choice != 0);
```

**Example: Input Validation**

```java
Scanner scanner = new Scanner(System.in);
int age;
do {
    System.out.print("Enter your age (1-120): ");
    age = scanner.nextInt();
    if (age < 1 || age > 120) {
        System.out.println("Invalid age. Please try again.");
    }
} while (age < 1 || age > 120);
System.out.println("Age entered: " + age);
```

#### 3.5. Nested Loops
##### What Are Nested Loops?
A loop inside another loop. The inner loop completes all its iterations for each iteration of the outer loop.

##### Syntax:

```java
for (initialization; condition; update) {
    for (initialization; condition; update) {
        // Inner loop body
    }
}
```

###### Example:

```java
for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= 3; j++) {
        System.out.println("i = " + i + ", j = " + j);
    }
}
```

**Output:**

```java
i = 1, j = 1
i = 1, j = 2
i = 1, j = 3
i = 2, j = 1
i = 2, j = 2
i = 2, j = 3
i = 3, j = 1
i = 3, j = 2
i = 3, j = 3
```

##### How It Works:
- For each iteration of outer loop (i = 1, 2, 3), inner loop runs completely (j = 1, 2, 3)
- Total iterations = outer iterations × inner iterations (3 × 3 = 9)

##### Time Complexity of Nested Loops

|**Structure**|**Time Complexity**|**Example**|
| Single loop (n iterations) | O(n) | **`for (int i = 0; i < n; i++)`** |
| Two nested loops (n × m) | O(n × m) | **`for (int i = 0; i < n; i++) for (int j = 0; j < m; j++)`** |
| Two nested loops (n × n) | O(n²) | **`for (int i = 0; i < n; i++) for (int j = 0; j < n; j++)`** |
| Three nested loops | O(n³) | **`for (i) for (j) for (k)`** |

##### Performance Impact:

```java
// n = 1000
for (int i = 0; i < n; i++) { }  // 1,000 iterations

for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) { }  // 1,000,000 iterations
}

for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        for (int k = 0; k < n; k++) { }  // 1,000,000,000 iterations
    }
}
```

##### Pattern Printing Examples
###### Pattern 1: Right Triangle

```java
for (int i = 1; i <= 5; i++) {
    for (int j = 1; j <= i; j++) {
        System.out.print("* ");
    }
    System.out.println();
}
```

**Output:**

```java
* 
* * 
* * * 
* * * * 
* * * * *
```

###### Pattern 2: Inverted Right Triangle

```java
for (int i = 5; i >= 1; i--) {
    for (int j = 1; j <= i; j++) {
        System.out.print("* ");
    }
    System.out.println();
}
```
**Output:**

```java
* * * * * 
* * * * 
* * * 
* * 
*
```

###### Pattern 3: Pyramid

```java
int n = 5;
for (int i = 1; i <= n; i++) {
    // Print spaces
    for (int j = 1; j <= n - i; j++) {
        System.out.print("  ");
    }
    // Print stars
    for (int k = 1; k <= 2 * i - 1; k++) {
        System.out.print("* ");
    }
    System.out.println();
}
```

**Output:**

```java
       * 
      * * * 
    * * * * * 
  * * * * * * * 
* * * * * * * * *
```

###### Pattern 4: Number Pyramid

```java
for (int i = 1; i <= 5; i++) {
    for (int j = 1; j <= i; j++) {
        System.out.print(j + " ");
    }
    System.out.println();
}
```

**Output:**


```java
1 
1 2 
1 2 3 
1 2 3 4 
1 2 3 4 5
```

##### Real-World Use Cases for Nested Loops
###### 1. Matrix Operations:

```java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

for (int i = 0; i < matrix.length; i++) {
    for (int j = 0; j < matrix[i].length; j++) {
        System.out.print(matrix[i][j] + " ");
    }
    System.out.println();
}
```

###### 2. Finding Pairs:

```java
int[] numbers = {1, 2, 3, 4, 5};
int target = 7;

for (int i = 0; i < numbers.length; i++) {
    for (int j = i + 1; j < numbers.length; j++) {
        if (numbers[i] + numbers[j] == target) {
            System.out.println("Pair found: " + numbers[i] + ", " + numbers[j]);
        }
    }
}
```

###### 3. Bubble Sort:

```java
int[] arr = {64, 34, 25, 12, 22, 11, 90};
for (int i = 0; i < arr.length - 1; i++) {
    for (int j = 0; j < arr.length - i - 1; j++) {
        if (arr[j] > arr[j + 1]) {
            // Swap
            int temp = arr[j];
            arr[j] = arr[j + 1];
            arr[j + 1] = temp;
        }
    }
}
```

#### 3.6. Infinite Loops
##### What is an Infinite Loop?
A loop that never terminates because its condition never becomes false.

##### Intentional Infinite Loops:
###### 1. Server Applications:

```java
while (true) {
    Connection conn = server.acceptConnection();
    handleConnection(conn);
}
```

###### 2. Game Loop:

```java
while (true) {
    processInput();
    update();
    render();
    if (exitRequested) break;
}
```

###### 3. Event Dispatch Thread:

```java
while (true) {
    Event event = eventQueue.getNext();
    if (event == null) break;
    dispatchEvent(event);
}
```

##### Unintentional Infinite Loops (Bugs)
###### 1. Forgot to Update Loop Variable:

```java
int i = 0;
while (i < 10) {
    System.out.println(i);
    // Missing: i++;
}
```

###### 2. Wrong Update Direction:

```java
for (int i = 0; i < 10; i--) {  // i decreases instead of increases
    System.out.println(i);
}
```

###### 3. Condition Always True:

```java
int x = 5;
while (x > 0) {
    System.out.println(x);
    x++;  // x keeps increasing, always > 0
}
```

###### 4. Floating-Point Precision:

```java
for (double d = 0.0; d != 1.0; d += 0.1) {
    System.out.println(d);
    // May never reach exactly 1.0 due to floating-point precision
}
```

##### How to Break Out of Infinite Loops
###### 1. Using break:

```java
while (true) {
    String input = scanner.nextLine();
    if (input.equals("exit")) {
        break;
    }
    processInput(input);
}
```

###### 2. Using return:

```java
void processRequests() {
    while (true) {
        Request request = getNextRequest();
        if (request == null) {
            return;  // Exit method and loop
        }
        handleRequest(request);
    }
}
```

###### 3. Using a Flag:

```java
boolean running = true;
while (running) {
    processTask();
    if (shutdownRequested()) {
        running = false;
    }
}
```

#### 3.7. Loop Control Statements
Java provides three statements to alter loop execution: break, continue, and return.

##### 3.7.1. break Statement
**Purpose:** Immediately exits the innermost loop or switch statement.

###### Syntax:

```java
break;
```
**Example:**

```java
for (int i = 0; i < 10; i++) {
    if (i == 5) {
        break;  // Exit loop when i is 5
    }
    System.out.println(i);
}
System.out.println("After loop");
```

**Output:**

```java
0
1
2
3
4
After loop
```

###### Use Cases:
- Searching for an element (stop when found)
- Error detection (exit loop on error)
- Early termination based on condition

**Example: Search in Array**

```java
int[] numbers = {10, 20, 30, 40, 50};
int target = 30;
boolean found = false;

for (int num : numbers) {
    if (num == target) {
        found = true;
        break;  // Stop searching once found
    }
}

if (found) {
    System.out.println("Found " + target);
} else {
    System.out.println(target + " not found");
}
```

###### Labeled `break` (Breaking Out of Nested Loops)

**Syntax:**

```java
labelName: for (...) {
    for (...) {
        if (condition) {
            break labelName;  // Exits both loops
        }
    }
}
```

**Example:**

```java
outer: for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (i == 1 && j == 1) {
            break outer;  // Exits both outer and inner loops
        }
        System.out.println("i = " + i + ", j = " + j);
    }
}
System.out.println("After loops");
```

**Output:**

```java
i = 0, j = 0
i = 0, j = 1
i = 0, j = 2
i = 1, j = 0
After loops
```

**Without Label:**

```java
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (i == 1 && j == 1) {
            break;  // Only exits inner loop
        }
        System.out.println("i = " + i + ", j = " + j);
    }
}
```

**Output:**

```java
i = 0, j = 0
i = 0, j = 1
i = 0, j = 2
i = 1, j = 0
i = 2, j = 0
i = 2, j = 1
i = 2, j = 2
```

##### 3.7.2. continue Statement
**Purpose:** Skips the remaining code in the current iteration and moves to the next iteration of the loop.

###### Syntax:

```java
continue;
```

**Example:**

```java
for (int i = 0; i < 10; i++) {
    if (i % 2 == 0) {
        continue;  // Skip even numbers
    }
    System.out.println(i);
}
```

**Output:**

```java
1
3
5
7
9
```

###### How It Works:
- When continue is encountered, the rest of the loop body is skipped
- For for loops, the update statement still executes
- Control returns to the condition check

###### Use Cases:
- Skipping invalid data
- Processing only specific elements
- Avoiding deep nesting

**Example: Processing Valid Items**

```java
String[] items = {"apple", null, "banana", "", "cherry", null};

for (String item : items) {
    if (item == null || item.isEmpty()) {
        continue;  // Skip invalid items
    }
    System.out.println("Processing: " + item);
}
```

**Output:**

```java
Processing: apple
Processing: banana
Processing: cherry
```

###### Labeled continue

**Syntax:**

```java
labelName: for (...) {
    for (...) {
        if (condition) {
            continue labelName;  // Continues outer loop
        }
    }
}
```

**Example:**

```java
outer: for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (j == 1) {
            continue outer;  // Skip to next iteration of outer loop
        }
        System.out.println("i = " + i + ", j = " + j);
    }
}
```

**Output:**

```java
i = 0, j = 0
i = 1, j = 0
i = 2, j = 0
```

##### 3.7.3. return Statement in Loops
**Purpose:** Exits the entire method immediately, not just the loop.

**Syntax:**

```java
return;  // For void methods
return value;  // For methods with return type
```

**Example:**

```java
public int findIndex(int[] arr, int target) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == target) {
            return i;  // Exit method immediately, returning index
        }
    }
    return -1;  // Not found
}
```

###### Difference from break:
- break exits the loop but continues method execution
- return exits the method entirely

**Example Comparison:**

```java
void methodWithBreak() {
    for (int i = 0; i < 10; i++) {
        if (i == 5) break;
        System.out.println(i);
    }
    System.out.println("After loop");  // This executes
}

void methodWithReturn() {
    for (int i = 0; i < 10; i++) {
        if (i == 5) return;
        System.out.println(i);
    }
    System.out.println("After loop");  // This does NOT execute
}
```

###### Summary: break vs continue vs return

|**Statement**|**Scope**|**Effect**|**Common Use**|
|-------------|---------|----------|--------------|
| break | Loop/switch | Exits the innermost loop or switch | Search, early termination |
| continue | Loop | Skips to next iteration | Skip invalid data, filtering |
| return | Method | Exits the entire method | Return result, error handling |
| Labeled break | Multiple loops | Exits specified loop | Nested loop early exit |
| Labeled continue | Multiple loops |Continues specified loop  | Complex nested flow control |

#### 3.8. Loop Examples & Real-World Applications
##### Example 1: Factorial Calculation

```java
int n = 5;
long factorial = 1;
for (int i = 1; i <= n; i++) {
    factorial *= i;
}
System.out.println(n + "! = " + factorial);  // 5! = 120
```
##### Example 2: Fibonacci Series

```java
int n = 10;
int a = 0, b = 1;
System.out.print("Fibonacci series: " + a + " " + b);
for (int i = 2; i < n; i++) {
    int next = a + b;
    System.out.print(" " + next);
    a = b;
    b = next;
}
```

**Output:**

```java
Fibonacci series: 0 1 1 2 3 5 8 13 21 34
```

##### Example 3: Prime Number Check

```java
int num = 29;
boolean isPrime = true;

if (num <= 1) {
    isPrime = false;
} else {
    for (int i = 2; i <= Math.sqrt(num); i++) {
        if (num % i == 0) {
            isPrime = false;
            break;  // No need to check further
        }
    }
}

System.out.println(num + " is " + (isPrime ? "prime" : "not prime"));
```

##### Example 4: Reverse a Number

```java
int num = 12345;
int reversed = 0;

while (num != 0) {
    int digit = num % 10;
    reversed = reversed * 10 + digit;
    num /= 10;
}

System.out.println("Reversed: " + reversed);  // 54321
```

##### Example 5: Sum of Digits

```java
int num = 12345;
int sum = 0;

while (num > 0) {
    sum += num % 10;
    num /= 10;
}

System.out.println("Sum of digits: " + sum);  // 15
```

##### Example 6: Multiplication Table

```java
int num = 7;
for (int i = 1; i <= 10; i++) {
    System.out.println(num + " x " + i + " = " + (num * i));
}
```
 
##### Example 7: Diamond Pattern

```java
int n = 5;
// Upper half
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n - i; j++) System.out.print(" ");
    for (int k = 1; k <= 2 * i - 1; k++) System.out.print("*");
    System.out.println();
}
// Lower half
for (int i = n - 1; i >= 1; i--) {
    for (int j = 1; j <= n - i; j++) System.out.print(" ");
    for (int k = 1; k <= 2 * i - 1; k++) System.out.print("*");
    System.out.println();
}
```

---
---

### 4. Variations / Types / Categories
#### Entry-Controlled Loops:
1. for loop - Known iterations, compact syntax
2. Enhanced for loop - Collection iteration, read-only
3. while loop - Unknown iterations, pre-check condition

#### Exit-Controlled Loop:
1. do-while loop - At least one execution, post-check condition

#### Loop Control Statements:
1. break - Exit loop immediately
2. continue - Skip to next iteration
3. return - Exit method

#### Special Categories:
1. Nested loops - Loop within a loop
2. Infinite loops - Never-ending execution (intentional or bug)
3. Labeled statements - Control nested loop flow

---
---

### 5. Memory & Performance Impact
#### Stack Memory
##### Loop Variables:

```java
for (int i = 0; i < 10; i++) {
    int temp = i * 2;  // Created and destroyed each iteration
}
// i and temp no longer exist
```

- Loop control variables (i, j, k) are stored on the stack
- Local variables inside loops are created and destroyed each iteration
- Nested loops create separate stack frames for each level
- No heap allocation unless objects are created

#### Performance Considerations
##### 1. Loop Unrolling (JIT Optimization):
The JIT compiler may unroll small loops to reduce branching overhead:

**Your Code:**

```java
for (int i = 0; i < 4; i++) {
    sum += arr[i];
}
```

**JIT May Optimize To:**

```java
sum += arr[0];
sum += arr[1];
sum += arr[2];
sum += arr[3];
```

###### Benefits:
- Fewer branch instructions
- Better CPU pipeline utilization
- Increased instruction-level parallelism

##### 2. Loop Hoisting (Moving Invariant Code):
###### Your Code:

```java
for (int i = 0; i < arr.length; i++) {
    int limit = calculateLimit();  // Same result every iteration
    if (arr[i] < limit) {
        process(arr[i]);
    }
}
```

###### JIT Optimizes To:

```java
int limit = calculateLimit();  // Moved outside loop
for (int i = 0; i < arr.length; i++) {
    if (arr[i] < limit) {
        process(arr[i]);
    }
}
```

##### 3. Enhanced For Loop Performance:
###### Array Iteration:

```java
// Nearly identical performance
for (int i = 0; i < arr.length; i++) { }  // Traditional
for (int num : arr) { }  // Enhanced
```

###### Collection Iteration:

```java
// Enhanced for is often faster for collections
for (int num : list) { }  // Uses iterator
```

Why? Direct iterator usage can be more efficient than indexed access for linked structures.

##### 4. Avoiding Object Creation in Loops:
###### Bad (Creates 1000 objects):

```java
for (int i = 0; i < 1000; i++) {
    String s = new String("Hello");  // New object each iteration
    System.out.println(s);
}
```

###### Good (Reuses string literal):

```java
String s = "Hello";  // String pool
for (int i = 0; i < 1000; i++) {
    System.out.println(s);
}
```

##### 5. Loop Fusion (Combining Loops):
###### Before:

```java
for (int i = 0; i < n; i++) {
    a[i] = b[i] + 1;
}
for (int i = 0; i < n; i++) {
    c[i] = a[i] * 2;
}
```

###### After:

```java
for (int i = 0; i < n; i++) {
    a[i] = b[i] + 1;
    c[i] = a[i] * 2;
}
```

Benefits: Better cache locality, fewer loop overhead instructions.

##### 6. Avoiding Method Calls in Loop Conditions:
###### Bad:

```java
for (int i = 0; i < list.size(); i++) {  // Calls size() each iteration
    process(list.get(i));
}
```

###### Good:

```java
int size = list.size();  // Call once
for (int i = 0; i < size; i++) {
    process(list.get(i));
}
```

###### Or better (for collections):

```java
for (String item : list) {  // Iterator-based, efficient
    process(item);
}
```

---
---

### 6. Real-World Use Cases
#### Beginner Level:
##### 1. Multiplication Table:

```java
for (int i = 1; i <= 10; i++) {
    System.out.println("5 x " + i + " = " + (5 * i));
}
```

##### 2. Sum of Array:

```java
int[] numbers = {10, 20, 30, 40, 50};
int sum = 0;
for (int num : numbers) {
    sum += num;
}
System.out.println("Sum: " + sum);
```

##### 3. Count Even Numbers:

```java
int[] numbers = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
int count = 0;
for (int num : numbers) {
    if (num % 2 == 0) count++;
}
System.out.println("Even numbers: " + count);
```

#### Interview Level:
##### 1. Palindrome Check:

```java
String str = "radar";
boolean isPalindrome = true;
for (int i = 0; i < str.length() / 2; i++) {
    if (str.charAt(i) != str.charAt(str.length() - 1 - i)) {
        isPalindrome = false;
        break;
    }
}
```

##### 2. Find Largest Element:

```java
int[] arr = {45, 23, 78, 12, 90, 34};
int max = arr[0];
for (int i = 1; i < arr.length; i++) {
    if (arr[i] > max) {
        max = arr[i];
    }
}
```

##### 3. Armstrong Number:
```java
int num = 153;
int original = num, sum = 0;
while (num > 0) {
    int digit = num % 10;
    sum += digit * digit * digit;
    num /= 10;
}
boolean isArmstrong = (sum == original);
```

#### Production Level:
##### Batch Processing:

```java
List<Order> orders = getOrders();
for (Order order : orders) {
    try {
        processOrder(order);
    } catch (Exception e) {
        logger.error("Failed to process order: " + order.getId(), e);
        continue;  // Skip failed order, process rest
    }
}
```

##### Pagination:

```java
int pageSize = 100;
int offset = 0;
while (true) {
    List<Record> records = database.fetchRecords(offset, pageSize);
    if (records.isEmpty()) break;
    
    for (Record record : records) {
        process(record);
    }
    offset += pageSize;
}
```

##### Retry Logic:

```java
int maxRetries = 3;
int attempt = 0;
boolean success = false;

while (attempt < maxRetries && !success) {
    try {
        makeApiCall();
        success = true;
    } catch (NetworkException e) {
        attempt++;
        if (attempt >= maxRetries) {
            throw new RuntimeException("Max retries exceeded", e);
        }
        Thread.sleep(1000 * attempt);  // Exponential backoff
    }
}
```


---
---

### 7. Important Diagrams (Described in Words)
#### Diagram 1: For Loop Execution Flow

```java
Start → Initialization → Condition (True?) → Loop Body → Update → Condition (True?) → Loop Body → Update → Condition (False) → Exit
```

#### Diagram 2: While Loop Execution Flow

```java
Start → Condition (True?) → Loop Body → Condition (True?) → Loop Body → Condition (False) → Exit
```

#### Diagram 3: Do-While Loop Execution Flow

```java
Start → Loop Body → Condition (True?) → Loop Body → Condition (True?) → Loop Body → Condition (False) → Exit
```

#### Diagram 4: Nested Loop Execution

```java
Outer Loop (i=0) → Inner Loop (j=0, 1, 2) → Outer Loop (i=1) → Inner Loop (j=0, 1, 2) → Outer Loop (i=2) → Inner Loop (j=0, 1, 2) → End
```

#### Diagram 5: Break vs Continue

```java
Break: Loop → Condition → Body → break → EXIT LOOP → Continue Execution

Continue: Loop → Condition → Body → continue → SKIP Rest of Body → Next Iteration
```

---
---

### 8. Common Mistakes & Misconceptions
#### 1. Off-by-One Error

```java
// Wrong: Runs 11 times (i = 0 to 10)
for (int i = 0; i <= 10; i++) { }

// Correct: Runs 10 times (i = 0 to 9)
for (int i = 0; i < 10; i++) { }
```

#### 2. Modifying Collection During Enhanced For Loop

```java
List<Integer> list = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5));
for (int num : list) {
    if (num % 2 == 0) {
        list.remove(Integer.valueOf(num));  // ConcurrentModificationException
    }
}
```

#### 3. Infinite Loop Due to Floating-Point

```java
// May never terminate due to precision
for (double d = 0.0; d != 1.0; d += 0.1) {
    System.out.println(d);
}
```

#### 4. Forgetting Break in Switch Inside Loop

```java
for (int i = 0; i < 5; i++) {
    switch (i) {
        case 1:
            System.out.println("One");
            // Missing break - falls through
        case 2:
            System.out.println("Two");
            break;
    }
}
```

#### 5. Scope Confusion

```java
for (int i = 0; i < 10; i++) {
    // i is accessible here
}
// i is NOT accessible here - compilation error
System.out.println(i);
```

#### 6. Using Wrong Loop Type

```java
// BAD: Unknown iterations, but using for loop
for (int i = 0; ; i++) {
    String line = reader.readLine();
    if (line == null) break;
    process(line);
}

// BETTER: Use while for unknown iterations
String line;
while ((line = reader.readLine()) != null) {
    process(line);
}
```

#### 7. Not Checking Empty Collection

```java
int[] arr = {};
int max = arr[0];  // ArrayIndexOutOfBoundsException
for (int i = 1; i < arr.length; i++) {
    if (arr[i] > max) max = arr[i];
}
```

#### 8. Incrementing Wrong Variable in Nested Loop

```java
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        System.out.println(i + ", " + j);
        i++;  // BUG: Incrementing outer loop variable
    }
}
```

---
---

### 9. Best Practices (5+ YOE Expectation)
#### 1. Choose the Right Loop Type

```java
// Known iterations → for loop
for (int i = 0; i < 10; i++) { }

// Unknown iterations → while loop
while (!queue.isEmpty()) { }

// At least one execution → do-while
do { } while (condition);

// Collection iteration → enhanced for
for (String name : names) { }
```

#### 2. Cache Collection Size

```java
// AVOID
for (int i = 0; i < list.size(); i++) { }

// PREFER
int size = list.size();
for (int i = 0; i < size; i++) { }

// OR USE enhanced for
for (String item : list) { }
```

#### 3. Use Enhanced For Loop When Possible

```java
// Less code, cleaner, no index errors
for (String name : names) {
    process(name);
}
```

#### 4. Break Out of Nested Loops with Labels

```java
outer: for (int i = 0; i < 10; i++) {
    for (int j = 0; j < 10; j++) {
        if (found(i, j)) {
            break outer;
        }
    }
}
```

#### 5. Avoid Deep Nesting

```java
// BAD: Hard to read
for (...) {
    for (...) {
        for (...) {
            for (...) {
                // Code
            }
        }
    }
}

// BETTER: Extract to methods
for (...) {
    processRow(row);
}
```

#### 6. Use continue to Reduce Nesting

```java
// BEFORE
for (String item : items) {
    if (item != null) {
        if (!item.isEmpty()) {
            if (item.startsWith("A")) {
                process(item);
            }
        }
    }
}

// AFTER
for (String item : items) {
    if (item == null) continue;
    if (item.isEmpty()) continue;
    if (!item.startsWith("A")) continue;
    process(item);
}
```

#### 7. Document Intentional Infinite Loops

```java
while (true) {  // Intentional infinite loop - server accepts connections
    Connection conn = server.accept();
    if (conn == null) break;
    handleConnection(conn);
}
```

#### 8. Avoid Creating Objects in Tight Loops

```java
// BAD
for (int i = 0; i < 10000; i++) {
    StringBuilder sb = new StringBuilder();  // 10000 objects created
    sb.append("Hello");
}

// GOOD
StringBuilder sb = new StringBuilder();  // Reuse
for (int i = 0; i < 10000; i++) {
    sb.setLength(0);  // Reset
    sb.append("Hello");
}
```

#### 9. Use Descriptive Loop Variables

```java
// OK for simple loops
for (int i = 0; i < n; i++) { }

// BETTER for clarity
for (int rowIndex = 0; rowIndex < rows.length; rowIndex++) { }
for (User user : users) { }
```

#### 10. Consider Stream API for Collection Operations (Java 8+)

```java
// Traditional loop
List<String> filtered = new ArrayList<>();
for (String name : names) {
    if (name.startsWith("A")) {
        filtered.add(name.toUpperCase());
    }
}

// Functional approach
List<String> filtered = names.stream()
    .filter(name -> name.startsWith("A"))
    .map(String::toUpperCase)
    .collect(Collectors.toList());
```

---
---

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

### 12. Conclusion
This knowledge is foundational and unchanged through Java 25, forming the basis for algorithm implementation, data processing, and application logic across all Java development.

---
---
