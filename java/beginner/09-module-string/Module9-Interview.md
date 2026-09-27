## MODULE 9: Strings

---
---

### Interview Question 1

**Q: Explain the difference between `String s = "Java"` and `String s = new String("Java")`. Which one is preferred and why?**

**A**: When you write `String s = "Java"`, the JVM checks the String Pool for the literal "Java". If found, `s` references that pooled object; if not, it creates one in the pool. This saves memory through reuse. In contrast, `String s = new String("Java")` explicitly creates a new object in the heap, bypassing the pool (though "Java" as a literal will still exist in the pool). This creates two objects—one in the pool and one in the heap—wasting memory. The first approach is always preferred in production code because it leverages Java's built-in memory optimization. Use `new String()` only when you explicitly need a separate heap object, which is extremely rare.

---

### Interview Question 2

**Q: What is the String Pool, and how did its location change from Java 6 to Java 7? What impact did this change have?**

**A**: The String Pool is a special memory area that stores string literals to enable memory reuse. In Java 6 and earlier, it was located in PermGen (Permanent Generation) space, which had a fixed size and was rarely garbage collected. This caused OutOfMemoryError when too many strings were interned. From Java 7 onwards, the String Pool was moved to the heap memory, making it eligible for normal garbage collection. This change improved memory management, reduced OutOfMemoryError risks, and made `intern()` safer to use in production. The pool remains in the heap through Java 25.

---

### Interview Question 3

**Q: Why are strings immutable in Java? Explain at least three reasons with real-world implications.**

**A**: Strings are immutable for several critical reasons. First, immutability enables the String Pool optimization—if strings were mutable, changing one reference would affect all references pointing to the same pooled object, making pooling impossible. Second, it provides thread safety without synchronization overhead, which is crucial in multi-threaded applications where strings are frequently shared. Third, it ensures security in sensitive operations like file paths, database URLs, or network connections, preventing malicious code from altering these values. Fourth, immutability allows hashcode caching, making strings ideal for HashMap keys since their hash value never changes. These design decisions make Java applications more efficient, safer, and easier to reason about.

---

### Interview Question 4

**Q: What is the `intern()` method? When should you use it, and when should you avoid it?**

**A**: The `intern()` method places a string into the String Pool if it doesn't exist, or returns a reference to the existing pooled string if it does. You should use `intern()` when dealing with many duplicate strings, such as parsing CSV files with repeated category names or processing log files with repeated error codes. This reduces memory footprint significantly. However, avoid `intern()` for unique or rarely repeated strings (like UUIDs or random tokens) because it unnecessarily occupies pool space. Also avoid it for very large strings, as pooling them provides no benefit and can impact garbage collection performance. Remember that `intern()` has a lookup cost, so profile before using it extensively.

---

### Interview Question 5

**Q: Explain the difference between `StringBuilder` and `StringBuffer`. In what scenarios would you choose one over the other in a production environment?**

**A**: Both StringBuilder and StringBuffer are mutable string classes, but StringBuilder is not thread-safe while StringBuffer is synchronized and thread-safe. In single-threaded scenarios, which represent 99% of string manipulation cases, StringBuilder is preferred because it's faster due to no synchronization overhead. Use StringBuffer only when multiple threads need to modify the same string object concurrently, which is rare in practice. For example, if you have a shared log buffer being written to by multiple threads, StringBuffer would be appropriate. However, even in multi-threaded contexts, it's often better to use thread-local StringBuilder instances or immutable strings with proper synchronization at a higher level.

---

### Interview Question 6

**Q: Why is string concatenation in loops a performance problem? Provide an example and explain the JVM-level behavior.**

**A**: String concatenation in loops using the `+` operator creates a new String object in each iteration because strings are immutable. For example, in a loop with 1000 iterations doing `result += i`, you create 1000 intermediate String objects, each copying all previous content. This results in O(n²) time complexity and excessive memory allocation, triggering frequent garbage collection. At the JVM level, each concatenation allocates a new character array, copies existing characters, appends new characters, and creates a new String object. Using StringBuilder instead maintains a single mutable buffer, expanding capacity as needed, resulting in O(n) complexity and significantly better performance—often 100x faster for large iterations.

---

