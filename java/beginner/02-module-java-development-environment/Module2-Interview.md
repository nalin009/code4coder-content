## MODULE: 2 Java Development Environment

---
---

#### Question 1: What is the fundamental difference between JDK, JRE, and JVM? Why does this matter in production environments?
**Answer:** JDK (Java Development Kit) is a complete software development kit that includes the JRE plus development tools like the Java compiler (javac), debugger (jdb), and documentation tools. JRE (Java Runtime Environment) contains the JVM and core libraries necessary to run Java applications but lacks development tools. JVM (Java Virtual Machine) is the execution engine that interprets and executes bytecode. In production environments, we typically deploy only the JRE (or JRE-based Docker images) to minimize the deployment footprint, reduce security vulnerabilities, and avoid exposing development tools unnecessarily. This distinction is critical for containerized applications where image size and attack surface matter.

---

#### Question 2: Explain the complete execution flow of a Java program from source code to output. What happens at compile-time vs runtime?
**Answer:** At compile-time, the Java compiler (javac) reads the source code (.java file), performs syntax and type checking, and generates platform-independent bytecode stored in .class files. At runtime, the JVM loads the .class file using the Class Loader, verifies the bytecode for security using the Bytecode Verifier, and then the Execution Engine (comprising an Interpreter and JIT Compiler) converts bytecode to native machine code for execution. The Interpreter executes bytecode line-by-line, while the JIT Compiler optimizes frequently executed code (hot spots) by compiling it directly to native machine code for performance. This two-phase model enables platform independence—the same bytecode runs on any OS with a JVM.

---

#### Question 3: Why must the main() method be public, static, and void? What happens if any of these modifiers are missing?
**Answer:** The main() method must be public so the JVM (an external entity) can access it to start execution. It must be static because the JVM calls main() without creating an object—if it were non-static, the JVM would need to instantiate the class first, creating a circular dependency problem. It must be void because the JVM doesn't expect a return value; program exit status is controlled via System.exit(int). If main() is not public, the JVM throws a runtime error. If not static, the error is: Main method is not static in class ClassName. If not void, the error is: Main method must return a value of type void.

---

#### Question 4: What is bytecode, and why does Java use it instead of compiling directly to machine code?
**Answer:** Bytecode is an intermediate, platform-independent instruction set that sits between source code and machine code. Java uses bytecode to achieve platform independence ("Write Once, Run Anywhere"). Traditional compiled languages like C/C++ compile directly to platform-specific machine code, requiring recompilation for each OS. Java compiles source code once into bytecode, which the platform-specific JVM then interprets or compiles to native machine code at runtime. This design allows the same .class file to run on Windows, Linux, or Mac without modification. The trade-off is a slight performance overhead due to interpretation, but modern JVMs use JIT compilation to optimize hot code paths, significantly reducing this overhead.

---

#### Question 5: What is the role of the JIT (Just-In-Time) compiler, and how does it improve performance?
**Answer:** The JIT compiler is part of the JVM's Execution Engine that improves performance by converting frequently executed bytecode into native machine code at runtime. Initially, the JVM interprets bytecode line-by-line, which is slower. The JIT compiler monitors execution and identifies "hot spots"—code paths that are executed frequently (e.g., loops, frequently called methods). It then compiles these hot spots to optimized native machine code, which the CPU can execute directly, bypassing interpretation. This adaptive optimization means Java programs can sometimes match or exceed the performance of statically compiled languages after a warm-up period. Modern JVMs (HotSpot, GraalVM) use sophisticated JIT techniques like inlining, loop unrolling, and escape analysis.

---

#### Question 6: Explain the difference between compile-time errors and runtime errors with examples.
**Answer:** Compile-time errors occur during the compilation phase when the Java compiler (javac) detects issues with syntax, types, or semantics. Examples include missing semicolons, undeclared variables, type mismatches (String s = 10;), or calling undefined methods. These errors prevent the generation of .class files. Runtime errors occur during program execution and are not detected by the compiler. Examples include NullPointerException, ArrayIndexOutOfBoundsException, ArithmeticException (division by zero), or ClassNotFoundException. Compile-time errors are caught early and are easier to fix, while runtime errors require testing and defensive programming to handle gracefully using try-catch blocks or input validation.

---

