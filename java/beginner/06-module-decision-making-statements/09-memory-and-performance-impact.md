## 9 Memory & Performance Impact

---

#### 9.1 Stack Memory:
- Boolean expressions are `evaluated` on the operand stack
- `Local` variables in if-else blocks are stored on the `stack` frame
- Each branch may have its own `stack frame` for local variables
- Variables declared inside if blocks are `destroyed` when the block exits

**Example:**

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
- && (AND): If `first` condition is false, `second` is not evaluated
- || (OR): If `first` condition is true, `second` is not evaluated
- Saves `computation` and `prevents` errors

###### 2. if-else vs switch Performance:

|**Number of Conditions**|**if-else**|**switch (traditional)**|**switch expression**|
|------------------------|-----------|------------------------|---------------------|
| **1-3 conditions** | Fast (similar) | Fast (similar) | Fast (similar) |
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

---

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