### Interview Question 7

**Q: What will `s1 == s2` return in the following code? Explain why.**
```java
String s1 = "Hello";
String s2 = new String("Hello").intern();
```

**A**: This will return `true`. Here's why: `s1 = "Hello"` creates or references the string literal "Hello" in the String Pool. `new String("Hello")` creates a new object in the heap. However, calling `.intern()` on this heap object checks the pool for "Hello", finds it (because of `s1`), and returns a reference to that pooled object. Therefore, both `s1` and `s2` reference the same pooled String object, making the reference comparison `s1 == s2` return true. This demonstrates how `intern()` can reunify string references to leverage the pool.

---

### Interview Question 8

**Q: Explain how Java 9+ optimized string concatenation. What was the old approach, and how does the new approach improve performance?**

**A**: Before Java 9, the compiler converted string concatenation using `+` into explicit StringBuilder operations. For example, `s1 + s2 + s3` became `new StringBuilder().append(s1).append(s2).append(s3).toString()`. From Java 9 onwards, the compiler uses the `invokedynamic` bytecode instruction and delegates to `StringConcatFactory` methods. This allows the JVM to optimize concatenation strategies at runtime based on the specific scenario—it might use StringBuilder, direct byte array manipulation, or other optimizations without the compiler committing to a specific implementation. This makes concatenation more flexible and potentially faster. These improvements remain through Java 25.

---

### Interview Question 9

**Q: What are common mistakes developers make when comparing strings, and how would you prevent NullPointerException in string comparison?**

**A**: The most common mistake is using `==` instead of `.equals()` for content comparison, which compares references instead of content, leading to bugs. Another mistake is not handling null values, causing NullPointerException when calling `.equals()` on a null string. The best defensive pattern is placing the known non-null value (often a literal) first: `"EXPECTED".equals(variableString)`. This way, even if `variableString` is null, the method returns false instead of throwing an exception. Alternatively, use null checks: `if (str != null && str.equals("value"))`, or use Java 7+ `Objects.equals(str1, str2)` which handles nulls safely.

---

### Interview Question 10

**Q: In a high-throughput web service, you need to build JSON responses by concatenating hundreds of string fields. What approach would you recommend and why?**

**A**: In a high-throughput scenario, use StringBuilder to build the JSON response because it's mutable and efficient for repeated concatenation. Create a StringBuilder instance at the start, append each field incrementally, and call `toString()` once at the end. This avoids creating hundreds of intermediate String objects. If responses follow a similar pattern, consider using a StringBuilder with pre-allocated capacity based on expected size: `new StringBuilder(500)`. For even better performance in production, use a dedicated JSON library like Jackson or Gson, which handle string building efficiently internally and provide proper escaping. Avoid string concatenation with `+` in loops, as it creates O(n²) complexity.

---

### Interview Question 11

**Q: How does String's character storage work internally, and how did it change from Java 8 to Java 9?**

**A**: In Java 8 and earlier, String stored characters internally as a `char[]` array, where each character occupied 2 bytes (UTF-16 encoding). From Java 9 onwards, String uses a `byte[]` array combined with an encoding flag. If all characters in the string are Latin-1 (ASCII-compatible), they're stored as single bytes, saving 50% memory. If any character requires more than one byte, the string uses UTF-16 encoding (two bytes per character). This optimization, called "Compact Strings," significantly reduces memory usage for the common case where strings contain only Latin-1 characters. This internal change is transparent to developers and remains through Java 25.

---

### Interview Question 12

**Q: You're reviewing code that uses `intern()` extensively on user-generated content. What concerns would you raise, and what would you recommend?**

**A**: I would raise several concerns. First, interning user-generated content (potentially unique strings) can bloat the String Pool unnecessarily, as the pool retains these strings for longer than needed, impacting garbage collection. Second, excessive use of `intern()` can become a performance bottleneck because it requires hash table lookups and synchronization. Third, if user input is malicious or extremely large, interning could cause memory exhaustion. I would recommend removing `intern()` unless there's proven evidence of duplicate user input. Instead, use normal String objects and let the JVM's garbage collector handle them. If memory optimization is truly needed, consider using a Map to track duplicates at the application level where you have control over lifecycle.