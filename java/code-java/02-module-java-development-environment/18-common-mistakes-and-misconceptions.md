## 18. Common Mistakes & Misconceptions

---

###### **Mistake 1: Confusing JDK, JRE, and JVM**
**Misconception:** "JDK and JVM are the same."
**Reality:** `JVM` is a `subset` of `JRE`, which is a `subset` of `JDK`.

---

###### **Mistake 2: Running .java Files with java Command**
**Mistake:** java HelloWorld.java
**Correct:** First `compile` with `javac` `HelloWorld.java`, then run `java` `HelloWorld`.
**Note: Java 11+ allows `java HelloWorld.java` (source-file mode), but this is NOT standard for production code.**

---

###### **Mistake 3: Incorrect JAVA_HOME Path**
**Mistake:** Setting `JAVA_HOME` to `C:\Program Files\Java\jdk-21\bin`
**Correct:** `C:\Program Files\Java\jdk-21 (do NOT include bin)`.

---

###### **Mistake 4: Not Matching Public Class Name with Filename**
**Mistake:** File named `Test.java` but contains `public` `class Demo`.
**Compiler Error:** class Demo is `public`, should be declared in a file named `Demo.java`

---

###### **Mistake 5: Using Keywords as Identifiers**
**Mistake:** int class = 10;
**Compiler Error:** not a statement
**Reality:** class is a `keyword`; cannot be used as a `variable` name.

---

###### **Mistake 6: Assuming main() Can Have Any Signature**
**Mistake:** `public void main(String[] args)` (missing static)
**Compiler:** Compiles successfully.
**Runtime:** Error: Main method is not static in class HelloWorld

---

###### **Mistake 7: Ignoring Case Sensitivity**
**Mistake:** Saving file as `helloworld.java` but class named HelloWorld.
**Compiler Error:** cannot find symbol (on Linux/macOS; Windows may be lenient).

---

###### **Mistake 8: Misunderstanding Bytecode**
**Misconception:** "Bytecode is machine code."
**Reality:** Bytecode is an intermediate representation; JVM converts it to machine code.