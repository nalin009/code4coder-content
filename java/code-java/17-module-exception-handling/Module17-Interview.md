## MODULE 17: Exception Handling

---
---

### Question 1: What is the difference between Error and Exception in Java?

**Answer**: Error and Exception are both subclasses of Throwable, but they serve different purposes. Error represents serious problems that are typically external to the application and should not be caught, such as OutOfMemoryError or StackOverflowError—these indicate the JVM itself is in trouble. Exception represents conditions that applications should catch and potentially recover from, such as IOException or SQLException. Exceptions are further divided into checked exceptions (must be declared or caught) and unchecked exceptions like RuntimeException (indicate programming errors). This design separates recoverable conditions from catastrophic failures, and this distinction has remained unchanged till Java 25.

---

### Question 2: Explain the difference between throw and throws with examples.

**Answer**: throw and throws serve completely different purposes. throw is a keyword used inside a method body to explicitly throw an exception object: `throw new IllegalArgumentException("Invalid input");` It performs an action and stops execution immediately. throws is used in the method signature to declare that a method might throw certain checked exceptions: `public void readFile() throws IOException`. It's a declaration for the compiler and callers, not an action. You use throw when you want to signal an error, and throws when you want to declare potential errors. A method can use throw without throws (for unchecked exceptions), but checked exceptions require both throw inside and throws in the signature.

---

### Question 3: Why should exceptions not be used for control flow?

**Answer**: Using exceptions for control flow is a significant anti-pattern due to performance costs. When an exception is thrown, the JVM must capture the entire call stack by walking through all the frames and creating an array of StackTraceElement objects, which is expensive—roughly 100-1000x more costly than a normal method call. Additionally, exception throwing disrupts the CPU's branch prediction and instruction pipelining, further degrading performance. Exceptions also create heap objects that increase GC pressure. They're designed for truly exceptional, rare conditions, not normal program logic. For example, using NumberFormatException to check if a string is numeric is much slower than using regex or character validation. This principle has been a best practice since Java's inception and remains unchanged till Java 25.

---

### Question 4: When should you use checked exceptions versus unchecked exceptions?

**Answer**: Use checked exceptions when the caller can reasonably recover from the failure and when the failure is an expected part of the operation, such as FileNotFoundException when opening a file—the caller might prompt the user for a different path. Use unchecked exceptions (RuntimeException) for programming errors that indicate bugs which should be fixed, such as NullPointerException or IllegalArgumentException. Checked exceptions force explicit handling at compile time, making them suitable for APIs where failure modes need to be explicit. However, overuse leads to verbose code and empty catch blocks. Modern frameworks often favor unchecked exceptions to avoid this verbosity. The choice depends on whether the condition is recoverable and whether you want compile-time enforcement of handling. This design philosophy has remained consistent and is unchanged till Java 25.

---

### Question 5: Explain what happens during exception propagation in the JVM.

**Answer**: When an exception is thrown and not caught in the current method, the JVM performs stack unwinding. It immediately stops executing the current method, pops its frame off the call stack, and checks the caller's method for a matching catch block. The JVM uses instanceof logic to match the thrown exception against each catch block's parameter type in order. If a match is found, that catch block executes; if not, the frame is popped and the search continues up the call stack. At each level, any finally blocks are executed before popping the frame. If the exception propagates all the way to the main method without being caught, the JVM terminates the thread, prints the stack trace showing the full call chain, and if it's the main thread, the program terminates. This unwinding is automatic and is part of the JVM specification, unchanged till Java 25.

---

### Question 6: What is exception chaining and why is it important?

**Answer**: Exception chaining is the practice of wrapping a caught exception in a new exception while preserving the original as the cause. You do this by passing the original exception to the new exception's constructor: `throw new ServiceException("Service failed", originalException);` This is crucial for debugging production issues because it preserves the complete error context and stack trace. When you catch a low-level exception like SQLException and throw a high-level domain exception like DataAccessException, chaining lets you see both the high-level business context and the root technical cause. The full chain is accessible via getCause() and is printed in stack traces. Without chaining, the original exception and its valuable information are lost, making debugging nearly impossible. This practice has been standard since Java 1.4 and remains essential in modern Java.

---

### Question 7: Explain the execution order when a try block has a return statement and there's a finally block.