#### Question 7: What are environment variables like JAVA_HOME, PATH, and CLASSPATH, and why are they important?
**Answer:** Environment variables are system-level settings that tell the OS where to find executables and libraries. JAVA_HOME points to the JDK installation directory and is used by tools like Maven, Gradle, and IDEs to locate Java. PATH contains directories where the OS searches for executable commands; adding $JAVA_HOME/bin to PATH allows running javac and java from any directory. CLASSPATH tells the JVM where to find user-defined classes and external libraries (.jar files). Incorrect environment variables lead to errors like "javac is not recognized" (PATH issue) or NoClassDefFoundError (CLASSPATH issue). In modern development, build tools manage CLASSPATH automatically, but understanding these variables is crucial for troubleshooting deployment and CI/CD pipeline issues.

---

#### Question 8: What happens during class loading, and what are the three sub-processes involved?
**Answer:** Class loading is the process by which the JVM loads .class files into memory. It involves three sub-processes: (1) Loading: The Class Loader reads the .class file and creates a Class object in the Metaspace (Java 8+) or Method Area (Java 7 and earlier). (2) Linking: This phase is further divided into (a) Verification—the Bytecode Verifier checks bytecode for security and correctness, (b) Preparation—memory is allocated for static variables and initialized to default values, and (c) Resolution—symbolic references in bytecode are replaced with direct references. (3) Initialization: Static initializers and static blocks are executed. If a class has a static block, it runs during this phase, before main() is called.

---

#### Question 9: What is the difference between Stack, Heap, and Metaspace in the JVM?
**Answer:** Stack memory stores method call frames and local variables. Each thread has its own stack, and when a method is called, a stack frame is pushed onto the stack; when the method returns, the frame is popped. Stack is LIFO (Last In, First Out) and is automatically managed—no garbage collection is needed. Heap memory stores objects and instance variables. It is shared among all threads and is managed by the Garbage Collector, which reclaims memory from unreachable objects. Metaspace (Java 8+) stores class metadata (bytecode, method information, static variables). It replaced PermGen and uses native memory, growing dynamically, which reduces OutOfMemoryError: PermGen space issues common in Java 7 and earlier.

---

#### Question 10: What are Java keywords, and can you name some categories with examples?
**Answer:** Java keywords are reserved words with predefined meanings that cannot be used as identifiers. There are 53 keywords (as of Java 25). Categories include: (1) Access Modifiers: public, private, protected; (2) Data Types: int, float, double, boolean, char, byte, short, long, void; (3) Control Flow: if, else, switch, case, for, while, do, break, continue, return; (4) Class/Object/Interface: class, interface, extends, implements, new, this, super; (5) Exception Handling: try, catch, finally, throw, throws; (6) Modifiers: static, final, abstract, synchronized, volatile, transient, native; (7) Unused/Reserved: goto, const (reserved but not used).

---

#### Question 11: What are the rules for valid Java identifiers, and what naming conventions should be followed?
**Answer:** Valid Java identifiers can contain letters (A-Z, a-z), digits (0-9), underscores (_), and dollar signs ($), but cannot start with a digit. They cannot be Java keywords. Identifiers are case-sensitive (age, Age, AGE are distinct). While technically unlimited in length, practical limits apply. Naming conventions (not enforced by the compiler but industry-standard) include: (1) Classes/Interfaces: PascalCase (e.g., Student, EmployeeDetails); (2) Methods/Variables: camelCase (e.g., calculateSalary, employeeName); (3) Constants: ALL_UPPERCASE with underscores (e.g., MAX_VALUE, PI); (4) Packages: all lowercase, often reverse domain (e.g., com.company.project). Following these conventions improves code readability and professionalism, and is expected in interviews and production code.

---

#### Question 12: Why does Java require the filename to match the public class name, and what happens if they don't match?
**Answer:** Java requires the filename to match the public class name (case-sensitive) to maintain a clear mapping between source files and class definitions, which simplifies class loading and reduces ambiguity. If a file named Test.java contains public class Demo, the Java compiler throws a compile-time error: class Demo is public, should be declared in a file named Demo.java. This rule applies only to public classes. A source file can contain multiple non-public classes, and the filename can match any of them (though it's best practice to match the first or primary class). This design decision enforces code organization and makes it easier for the JVM and developers to locate classes.