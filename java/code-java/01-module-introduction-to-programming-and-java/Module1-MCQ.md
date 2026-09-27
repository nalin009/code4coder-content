## MODULE 1:  Introduction to Programming & Java

---
---

##### MCQ 1 (Beginner)
##### What is the primary purpose of a programming language?
##### A) To execute machine code directly
##### B) To provide a way for humans to communicate instructions to computers
##### C) To replace operating systems
##### D) To store data in databases
###### Answer: B) To provide a way for humans to communicate instructions to computers
###### Explanation: A programming language acts as a bridge between human logic and machine execution. It allows developers to write instructions in a human-readable format that can be translated into machine code.

---

##### MCQ 2  (Beginner)
##### Which of the following is NOT a feature of Java?
##### A) Platform Independent
##### B) Object-Oriented
##### C) Supports Pointers
##### D) Multithreaded
###### Answer: C) Supports Pointers
###### Explanation: Java does not support pointers to ensure security and simplicity. Pointers allow direct memory access, which can lead to security vulnerabilities and crashes.

---

##### MCQ 3 (Beginner)
##### What is bytecode in Java?
##### A) Machine code specific to Windows
##### B) An intermediate, platform-independent representation of Java programs
##### C) The source code written by developers
##### D) A type of virus
###### Answer: B) An intermediate, platform-independent representation of Java programs
###### Explanation: Bytecode is the compiled form of Java source code (.class files). It is platform-independent and executed by the JVM, which converts it to machine code for the specific operating system.

---

##### MCQ 4  (Beginner)
##### Which of the following is a valid reason for Java's popularity?
##### A) It requires manual memory management
##### B) It supports pointers for low-level operations
##### C) It is platform-independent and has a rich ecosystem
##### D) It is only used for Android development
###### Answer: C) It is platform-independent and has a rich ecosystem
###### Explanation: Java's popularity stems from its platform independence (WORA), robust ecosystem (frameworks like Spring, Hibernate), strong community support, and wide applicability across domains (web, mobile, enterprise, big data).

---

##### MCQ 5 (Beginner)
##### Which of the following is NOT an application of Java?
##### A) Web development
##### B) Operating system development
##### C) Mobile development (Android)
##### D) Big data processing
###### Answer: B) Operating system development
###### Explanation: Java is not typically used for operating system development, which requires low-level system programming languages like C or Assembly. Java is used for web, mobile, big data, and enterprise applications.

---

##### MCQ 6 (Intermediate)
##### What does "Write Once, Run Anywhere" (WORA) mean in Java?
##### A) Java code can be written on any text editor
##### B) Java bytecode can run on any platform with a JVM without modification
##### C) Java programs run faster on all operating systems
##### D) Java does not require compilation
###### Answer: B) Java bytecode can run on any platform with a JVM without modification
###### Explanation: WORA means that once Java source code is compiled into bytecode, it can run on any platform (Windows, Mac, Linux) that has a JVM, without needing to recompile.

---

##### MCQ 7 (Intermediate)
##### Which Java edition is used for building enterprise applications?
##### A) Java SE
##### B) Java ME
##### C) Java EE / Jakarta EE
##### D) Java FX
###### Answer: C) Java EE / Jakarta EE
###### Explanation: Java EE (now Jakarta EE) extends Java SE with APIs for building large-scale, distributed, multi-tier enterprise applications like web servers, ERP systems, and banking platforms.

---

##### MCQ 8 (Intermediate)
##### What is the role of the JVM in Java?
##### A) To write Java code
##### B) To compile Java source code to bytecode
##### C) To execute bytecode and convert it to machine code for the specific platform
##### D) To manage databases
###### Answer: C) To execute bytecode and convert it to machine code for the specific platform
###### Explanation: The JVM (Java Virtual Machine) loads, verifies, and executes bytecode. It converts bytecode into native machine code for the underlying operating system, enabling platform independence.

---

##### MCQ 9 (Intermediate)
##### What replaced PermGen in Java 8?
##### A) Heap
##### B) Stack
##### C) Metaspace
##### D) Method Area
###### Answer: C) Metaspace
###### Explanation: In Java 8, PermGen (Permanent Generation) was replaced by Metaspace. Metaspace stores class metadata and uses native memory instead of JVM heap, reducing OutOfMemoryError issues.

---

##### MCQ 10 (Intermediate)
##### What is the purpose of the Garbage Collector in Java?
##### A) To delete unused bytecode
##### B) To automatically deallocate memory occupied by objects no longer in use
##### C) To compile Java source code
##### D) To optimize CPU usage
###### Answer: B) To automatically deallocate memory occupied by objects no longer in use
###### Explanation: The Garbage Collector (GC) is a JVM component that automatically identifies and frees memory occupied by objects that are no longer referenced by the program, preventing memory leaks.

---

##### MCQ 11 (Intermediate)
##### What is the significance of Java being "strongly typed"?
##### A) Variables must be explicitly declared with a data type
##### B) Java does not support type casting
##### C) Java allows variables to change types at runtime
##### D) Java does not have primitive data types
###### Answer: A) Variables must be explicitly declared with a data type
###### Explanation: Java is a strongly typed language, meaning every variable must be declared with a specific data type (e.g., int, String). This enforces type safety at compile-time, reducing runtime errors.

---

##### MCQ 12 (Advanced)
##### What is the difference between Java SE and Java ME?
##### A) Java SE is for desktops, Java ME is for mobile devices
##### B) Java SE is interpreted, Java ME is compiled
##### C) Java SE uses the JVM, Java ME does not
##### D) There is no difference
###### Answer: A) Java SE is for desktops, Java ME is for mobile devices
###### Explanation: Java SE (Standard Edition) is the core platform for general-purpose desktop and server applications. Java ME (Micro Edition) is a subset designed for resource-constrained devices like mobile phones, embedded systems, and IoT devices.

---

##### MCQ 13 (Advanced)
##### Which Java feature was introduced in Java 21 to improve concurrency?
##### A) Lambda Expressions
##### B) Virtual Threads (Project Loom)
##### C) Streams API
##### D) Generics
###### Answer: B) Virtual Threads (Project Loom)
###### Explanation: Java 21 introduced Virtual Threads (part of Project Loom), which are lightweight threads that allow applications to scale to millions of concurrent tasks efficiently, improving performance in highly concurrent systems.

---

##### MCQ 14 (Advanced)
##### Which statement is TRUE about Java's compilation and execution process?
##### A) Java is purely interpreted like Python
##### B) Java is purely compiled like C++
##### C) Java is compiled to bytecode, then interpreted or JIT-compiled by the JVM
##### D) Java does not require compilation
###### Answer: C) Java is compiled to bytecode, then interpreted or JIT-compiled by the JVM
###### Explanation: Java uses a hybrid approach. The source code is compiled to platform-independent bytecode by the Java compiler (javac). The JVM then interprets or uses Just-In-Time (JIT) compilation to convert bytecode to native machine code at runtime.

---

##### MCQ 15 (Advanced)
##### What is the main advantage of Java's JIT (Just-In-Time) compiler?
##### A) It compiles code before execution
##### B) It interprets bytecode line-by-line
##### C) It compiles frequently used bytecode into native machine code at runtime, improving performance
##### D) It reduces the size of bytecode
###### Answer: C) It compiles frequently used bytecode into native machine code at runtime, improving performance
###### Explanation: The JIT compiler identifies "hot spots" (frequently executed code) in bytecode and compiles them into native machine code at runtime. This significantly improves performance compared to pure interpretation.

---