## 5. Why Java Is Unique

### 5.1 Java Uses a Two-Step Process

1. **Compile-time:** Java source code (`.java`) is compiled into `bytecode` (`.class`) by the Java compiler (`javac`).

2. **Runtime:** The JVM executes the `bytecode`. It may interpret the bytecode and/or use `JIT (Just-In-Time) compilation` to compile frequently executed code into `machine code` for the underlying platform.

This approach contributes to Java's `portability` and `performance`.

---

### 5.2 History of Java

Understanding Java's history helps you appreciate why certain design decisions were made.

#### Timeline

| **Year** | **Event**                                                                                                                                                                                                                        |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1991** | `James Gosling`, `Mike Sheridan`, and `Patrick Naughton`, part of the "Green Team" at Sun Microsystems, started the Java project. The project was originally called `Oak` and was initially intended for interactive television. |
| **1995** | The language was renamed `Java`. Java 1.0 was officially released with the goal of **"Write Once, Run Anywhere" (WORA)**.                                                                                                        |
| **1996** | Java 1.1 introduced features such as `inner classes`, `JavaBeans`, `JDBC`, and `RMI`.                                                                                                                                            |
| **1998** | Java 2 (J2SE 1.2) introduced major features including `Swing` and the `Collections Framework`.                                                                                                                                   |
| **2004** | Java 5 (J2SE 5.0) introduced major language features such as `Generics`, `Annotations`, `Enums`, `Autoboxing`, the `Enhanced for-loop`, and `Varargs`.                                                                           |
| **2006** | Java 6 (Java SE 6) improved performance and introduced several enhancements, including scripting support.                                                                                                                        |
| **2010** | Oracle acquired Sun Microsystems and became the steward of Java.                                                                                                                                                                 |
| **2014** | Java 8 introduced `Lambda expressions`, the `Streams API`, and the `Date-Time API`, making it one of the most significant Java releases.                                                                                         |
| **2017** | Java 9 introduced the `Module System` (Project Jigsaw) and `JShell` (REPL).                                                                                                                                                      |
| **2018** | Java moved to a six-month release cycle. Java 10 introduced `var` for local variable type inference.                                                                                                                             |
| **2018** | Java 11, an `LTS` release, introduced the new `HTTP Client API` and removed several Java EE and CORBA modules from the JDK.                                                                                                      |
| **2021** | Java 17, an `LTS` release, introduced features such as `Sealed Classes` and stronger encapsulation of JDK internals.                                                                                                             |
| **2023** | Java 21, an `LTS` release, introduced features including `Virtual Threads`, `Record Patterns`, and `Sequenced Collections`.                                                                                                      |
| **2025** | Java 25, an `LTS` release, continued Java's evolution with further language, JVM, and library enhancements.                                                                                                                      |

### Key Takeaway

Java has evolved from a language originally designed for consumer and embedded-device applications into a versatile platform used across `enterprise applications`, `Android`, `cloud`, `big data`, and `microservices`.
