## MODULE 17: Exception Handling

---

##### MCQ 1 (Beginner)
##### What happens when an exception is thrown but not caught anywhere in the program?
##### A) The program continues execution normally  
##### B) The exception is automatically handled by the JVM  
##### C) The program terminates and prints the stack trace  
##### D) The program enters an infinite loop 
###### Answer: C) The program terminates and prints the stack trace  
###### Explanation: When an exception propagates through the entire call stack without being caught, the JVM terminates the program and prints the exception's stack trace to standard error, showing where the exception occurred and the call chain.

---

##### MCQ 2 (Beginner)
##### Which of these is a checked exception?
##### A) NullPointerException  
##### B) ArrayIndexOutOfBoundsException  
##### C) IOException  
##### D) ArithmeticException
###### Answer: C) IOException 
###### Explanation: IOException is a checked exception that extends Exception but not RuntimeException. The compiler forces you to handle it. Options A, B, and D are all unchecked exceptions extending RuntimeException, indicating programming errors rather than recoverable conditions.


---

##### MCQ 3 (Beginner)
##### What is the purpose of the finally block?
##### A) To catch exceptions  
##### B) To throw exceptions  
##### C) To execute code regardless of whether an exception occurred  
##### D) To declare checked exceptions
###### Answer: C) To execute code regardless of whether an exception occurred 
###### Explanation: The finally block is designed for cleanup code that must execute whether an exception occurs or not. It runs after try and catch blocks complete, making it ideal for closing resources like files or database connections.

---

##### MCQ 4 (Beginner)
##### Which exception indicates that an array index is out of bounds?
##### A) IndexOutOfBoundsException  
##### B) ArrayException  
##### C) ArrayIndexOutOfBoundsException  
##### D) OutOfBoundsException
###### Answer: C) ArrayIndexOutOfBoundsException  
###### Explanation: ArrayIndexOutOfBoundsException is the specific unchecked exception thrown when trying to access an array with an invalid index. It extends IndexOutOfBoundsException, which is a more general exception.

---

##### MCQ 5 (Beginner)
##### Can you catch an Error in Java?
##### A) No, it's illegal and causes a compilation error  
##### B) Yes, but it's generally not recommended  
##### C) Only if it's a checked Error  
##### D) Errors cannot be thrown
###### Answer: B) Yes, but it's generally not recommended  
###### Explanation: Technically you can catch Error (it's legal), but it's strongly discouraged. Errors represent serious problems like OutOfMemoryError or StackOverflowError that indicate the JVM is in an unstable state. Applications should generally let these propagate and terminate the program.

---

##### MCQ 6 (Intermediate)
##### What is the purpose of custom exceptions?
##### A) To avoid using Java's built-in exceptions  
##### B) To represent domain-specific errors and provide additional context  
##### C) To make code more complex  
##### D) They serve no purpose; built-in exceptions are sufficient
###### Answer: B) To represent domain-specific errors and provide additional context
###### Explanation: Custom exceptions allow you to model business logic errors specific to your application domain. They can carry additional fields for context, make exception handling more specific, and make your API's error conditions explicit and well-documented.

---

##### MCQ 7 (Intermediate)
##### What is the output of the following code?

```java
try {
    System.out.print("A");
    throw new RuntimeException();
} catch (RuntimeException e) {
    System.out.print("B");
} finally {
    System.out.print("C");
}
System.out.print("D");
```

##### A) ABCD  
##### B) ACD  
##### C) ABC  
##### D) AD 
###### Answer: A) ABCD 
###### Explanation: The try block prints "A" and throws an exception. The catch block catches it and prints "B". The finally block executes and prints "C". Then normal execution continues and prints "D". Output: ABCD.

---

##### MCQ 8 (Intermediate)
##### Which statement about catch blocks is TRUE?
##### A) You can place a general exception before a specific exception  
##### B) More specific exceptions must come before more general exceptions  
##### C) The order of catch blocks doesn't matter  
##### D) You can only have one catch block per try
###### Answer: B) More specific exceptions must come before more general exceptions
###### Explanation: The compiler enforces that specific exceptions must appear before general ones. If a general exception like Exception comes first, subsequent specific catch blocks would be unreachable, causing a compilation error. The JVM checks catch blocks in order from top to bottom.

