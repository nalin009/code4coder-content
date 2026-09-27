## 14. Memory & Performance Impact

---

#### 14.1. Stack vs Heap

##### Stack:
- Stores local primitive variables and object references
- Fast allocation/deallocation (LIFO structure)
- Small size (typically 1-2 MB per thread)

##### Heap:
- Stores objects (including wrapper objects, arrays, instance variables)
- Slower allocation (requires garbage collection)
- Large size (configurable, often hundreds of MBs or GBs)

**Example:**

```java
public void example() {
    int x = 10;           // 'x' on stack
    Integer y = 20;       // 'y' (reference) on stack, object on heap
}
```

---

#### 14.2. Metaspace (Static Variables)
**Metaspace (Java 8+):** Stores class `metadata` and `static` variables.
- Replaced the older "PermGen" space
- Auto-resizes (no fixed size like PermGen)
- Can cause memory leaks if static collections grow unbounded

---

#### 14.3. Performance: Primitives vs Wrappers
**Benchmark (conceptual):**
- **Primitive int:** ~1 nanosecond per operation
- **Wrapper Integer:** ~10 nanoseconds (due to object creation, method calls)

**Rule of Thumb:** Use primitives for performance-critical code. Use wrappers only when necessary (collections, null values, APIs requiring objects).

---

#### 14.4. Garbage Collection Impact
Autoboxing creates millions of short-lived objects, triggering frequent minor GCs.

**Example:**

```java
// Bad: Creates 1 million Integer objects
for (int i = 0; i < 1_000_000; i++) {
    Integer x = i; // Autoboxing
}
```

**Mitigation:** Use primitives where possible, or use specialized primitive collections (e.g., Eclipse Collections, Trove).