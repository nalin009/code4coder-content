## MODULE 10: Methods

---
---

### Q1. Explain the difference between parameters and arguments with an example.

**Answer:** Parameters are variables declared in a method's signature that act as placeholders for values the method expects. Arguments are the actual values passed to the method when it is called. For example, in `public void add(int x, int y)`, `x` and `y` are parameters. When calling `add(5, 10)`, `5` and `10` are arguments. Parameters exist only during method declaration, while arguments are provided at runtime during method invocation.

---

### Q2. Why is Java considered "pass-by-value" and not "pass-by-reference"? Provide an example to support your answer.

**Answer:** Java is strictly pass-by-value because it copies the value of variables when passing them to methods. For primitives, the value itself is copied. For objects, the reference value (memory address) is copied, not the actual object. This means you can modify the object's state through the copied reference, but reassigning the reference inside the method does not affect the original reference. Example: if you pass an object and reassign it inside a method (`obj = new Object()`), the original reference remains unchanged outside the method.

---

### Q3. How does method overloading work at compile-time? What are the rules for valid overloading?

**Answer:** Method overloading allows multiple methods with the same name but different parameter lists within the same class. The compiler resolves the correct method at compile-time based on the number, type, and order of arguments. Valid overloading requires differences in the parameter list—return type alone does not determine overloading. Access modifiers can differ between overloaded methods. If the compiler cannot uniquely determine which method to call (ambiguity), a compile-time error occurs. Type promotion follows the order: byte → short → int → long → float → double.

---

### Q4. What is a stack frame, and what information does it contain during method execution?

**Answer:** A stack frame is a data structure created on the JVM call stack each time a method is invoked. It contains local variables declared within the method, method parameters passed during the call, the return address indicating where control should return after method completion, and an operand stack for intermediate computations during expression evaluation. When the method completes execution, its stack frame is popped from the call stack and destroyed, releasing the memory back to the stack.

---

### Q5. Explain recursion with a real-world example. What are the risks of using recursion in production code?

**Answer:** Recursion is when a method calls itself to solve smaller instances of the same problem. A classic example is calculating factorial: `factorial(n) = n * factorial(n-1)` with base case `factorial(0) = 1`. Each recursive call creates a new stack frame. The primary risk is StackOverflowError if recursion is too deep or lacks a proper base case, exhausting stack memory. In production, deep recursion can degrade performance due to function call overhead. For performance-critical applications, iteration is often preferred, though recursion remains valuable for tree traversal, backtracking, and divide-and-conquer algorithms.

---

### Q6. Why must the main() method be public, static, and void? Can you have multiple main() methods in a class?

**Answer:** The main() method must be `public` so the JVM can access it from outside the class, `static` so the JVM can invoke it without creating an instance (reducing startup overhead), and `void` because it does not return any value to the JVM (exit codes are handled via `System.exit()`). You can have multiple overloaded main() methods in a class, but the JVM recognizes only `public static void main(String[])` as the entry point. Other overloaded versions are regular methods that can be called explicitly within the program.

---

### Q7. What happens in memory when you pass an array to a method and modify its elements?

**Answer:** When an array is passed to a method, the reference to the array (memory address) is passed by value. Both the original reference and the method's parameter point to the same array object in heap memory. If you modify array elements inside the method (e.g., `arr[0] = 100`), the changes are reflected in the original array because both references point to the same object. However, if you reassign the parameter to a new array (`arr = new int[5]`), only the local reference changes—the original reference remains unaffected.

---

### Q8. Describe the difference between method overloading and method overriding.

**Answer:** Method overloading occurs when multiple methods in the same class have the same name but different parameter lists. It is resolved at compile-time (static polymorphism) and allows methods to handle different types or numbers of inputs. Method overriding occurs when a subclass provides a specific implementation for a method already defined in its superclass, with the exact same signature. It is resolved at runtime (dynamic polymorphism) and enables subclasses to modify or extend inherited behavior. Overloading focuses on compile-time flexibility, while overriding enables runtime polymorphism.

---

### Q9. What is tail recursion, and does Java optimize it?

**Answer:** Tail recursion is a special form of recursion where the recursive call is the last operation in the method, with no additional computation after the call returns. In tail-recursive functions, the current stack frame can theoretically be reused instead of creating a new one, avoiding stack growth. However, Java does NOT optimize tail recursion—the JVM does not perform tail call elimination. Each recursive call still creates a new stack frame, making tail recursion in Java no more efficient than regular recursion. This behavior remains unchanged till Java 25.

---

### Q10. Explain method inlining by the JIT compiler. When does it occur and why is it beneficial?

**Answer:** Method inlining is an optimization performed by the JIT (Just-In-Time) compiler where the method call is replaced by the method's body directly at the call site, eliminating the overhead of method invocation. It typically occurs for small, frequently called methods (hotspots detected during runtime profiling). Inlining improves performance by reducing stack frame creation/destruction overhead, improving cache locality, and enabling further optimizations like constant folding. The JIT compiler automatically determines which methods to inline based on runtime behavior and method size.

---

### Q11. Can you change the signature of the main() method and still run the program? What are valid variations?

**Answer:** You cannot change the essential signature `public static void main(String[])` and expect the JVM to recognize it as the entry point. Valid variations include using `String... args` (varargs), changing the array notation to `String args[]`, adding modifiers like `final` or `synchronized`, and changing the parameter name (e.g., `String[] xyz`). All of these are syntactically valid, but the JVM will only invoke `main(String[])` as the entry point. You can overload main() with different signatures, but those become regular methods, not entry points.

---

### Q12. What is the difference between local variables in a method and instance variables of a class?

**Answer:** Local variables are declared inside methods and exist only during method execution within the method's stack frame. They must be initialized before use and are destroyed when the method returns. Instance variables belong to objects and are stored in heap memory. They have default values (0, null, false) and exist as long as the object exists. Local variables have method scope, while instance variables have object scope. Local variables are faster to access (stack), while instance variables persist across multiple method calls and require heap access, which is slightly slower.