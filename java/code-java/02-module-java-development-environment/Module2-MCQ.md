## MODULE: 2 Java Development Environment

---

##### MCQ 1 Beginner
##### What does JDK stand for?
##### A) Java Development Kit
##### B) Java Deployment Kit
##### C) Java Debugging Kit
##### D) Java Distribution Kit
###### Answer: A) Java Development Kit
###### Explanation: JDK stands for Java Development Kit, which includes development tools like javac, jar, and the JRE.

---

##### MCQ 2 Beginner
##### Which command is used to compile a Java program?
##### A) java
##### B) javac
##### C) compile
##### D) javarun
###### Answer: B) javac
###### Explanation: The javac command invokes the Java compiler, which converts .java source files into .class bytecode files.

---

##### MCQ 3 Beginner
##### What is the file extension of Java bytecode?
##### A) .java
##### B) .class
##### C) .byte
##### D) .jvm
###### Answer: B) .class
###### Explanation: Compiled Java programs are stored in .class files containing platform-independent bytecode.

---

##### MCQ 4 Beginner
##### How many public classes can a single Java source file contain?
##### A) No limit
##### B) Exactly one
##### C) Two
##### D) Depends on the JVM
###### Answer: B) Exactly one
###### Explanation: A Java source file can contain at most one public class, and the filename must match the public class name.

---

##### MCQ 5 Intermediate
##### Which component of the Java platform is platform-specific?
##### A) Bytecode
##### B) JVM
##### C) Source Code
##### D) JRE Libraries
###### Answer: B) JVM
###### Explanation: The JVM is platform-specific (different implementations for Windows, Linux, Mac), but it executes the same platform-independent bytecode.

---

##### MCQ 6 Intermediate
##### What will happen if the main() method is declared as public void main(String[] args) (without static)?
##### A) Compilation error
##### B) Runtime error
##### C) Program runs successfully
##### D) JVM throws NullPointerException
###### Answer: B) Runtime error
###### Explanation: The program compiles successfully, but at runtime, the JVM throws: Error: Main method is not static in class ClassName.

---

##### MCQ 7 Intermediate
##### Which environment variable should point to the JDK installation directory?
##### A) JAVA_PATH
##### B) JAVA_HOME
##### C) JDK_HOME
##### D) CLASSPATH
###### Answer: B) JAVA_HOME
###### Explanation: JAVA_HOME is the standard environment variable that should point to the root of the JDK installation directory.

---

##### MCQ 8 Intermediate
##### What is the purpose of bytecode verification in the JVM?
##### A) To optimize code execution
##### B) To check for syntax errors
##### C) To ensure bytecode is safe and doesn't violate security constraints
##### D) To convert bytecode to machine code
###### Answer: C) To ensure bytecode is safe and doesn't violate security constraints
###### Explanation: To ensure bytecode is safe and doesn't violate security constraints
Explanation: Bytecode verification is a JVM security mechanism that checks bytecode for illegal operations before execution to prevent malicious code.

---

##### MCQ 9 Intermediate
##### Which of the following is a valid Java identifier?
##### A) 123variable
##### B) _myVariable
##### C) class
##### D) my-variable
###### Answer: B) _myVariable
###### Explanation: Identifiers can start with a letter, underscore, or dollar sign. 123variable starts with a digit (invalid), class is a keyword (invalid), and my-variable contains a hyphen (invalid).

---

##### MCQ 10 Intermediate
##### Which of the following statements about Java keywords is TRUE?
##### A) Keywords are case-insensitive
##### B) goto is a valid keyword used for control flow
##### C) const is reserved but not used in Java
##### D) var is a reserved keyword in all contexts
###### Answer: C) const is reserved but not used in Java
###### Explanation: const and goto are reserved keywords but are not used in Java. Keywords are case-sensitive. var is a contextual keyword (Java 10+) for local variable type inference.

---

##### MCQ 11 Intermediate
##### What is the output of the following program if the static block is present?
```java
public class Test {
    static {
        System.out.println("Static block");
    }

    public static void main(String[] args) {
        System.out.println("Main method");
    }
}
```

##### A) Main method then Static block
##### B) Static block then Main method
##### C) Only Main method
##### D) Compilation error
###### Answer: B) Static block then Main method
###### Explanation: Static blocks execute during class loading, which happens before main() is called. Output: Static block followed by Main method.

---

##### MCQ 12 Advanced
##### In which memory area does the JVM store class metadata (like bytecode and static variables) in Java 8 and later?
##### A) Heap
##### B) Stack
##### C) PermGen
##### D) Metaspace
###### Answer: D) Metaspace
###### Explanation: Java 8 replaced PermGen with Metaspace for storing class metadata. Metaspace uses native memory and grows dynamically.

---

##### MCQ 13 Advanced
##### What is the role of the JIT (Just-In-Time) compiler in the JVM?
##### A) It compiles Java source code to bytecode
##### B) It converts bytecode to native machine code at runtime for performance optimization
##### C) It interprets bytecode line by line
##### D) It performs garbage collection
###### Answer: B) It converts bytecode to native machine code at runtime for performance optimization
###### Explanation: The JIT compiler identifies frequently executed bytecode (hot spots) and compiles it to native machine code for faster execution, improving performance.

---

##### MCQ 14 Advanced
##### In a Docker container running a Java application, which is the better choice for the base image to reduce size?
##### A) JDK-based image
##### B) JRE-based image
##### C) Operating system with Java source code
##### D) JVM-only image
###### Answer: B) JRE-based image
###### Explanation: Production containers only need the JRE to run Java applications. Using JRE-based images reduces image size (JRE ~150-200 MB vs JDK ~300-400 MB) and reduces the attack surface.

---

##### MCQ 15 Advanced
##### When you run java HelloWorld, what does the JVM search for?
##### A) HelloWorld.java file
##### B) HelloWorld.class file
##### C) main.class file
##### D) HelloWorld.jvm file
###### Answer: B) HelloWorld.class file
###### Explanation: The java command expects compiled bytecode (.class files), not source code (.java files). It loads HelloWorld.class into memory.

---