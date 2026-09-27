## 8. var Keyword (Local Variable Type Inference)

---

**Introduced:** `Java 10`

**Definition:** The var keyword allows the compiler to infer the type of a local variable from its initializer.

**Example:**

```java
var count = 10;        // Inferred as int
var name = "Alice";    // Inferred as String
var list = new ArrayList<String>(); // Inferred as ArrayList<String>
```

---

#### 8.1. Restrictions:
**1.** Only for local variables (not instance or static variables)
**2.** Must initialize at declaration

```java
  var x; // Error: Cannot infer type
  var y = null; // Error: Cannot infer from null
```

**3.** Cannot use with lambda expressions without explicit target type (Before Java 11)

```java
  // var func = () -> {}; // Error
  var func = (Runnable) () -> {}; // OK
```

**4.** Since Java 11, you can use var in lambda parameters:

```java
// Java 11+
list.forEach((var item) -> System.out.println(item));
```

**But you cannot do:**

```java
var func = () -> {}; // Error: cannot infer type
```

**Recommendation**: Clarify this is about **variable declaration**, not lambda parameters.

**5.** Type Inference Limitations (var)
- Cannot use var in method signatures
- Cannot use var for array initialization without explicit type

```java
// var arr = {1, 2, 3}; // Error
var arr = new int[]{1, 2, 3}; // OK
```

**Benefits**:
- Reduces verbosity: `var map = new HashMap<String, List<Integer>>();`
- Improves readability when the type is obvious

**Drawbacks**:
- Can reduce clarity if overused
- Not allowed in method signatures or class fields

**Interview Insight**: `var` is **compile-time only**—the bytecode still has explicit types. It's syntactic sugar.

**Unchanged till Java 25**: The `var` keyword rules remain the same since Java 10.