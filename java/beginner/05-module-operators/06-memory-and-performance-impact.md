## 6. Memory & Performance Impact

---

#### 6.1. Stack Operations
Most operator computations occur on the JVM operand stack.

**Example:**

```java
int result = (a + b) * c;
```

**Bytecode** (simplified):

```java
iload_1      // Load 'a' onto stack
iload_2      // Load 'b' onto stack
iadd         // Pop two values, add, push result
iload_3      // Load 'c' onto stack
imul         // Pop two values, multiply, push result
istore_4     // Pop result, store in 'result'
```

No heap allocation occurs for primitive operator results — everything happens on the stack, making operations extremely fast.

---

#### 6.2. Autoboxing and Operators
Operators do not work directly on wrapper objects:

```java
Integer a = 100;
Integer b = 200;
Integer sum = a + b;  // Unboxed to int, added, then boxed back to Integer
```

**Performance Impact**:
1. **Unboxing**: Extract primitive value (method call overhead)
2. **Operation**: Perform primitive operation (fast)
3. **Autoboxing**: Create new wrapper object (heap allocation + GC pressure)

**Bytecode**:

```java
invokevirtual Integer.intValue()  // Unbox 'a'
invokevirtual Integer.intValue()  // Unbox 'b'
iadd                               // Add primitives
invokestatic Integer.valueOf()    // Box result
```

**Best Practice:** Use primitives for compute-heavy operations to avoid boxing overhead.

---

#### 6.3. String Concatenation
##### The `+` operator is special for strings:

```java
String result = "Hello" + " " + "World";
```

##### Java 8 and earlier: Compiled to `StringBuilder` operations:

```java
String result = new StringBuilder().append("Hello").append(" ").append("World").toString();
```

##### Java 9+: Uses invokedynamic with StringConcatFactory for optimized concatenation (unchanged till Java 25).
**Performance Consideration:** In loops, explicit StringBuilder is still faster:

```java
// Slow
String result = "";
for (int i = 0; i < 1000; i++) {
    result += i;  // Creates 1000 intermediate String objects
}

// Fast
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 1000; i++) {
    sb.append(i);  // Single StringBuilder instance
}
String result = sb.toString();
```

---

#### 6.4. GC Impact
- **Operators on primitives:** Zero GC impact (stack-only operations).
- Operators causing heap allocation:
  - String concatenation with +
  - Autoboxing from arithmetic on wrapper types
- **Production Insight:** In high-performance code (trading systems, game engines), avoid operators that trigger allocation in hot loops.