**Answer**: When a try block contains a return statement, the JVM evaluates the return expression and saves its value, but does not immediately return to the caller. Instead, it executes the finally block first. After finally completes, the saved return value is returned. If the finally block also contains a return statement, it overwrites the try block's return value, which is why returning from finally is considered bad practice. Similarly, if an exception is thrown in try and finally also throws an exception, the finally exception suppresses the try exception, losing the original error. The order is: (1) evaluate return expression in try, (2) execute finally, (3) actually return. This behavior ensures cleanup code always runs and has been consistent since Java's inception, unchanged till Java 25.

---

### Question 8: What are the scenarios where the finally block does NOT execute?

**Answer**: The finally block is designed to always execute, but there are rare extreme scenarios where it doesn't: (1) If System.exit() is called, the JVM terminates immediately and finally doesn't run. (2) If the JVM crashes due to a fatal error or external signal. (3) If the thread executing the try-finally is killed abruptly. (4) If a daemon thread is running and all non-daemon threads complete, the JVM may exit before finally runs. (5) In theory, if an infinite loop occurs in try or catch, finally won't be reached. In normal application code, you can rely on finally executing for cleanup, but in edge cases involving JVM shutdown or thread termination, it may not run. These limitations are JVM-dependent and have remained unchanged till Java 25.

---

### Question 9: How do you properly handle resources before Java 7, and what changed in Java 7?

**Answer**: Before Java 7, you had to manually close resources in a finally block with verbose null checking: declare the resource as null outside try, initialize it inside try, and close it in finally with null checks and nested try-catch for close exceptions. This was error-prone and verbose. Java 7 introduced try-with-resources, which automatically closes any resource implementing AutoCloseable: `try (FileReader reader = new FileReader(file))` The resource is automatically closed at the end of the try block, even if exceptions occur. Multiple resources can be declared separated by semicolons. Java 9 further improved this by allowing effectively final variables to be referenced. This feature also properly handles suppressed exceptions when both the try block and close() throw exceptions. Try-with-resources is now the standard best practice and this feature has been stable and unchanged in core behavior till Java 25.

---

### Question 10: What is the performance impact of exceptions, and how should this influence your design?

**Answer**: Exception creation is expensive because the JVM must capture the entire call stack, walk through all frames, and create an array of StackTraceElement objects—this can be 100-1000x slower than normal method calls. Exception throwing also disrupts CPU pipeline and branch prediction. This performance cost means exceptions should only be used for truly exceptional conditions, not normal control flow. In hot paths (code executed millions of times), this overhead is significant. You should validate inputs and use conditional logic for expected cases rather than catching exceptions. For example, checking array bounds before access is much faster than catching ArrayIndexOutOfBoundsException. However, for rare error conditions, the cost is acceptable and the code clarity benefit outweighs the performance impact. Modern JVMs have optimized exception handling, but the fundamental cost of stack trace creation remains, and this has been true throughout Java's history, unchanged till Java 25.

---

### Question 11: Explain how to design a good custom exception class.

**Answer**: A well-designed custom exception should extend the appropriate parent class—Exception for checked exceptions or RuntimeException for unchecked exceptions—based on whether you want compile-time enforcement. Include at least three constructors: no-arg, message-only, and message-with-cause for exception chaining. Add relevant fields that provide context for debugging, such as user IDs, transaction IDs, or amounts. Follow the naming convention of ending with "Exception." Document when and why the exception is thrown using Javadoc. For example: `public class InsufficientBalanceException extends Exception` with fields for balance and withdrawal amount, plus constructors passing through to super(). Make fields accessible via getters. This design provides rich context for debugging while maintaining clean exception handling patterns. Custom exceptions should model your domain's error conditions clearly and these design principles have been best practices throughout Java's history.

---

### Question 12: In a multi-layered application, how should exceptions be handled across layers?

**Answer**: Exception handling in layered architecture requires careful design. At the data layer, catch specific technical exceptions like SQLException and wrap them in domain exceptions like DataAccessException, preserving the cause via exception chaining. This prevents implementation details from leaking to higher layers. At the service layer, handle business logic exceptions and either resolve them or propagate domain exceptions upward. At the controller/API layer, catch all unhandled exceptions and convert them to appropriate responses (HTTP status codes, error messages) while logging the full exception chain. Each layer should only catch exceptions it can meaningfully handle—don't catch just to rethrow without adding value. Use exception chaining to preserve root causes. Log once at the boundary where you can add the most context, avoiding duplicate logging. This separation of concerns keeps code maintainable and has been an architectural best practice in enterprise Java applications, with frameworks like Spring providing built-in support that has evolved but maintained these core principles till Java 25.