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