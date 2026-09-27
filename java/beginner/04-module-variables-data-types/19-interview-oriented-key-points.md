## 19. Interview-Oriented Key Points (Quick Revision)

---

**a.** **Local variables**: No default value, must initialize, stored on stack.

**b.** **Instance variables**: Default values, stored on heap with objects.

**c.** **Static variables**: Shared across instances, stored in Metaspace.

**d.** **8 primitive types**: `byte`, `short`, `int`, `long`, `float`, `double`, `char`, `boolean`.

**e.** **Wrapper classes**: Object representation of primitives, immutable, support null.

**f.** **Autoboxing**: Primitive → Wrapper (automatic).

**g.** **Unboxing**: Wrapper → Primitive (automatic, can throw NPE if null).

**h.** **Caching**: Integer cache -128 to 127; use `.equals()` for comparison.

**i.** **Implicit casting**: Smaller → Larger (safe).

**j.** **Explicit casting**: Larger → Smaller (manual, potential data loss).

**k.** **`final` keyword**: Makes variables constants (immutable).

**l.** **`var` keyword**: Local variable type inference (Java 10+).

**m.** **Overflow**: Silent wrapping (use `Math.*Exact()` to detect).

**n.** **Performance**: Primitives are faster than wrappers (avoid autoboxing in loops).

**o.** **Default values**: Primitives: 0/false/'\u0000', References: null.

---

#### 19.1. One-Line Exam / Interview Answer
"Variables are named memory locations that store data of a specific type; Java has 8 primitive types (stored directly) and reference types (storing object addresses), with wrapper classes providing object representations of primitives, supporting features like autoboxing, unboxing, and null values."