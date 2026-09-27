## 21. One-Line Exam / Interview Answer

---

#### Q1: What is the difference between JDK, JRE, and JVM?
**A:** JDK is a development kit containing JRE and development tools like javac; JRE is a runtime environment containing JVM and core libraries; JVM is the execution engine that runs Java bytecode.

---

#### Q2: Explain how Java achieves platform independence.
**A:** Java source code compiles to platform-independent bytecode, which the platform-specific JVM interprets and converts to native machine code, enabling "Write Once, Run Anywhere."

---

#### Q3: Why must the main() method be static in Java?
**A:** The JVM calls main() to start execution without creating an object, so it must be static to belong to the class itself rather than an instance.

---

#### Q4: What happens if JAVA_HOME is not set?
**A:** Tools that rely on JAVA_HOME (like Maven, Gradle, IDEs) will fail to locate the JDK, though javac and java may still work if PATH is correctly set.

---

#### Q5: What is bytecode verification?
**A:** A JVM security mechanism that checks bytecode for illegal operations (like invalid type casts or stack overflows) before execution to prevent malicious code from running.