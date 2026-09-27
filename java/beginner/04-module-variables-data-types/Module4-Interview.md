## MODULE 4: Variables & Data Types

---
---

### Q1. What is the difference between instance variables and local variables?
**Answer**:  Instance variables are declared inside a class but outside methods, stored on the heap with the object, and automatically initialized to default values (0, null, false). Local variables are declared inside methods or blocks, stored on the stack, have no default value, and must be explicitly initialized before use. Instance variables have class-level scope, while local variables are limited to the block where they're declared.

---

### Q2. Why does Java have both primitives and wrapper classes?
**Answer**:  Primitives exist for performance and memory efficiency—they store values directly without object overhead. However, Java collections (like ArrayList, HashMap) and APIs requiring objects cannot use primitives. Wrapper classes provide object representations of primitives, enabling features like null values, utility methods (parseInt, toString), and compatibility with generics. The trade-off is performance: primitives are faster, but wrappers offer flexibility when objects are required.

---

### Q3. Explain autoboxing and unboxing with an example. What are the performance implications?
**Answer**:  Autoboxing is the automatic conversion from primitive to wrapper (e.g., `int` → `Integer`), while unboxing is the reverse. Example: `Integer x = 10;` (autoboxing) and `int y = x;` (unboxing). The compiler inserts `Integer.valueOf(10)` and `x.intValue()` respectively. Performance impact: autoboxing creates objects, causing heap allocation and garbage collection overhead. In tight loops processing millions of values, autoboxing can degrade performance significantly—prefer primitives in such cases.

---

### Q4. What happens when you compare two Integer objects using `==`? How should you compare them correctly?
**Answer**:  Using `==` with Integer objects compares references (memory addresses), not values. Due to Integer caching (-128 to 127), `Integer a = 100; Integer b = 100;` makes `a == b` true (same cached object), but `Integer c = 200; Integer d = 200;` makes `c == d` false (different objects). To compare values correctly, always use `.equals()` method, which compares the actual numeric values inside the Integer objects, regardless of caching.

---

### Q5. What is the difference between implicit and explicit type casting? Give examples of potential data loss.
**Answer**:  Implicit casting (widening) happens automatically when converting smaller to larger types (e.g., `int` → `long`) because no data loss occurs. Explicit casting (narrowing) requires manual syntax `(targetType)` when converting larger to smaller types, potentially losing data. Example of data loss: `double d = 3.99; int i = (int) d;` results in `i = 3` (fractional part lost). Overflow example: `int big = 130; byte small = (byte) big;` results in `-126` due to wrapping.

---

### Q6. Why are wrapper classes immutable? What are the benefits?
**Answer**:  Wrapper classes are immutable to ensure thread safety—multiple threads can safely share the same Integer object without synchronization. Immutability also enables efficient caching (Integer cache -128 to 127), prevents unintended modifications improving security, and makes wrapper objects suitable as HashMap keys (since their hashcode remains constant). However, modifying a wrapper in a loop creates new objects each iteration, causing garbage collection overhead.

---

### Q7. Explain the memory model for primitives vs reference types. Where are they stored?
**Answer**:  Primitive local variables are stored directly on the stack, which enables fast allocation and deallocation. Primitive instance variables are stored in the heap as part of the object. Reference type variables (local or instance) store memory addresses on the stack or heap, pointing to the actual object on the heap. Static variables (both primitive and reference) are stored in Metaspace (Java 8+). This separation means primitives avoid object overhead, but reference types require heap allocation and garbage collection.

---

### Q8. What is the purpose of the `final` keyword for variables? Are compile-time and runtime constants handled differently?
**Answer**:  The `final` keyword makes variables immutable—their value cannot change after initialization. It improves code readability, maintainability, and type safety. Compile-time constants (initialized with literals like `final int X = 10;`) are inlined by the compiler, meaning the value is directly embedded in bytecode for better performance. Runtime constants (initialized with method calls like `final int Y = calculate();`) are not inlined. If you change a compile-time constant in one class, dependent classes must be recompiled to see the new value.

---

### Q9. What are the risks of autoboxing a null value? How can you prevent NullPointerException?
**Answer**:  Unboxing a null wrapper throws NullPointerException because the compiler translates `int x = wrapperObj;` to `int x = wrapperObj.intValue();`, and calling a method on null causes NPE. This commonly occurs when retrieving database results or collection values that might be null. Prevention: always perform null-checks before unboxing (`if (wrapperObj != null) int x = wrapperObj;`) or use ternary operators to provide default values (`int x = (wrapperObj != null) ? wrapperObj : 0;`).

---

### Q10. Why does `long` to `float` implicit casting succeed despite potential precision loss?
**Answer**:  Java allows implicit casting from `long` (8 bytes) to `float` (4 bytes) because `float` has a wider range using scientific notation, even though it has fewer bytes. However, `float` maintains only ~7 significant digits, so large `long` values lose precision when converted. Example: `long big = 123456789012345L; float f = big;` results in rounding. The language prioritizes range over precision for implicit conversions, but developers must be aware of potential accuracy loss in such conversions.

---

### Q11. Explain the behavior of static variables in multi-threaded environments.
**Answer**:  Static variables are shared across all instances and threads, making them inherently not thread-safe. Multiple threads concurrently reading and writing a static variable can cause race conditions, lost updates, or inconsistent state. For thread safety, use synchronization (synchronized blocks/methods), volatile keyword (for visibility guarantees), or atomic classes like AtomicInteger. Additionally, static variables live for the JVM's lifetime and reside in Metaspace, so unbounded growth (e.g., static collections) can cause memory leaks.

---

### Q12. What is the `var` keyword, and when should you avoid using it?
**Answer**:  The `var` keyword (Java 10+) enables local variable type inference, letting the compiler deduce the type from the initializer (e.g., `var list = new ArrayList<String>();`). It reduces verbosity and improves readability when types are obvious. However, avoid `var` when: the initializer is unclear (e.g., `var x = getData();` where return type isn't obvious), in public APIs (reduces documentation clarity), or when explicit types improve code understanding. Remember, `var` is only for local variables—not fields, parameters, or return types.