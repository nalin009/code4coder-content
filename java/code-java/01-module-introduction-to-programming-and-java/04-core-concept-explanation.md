# 4. Core Concept Explanation

## 4.1 What is Programming?

Imagine you want to teach a `robot` to make tea. You would give it step-by-step instructions:

1. Take a clean pan.
2. Fill the pan with water.
3. Place the pan on the stove.
4. Turn on the stove.
5. Wait until the water starts boiling.
6. Add tea leaves and sugar into the boiling water.
7. Add milk to the pan.
8. Let it boil again for 1–2 minutes.
9. Turn off the stove.
10. Take a cup.
11. Pour the tea into the cup using a strainer.

`Programming` works the same way. You write instructions (code) that tell a computer `what to do`. The computer follows these instructions according to the rules of the programming language and execution environment.

### Key Insight

Computers ultimately execute machine instructions represented in binary. Programming languages like `Java` allow developers to write `human-readable` instructions, which are then translated into forms that the computer can execute.

---

## 4.2 What is a Programming Language?

A programming language is a tool used to communicate instructions to a computer. Just as humans use English, Hindi, or Spanish to communicate, programmers use languages like Java, Python, or C++ to write instructions for computers.

### Components of a Programming Language

1. **Syntax:** The `grammar` and `structure` of a programming language, such as how to write an `if` statement.

2. **Semantics:** The meaning behind the `syntax`, such as what an `if` statement actually does.

3. **Compiler/Interpreter:** Software that translates or executes program code so that it can ultimately be executed by the computer.

---

## 4.3 Types of Programming Languages

Programming languages can be broadly classified based on their level of abstraction from hardware and how programs are translated or executed.

### 4.3.1 Low-Level Languages

#### Machine Language (Binary)

* Consists of **0s** and **1s**.
* Directly understood by the CPU.
* Not human-readable.
* **Example:** `10110000 01100001`

#### Assembly Language

* Uses symbolic codes (mnemonics) like **ADD**, **MOV**, and **SUB**.
* Requires an assembler to convert it into machine code.
* Still hardware-dependent.
* **Example:** `MOV AX, 5`

#### Why Java Is NOT a Low-Level Language

Java abstracts many hardware details, making it easier for developers to write, understand, and maintain code.

### 4.3.2 High-Level Languages

High-level languages are designed to be easier for humans to read, write, and maintain than low-level languages.

#### Characteristics

* Human-readable syntax.
* Higher level of abstraction from hardware.
* Generally require translation or execution by language-specific tools such as compilers, interpreters, or virtual machines.
* Examples include Java, Python, C++, and JavaScript.

---

## 4.4 Further Classification of High-Level Languages

### 4.4.1 Compiled Languages

* Source code is translated into another executable form before or as part of execution.
* **Examples:** `C`, `C++`
* **Java:** Java source code is compiled into `bytecode`, not directly into native machine code.

### 4.4.2 Interpreted Languages

* Program code is executed by an interpreter or runtime environment rather than being directly compiled into native machine code ahead of execution.
* **Examples:** `Python`, `JavaScript`
* **Java:** Java bytecode can be interpreted by the `JVM`.

### 4.4.3 Hybrid Languages

Java is commonly described as a **hybrid language** because its execution combines compilation and runtime execution.

* Java source code is first `compiled` into an intermediate form called `bytecode`.
* The `JVM` executes the bytecode.
* The JVM can interpret bytecode and also use `JIT (Just-In-Time) compilation` to compile frequently executed code into native machine code.
* **Examples:** `Java`, `C#`