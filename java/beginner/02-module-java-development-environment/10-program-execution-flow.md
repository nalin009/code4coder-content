## 10. Program Execution Flow

---

#### 10.1 Step-by-Step Execution
###### **Example Program:**

```java
public class ExecutionFlow {
    static {
        System.out.println("Static block executed");
    }

    public static void main(String[] args) {
        System.out.println("Main method executed");
        greet();
    }

    static void greet() {
        System.out.println("Hello from greet method");
    }
}
```

###### **Execution Order**:
1. **Class Loading**: JVM loads `ExecutionFlow.class` into memory.
2. **Static Initialization**: Static blocks execute (if any).
   - Output: `Static block executed`
3. **main() Execution**: JVM calls `main()`.
   - Output: `Main method executed`
4. **Method Call**: `greet()` is called.
   - Output: `Hello from greet method`
5. **Program Termination**: `main()` finishes, program exits.

**Complete Output**:

```java
Static block executed
Main method executed
Hello from greet method
```

---

#### 10.2 Memory Allocation During Execution
##### Stack:
- Stores local variables and method call frames.
- When `main()` is called, a stack frame is created.
- When greet() is called, another stack frame is created on top of `main()`.

##### Heap:
- Stores objects.
- Example: `String s = new String("Hello");` → s reference stored in Stack, actual String object in Heap.

##### Metaspace (Java 8+):
- Stores class metadata (bytecode, static variables, method information).
- Replaces PermGen from Java 7.

**Key Point:** This memory model is unchanged till Java 25, though internal optimizations continue.