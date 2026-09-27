## 17. Important Diagrams (Described in Words)

---

#### Diagram 17.1: JDK, JRE, JVM Relationship
##### Description:
- Draw three nested boxes.
- **Outermost box:** JDK (label: "Java Development Kit").
  - **Inside JDK:** Tools like javac, jar, javadoc, jdb.
- **Middle box:** JRE (label: "Java Runtime Environment").
  - **Inside JRE:** Core libraries (java.lang, java.util, etc.) and JVM.
- **Innermost box:** JVM (label: "Java Virtual Machine").
  - **Inside JVM:** Class Loader, Bytecode Verifier, Execution Engine (Interpreter + JIT Compiler).

---

#### Diagram 17.2: Java Execution Flow
##### Description:
- Flowchart with the following steps:
  1. Source Code (`HelloWorld.java`) → Arrow labeled "javac" →
  2. Bytecode (HelloWorld.class) → Arrow labeled "java" →
  3. JVM → Contains three sub-steps:
    - Class Loader (loads .class)
    - Bytecode Verifier (checks security)
    - Execution Engine (Interpreter + JIT) → Native Machine Code
  4. Output (displayed to user)

---

#### Diagram 17.3: Memory Layout During Execution
##### Description:
- Divide into three sections:
  - **Stack:** Show method frames (main(), greet()).
  - **Heap:** Show objects (new String("Hello")).
  - **Metaspace:** Show class metadata (HelloWorld.class).