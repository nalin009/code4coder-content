## 6. Memory & Performance Impact

---

#### 6.1. Stack vs Heap
##### Local variables (declared in methods/blocks):
- Stored on the stack
- Fast allocation and deallocation
- Automatically cleaned when block/method exits
- No garbage collection needed

##### Objects (created with new):
- Stored on the heap
- Managed by garbage collector
- References to objects are stored on stack

**Example:**

```java
public void example() {
    int x = 10; // Stack
    String s = "Hello"; // Reference on stack, "Hello" in String Pool (Heap)
    Integer obj = new Integer(20); // Reference on stack, object on Heap
} // x and s reference are destroyed, obj reference is destroyed
  // Object on heap will be GC'd later
```

---

#### 6.2. Performance Considerations
1. **Print statements are slow**: I/O operations are expensive
2. **Scope management has zero overhead**: JVM handles it natively
3. **Comments have zero runtime cost**: Stripped during compilation
4. **Excessive nesting impacts readability**: Not performance