## 20. Interview-Oriented Key Points (Quick Revision)

----

**a.** `JDK` = `JRE` + `Development Tools`; `JRE` = `JVM` + `Core Libraries`.

**b.** `Compilation` (javac) converts .java to .class (bytecode); JVM executes `bytecode`.

**c.** `Bytecode` is platform-independent; `JVM` is platform-specific.

**d.** `main()` signature must be: `public static void main(String[] args)`.

**e.** `JAVA_HOME` points to `JDK` directory; `PATH` includes `$JAVA_HOME/bin`.

**f.** `CLASSPATH` tells `JVM` where to find `.class` files and `libraries`.

**g.** `Keywords` (53 total) are `reserved`; cannot be used as `identifiers`.

**h.** `Identifiers` can start with `letter`, `_` , or `$`; cannot start with a digit.

**i.** Filename must match `public class name` (case-sensitive).

**j.** One `public` class per file; multiple `non-public` classes allowed.

**k.** `JIT Compiler` optimizes `bytecode` to native code at `runtime` for performance.

**l.** Static blocks execute before `main()` during class loading.

**m.** `Stack` stores `method calls` and `local variables`; `Heap` stores `objects`.

**n.** `Metaspace` (Java 8+) stores `class metadata`; replaced PermGen.

**o.** Java 11+ allows running `.java` files directly with `java` (source-file mode), but not standard for production.

--- 