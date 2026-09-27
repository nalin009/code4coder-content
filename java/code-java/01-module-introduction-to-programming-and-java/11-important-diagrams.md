## 11. Important Diagrams (Described in Words)

---

#### Diagram 11.1: Java Execution Flow

```java
Step 1: Write Java source code (.java file)
Step 2: Compile using javac → generates bytecode (.class file)
Step 3: JVM loads bytecode
Step 4: Bytecode Verifier checks for security violations
Step 5: JIT Compiler converts bytecode to native machine code
Step 6: CPU executes machine code
```

---

#### Diagram 11.2: Platform Independence

```java
Same .class file (bytecode)
    ↓
JVM for Windows → Machine code for Windows
JVM for Linux → Machine code for Linux
JVM for Mac → Machine code for Mac
```

---

#### Diagram 11.3: Java Editions

```java
Java SE (Core)
    ↓
Java EE (Extends SE for Enterprise)
    ↓
Jakarta EE (Modern successor to Java EE)
     ↓
Java ME (Subset of SE for Embedded Systems)
```