---

##### MCQ 9 (Intermediate)
##### What is the difference between throw and throws?
##### A) There is no difference, they are interchangeable  
##### B) throw is used to throw an exception object; throws is used to declare exceptions in the method signature  
##### C) throw declares exceptions; throws throws exceptions  
##### D) throw is for checked exceptions; throws is for unchecked exceptions
###### Answer: B) throw is used to throw an exception object; throws is used to declare exceptions in the method signature  
###### Explanation: throw is a keyword used inside a method body to actually throw an exception object. throws is used in the method signature to declare that the method might throw certain checked exceptions, informing the compiler and callers.

---

##### MCQ 10 (Intermediate)
##### What happens if an exception is thrown in a catch block?
##### A) It's automatically caught by the same catch block  
##### B) It propagates to the outer try-catch or up the call stack  
##### C) The program terminates immediately  
##### D) It's ignored  
###### Answer: B) It propagates to the outer try-catch or up the call stack 
###### Explanation: An exception thrown in a catch block propagates just like any other exception. It looks for an outer try-catch block in the same method, and if not found, propagates up the call stack to the calling method.

---

##### MCQ 11 (Intermediate)
##### Which is NOT a valid reason to use checked exceptions?
##### A) The caller can reasonably recover from the condition  
##### B) The failure is an expected part of the operation  
##### C) It represents a programming error  
##### D) You're designing a library API and want to make failure modes explicit
###### Answer: C) It represents a programming error 
###### Explanation: Programming errors should be represented by unchecked exceptions (RuntimeException), not checked exceptions. Checked exceptions are for recoverable conditions that callers should explicitly handle, not bugs that should be fixed.

---

##### MCQ 12 (Advanced)
##### When does the finally block NOT execute?
##### A) When an exception is thrown  
##### B) When the try block completes normally  
##### C) When System.exit() is called  
##### D) When a catch block is executed
###### Answer: C) When System.exit() is called
###### Explanation: The finally block executes in almost all scenarios, but it does NOT execute if System.exit() is called, the JVM crashes, or the thread is abruptly terminated. These are the rare exceptions to the "finally always runs" rule, and this behavior is unchanged till Java 25.

---

##### MCQ 13 (Advanced)
##### What is the result of this code?

```java
public int test() {
    try {
        return 1;
    } finally {
        return 2;
    }
}
```

##### A) Returns 1  
##### B) Returns 2  
##### C) Compilation error  
##### D) Runtime exception 
###### Answer: B) Returns 2
###### Explanation: Although try has a return statement, the finally block executes before the method actually returns. Since finally also has a return statement, it overwrites the pending return value from try. The method returns 2. This is legal but considered bad practice.

---

##### MCQ 14 (Advanced)
##### In multi-catch (Java 7+), which statement is TRUE?

```java
catch (IOException | SQLException e) {
    // handle
}
```

##### A) IOException and SQLException can be in a subclass relationship  
##### B) The exceptions must not be in a subclass relationship  
##### C) The variable e can be reassigned  
##### D) You must handle them separately
###### Answer: B) The exceptions must not be in a subclass relationship
###### Explanation: Multi-catch requires that the exception types are not in a subclass relationship (no redundancy). Additionally, the variable is implicitly final and cannot be reassigned. This feature was introduced in Java 7 and remains unchanged till Java 25.

---

##### MCQ 15 (Advanced)
##### What is exception chaining?
##### A) Catching multiple exceptions in sequence  
##### B) Throwing one exception after another  
##### C) Wrapping an exception in a new exception while preserving the original as the cause  
##### D) Using multiple catch blocks
###### Answer: C) Wrapping an exception in a new exception while preserving the original as the cause 
###### Explanation: Exception chaining means wrapping a caught exception in a new exception while passing the original as the cause parameter. This preserves the full error context and stack trace, which is critical for debugging. Use getCause() to retrieve the original exception.

---