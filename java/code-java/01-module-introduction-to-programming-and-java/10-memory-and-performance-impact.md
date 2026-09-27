## 10. Memory & Performance Impact
Java's architecture involves multiple memory areas managed by the JVM.

---

#### 10.1 JVM Memory Areas
##### 10.1.1. **Heap**
- Stores objects and instance variables
- Shared across all threads
- Managed by the Garbage Collector

##### 10.1.2. **Stack**
- Stores method calls and local variables
- Each thread has its own stack
- LIFO (Last In, First Out) structure

##### 10.1.3. **Metaspace (Java 8+)**
- Stores class metadata (replaces PermGen)
- Uses native memory, not JVM heap

##### 10.1.4. **Method Area**
- Stores class structures, method bytecode, constant pool

---

#### 10.2 Performance Considerations:
- Java's JIT compiler optimizes bytecode at runtime, improving performance.
- Garbage Collection introduces pauses, but modern GCs (G1, ZGC, Shenandoah) minimize this.