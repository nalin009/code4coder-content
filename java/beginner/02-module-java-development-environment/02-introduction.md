## 2 Introduction

---

#### 2.1 Why This Topic Exists
Before writing even a single line of Java code, you must understand the environment in which Java programs are `created`, `compiled`, and `executed`. Java's revolutionary "`Write Once, Run Anywhere`" (WORA) promise depends entirely on understanding how the Java Development Kit (JDK), Java Runtime Environment (JRE), and Java Virtual Machine (JVM) work together.

---

#### 2.2 What Problem Java Is Solving
In the early 1990s, programs written for one operating system (like Windows) couldn't run on another (like Unix or Mac). Developers had to rewrite and recompile code for each platform. Java solved this by introducing an intermediate layer—the JVM—that translates platform-independent bytecode into platform-specific machine code. This means you write your code once, and it runs on any device with a JVM.

---

#### 2.3 Why Beginners Struggle With This Topic
###### **Most beginners want to jump straight into coding without understanding:**
- What happens when they type javac or java
- The difference between `JDK`, `JRE`, and `JVM` (often used interchangeably but are NOT the same)
- Why `PATH` and `CLASSPATH` matter
- What `bytecode` is and why it exists

This lack of foundational knowledge leads to errors like `"javac is not recognized"` or confusion about why Java code needs both compilation and execution steps.

---

#### 2.4 Why Interviewers Ask This (Especially 3–5+ Years Experience)
###### **For experienced developers, interviewers expect:**
- **Deep understanding of JVM internals:** How does `bytecode` get `interpreted`? What is `JIT` compilation?
- **JDK vs JRE distinction:** When do you need `JDK` vs just `JRE` in production?
- **Performance implications:** How does the `JVM` optimize code at runtime?
- **Troubleshooting skills:** Understanding environment setup helps debug `classpath` issues, `version` conflicts, and `deployment` problems in production.

Interviewers use these questions to assess whether you understand Java beyond syntax—whether you know how Java actually works under the hood.