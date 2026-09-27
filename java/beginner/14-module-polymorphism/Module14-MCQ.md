## MODULE 14: Polymorphism with Compile-Time vs Runtime Binding

---

##### MCQ 1 (Beginner)
##### What is the primary difference between method overloading and method overriding in Java?
##### A) Overloading occurs at runtime, overriding at compile time
##### B) Overloading requires inheritance, overriding does not
##### C) Overloading has different parameters, overriding has the same signature
##### D) Overloading uses dynamic binding, overriding uses static binding
###### Answer: C) Overloading has different parameters, overriding has the same signature
###### Explanation: Method overloading occurs within the same class with different parameter lists and is resolved at compile time (static binding). Method overriding occurs in a child class with the exact same method signature as the parent and is resolved at runtime (dynamic binding). Option C correctly captures this distinction.

---

##### MCQ 2 (Beginner)
##### Which of the following is NOT a valid method overloading in Java?
##### A) void print(int x) and void print(double x)
##### B) void print(int x) and void print(int x, int y)
##### C) void print(int x) and int print(int x)
##### D) void print(String s) and void print(Object o)
###### Answer: C) void print(int x) and int print(int x)
###### Explanation: Return type alone cannot distinguish overloaded methods. Options A, B, and D have different parameter lists (different types, different number of parameters, or different parameter types), which make them valid overloading. Option C only differs in return type, making it invalid overloading and causing a compilation error.

---

##### MCQ 3 (Beginner)
##### What does the instanceof operator return when checking a null reference?
##### A) Throws NullPointerException
##### B) Returns true
##### C) Returns false
##### D) Compilation error
###### Answer: C) Returns false
###### Explanation: The instanceof operator is null-safe and returns false when the object reference is null, without throwing any exception. This is by design to allow safe type checking. The code (null instanceof AnyType) always returns false.

---

##### MCQ 4 (Beginner)
##### In method overloading, which of the following can vary?
##### A) Only the number of parameters
##### B) Only the types of parameters
##### C) Only the return type
##### D) The number, type, or order of parameters
###### Answer: D) The number, type, or order of parameters
###### Explanation: Method overloading is determined by the method signature, which includes the method name and parameter list. The parameter list can vary in the number of parameters, the types of parameters, or the order of parameters. Return type alone does not contribute to overloading and cannot be the only difference.

---

##### MCQ 5 Intermediate)
##### Pattern matching with instanceof (Java 16+) allows you to:
##### A) Skip the need for casting after the check
##### B) Check multiple types simultaneously
##### C) Modify the original object's type
##### D) Avoid using inheritance
###### Answer: A) Skip the need for casting after the check
###### Explanation: Pattern matching with instanceof (introduced in Java 16 and enhanced further) allows automatic casting within the scope where the check is true, eliminating redundant explicit casting. Example: if (obj instanceof String s) { /* use s directly */ }.

---

##### MCQ 6 (Intermediate)
##### In the following code, which version of the process method will be called?

```java
class Test {
    void process(Object o) { System.out.println("Object"); }
    void process(String s) { System.out.println("String"); }
}
Test t = new Test();
t.process(null);
```

##### A) Object version
##### B) String version
##### C) Compilation error
##### D) Runtime error
###### Answer: C) Compilation error
###### Explanation: This results in a compilation error due to ambiguity. Both Object and String are reference types that can accept null, and neither is more specific than the other from the compiler's perspective when the argument is null. The compiler cannot decide which method to call, resulting in an "ambiguous method call" error.

---

##### MCQ 7 (Intermediate)
##### What is the output of the following code?

```java
class Animal {
    public static void makeSound() { System.out.println("Animal"); }
}
class Dog extends Animal {
    public static void makeSound() { System.out.println("Dog"); }
}
Animal a = new Dog();
a.makeSound();
```

##### A) Animal
##### B) Dog
##### C) Compilation error
##### D) Runtime error
###### Answer: A) Animal
###### Explanation: Static methods are not overridden; they are hidden. The method called is determined by the reference type (Animal) at compile time, not the object type (Dog) at runtime. This is method hiding, not polymorphism. The output is "Animal".

---

##### MCQ 8 (Intermediate)
##### Which statement about covariant return types is TRUE?
##### A) Covariant return types are not supported in Java
##### B) A child class can return any type when overriding a method
##### C) A child class can return a subtype of the parent method's return type
##### D) Covariant return types only work with primitive types
###### Answer: C) A child class can return a subtype of the parent method's return type
###### Explanation: Since Java 5, covariant return types are supported, allowing an overriding method in a child class to return a subtype (more specific type) of the return type declared in the parent class. For example, if the parent returns Number, the child can return Integer. This does not work with primitive types (only reference types).

---

##### MCQ 9 (Intermediate)
##### What is dynamic method dispatch in Java?
##### A) The compiler selecting methods based on parameters
##### B) The JVM calling overridden methods based on actual object type at runtime
##### C) The process of method overloading
##### D) The mechanism for calling static methods
###### Answer: B) The JVM calling overridden methods based on actual object type at runtime
###### Explanation: Dynamic method dispatch is the mechanism by which the JVM resolves calls to overridden methods at runtime based on the actual object type in the heap, not the reference type. This is the foundation of runtime polymorphism and uses the vtable (virtual method table) for method lookup.

---

##### MCQ 10 (Intermediate)
##### What happens when a child class method has a more restrictive access modifier than the parent method it attempts to override?
##### A) The program runs with a warning
##### B) Compilation error occurs
##### C) The parent method is called instead
##### D) Runtime exception is thrown
###### Answer: B) Compilation error occurs
###### Explanation: If a child class attempts to override a parent method with a more restrictive access modifier (e.g., parent is public, child is private), it violates Java's overriding rules and results in a compilation error. The override must be equally or less restrictive to maintain the Liskov Substitution Principle.

---

##### MCQ 11 (Advanced)
##### Consider the following code. What is the output?

```java
class Parent {
    void display() { System.out.println("Parent"); }
}
class Child extends Parent {
    void display() { System.out.println("Child"); }
}
Parent p = new Child();
((Parent) p).display();
```

##### A) Parent
##### B) Child
##### C) Compilation error
##### D) ClassCastException
###### Answer: B) Child
###### Explanation: Casting the reference to Parent ((Parent) p) does not change the actual object type, which is still Child. Method overriding is resolved at runtime based on the actual object type (Child), not the reference type. The JVM uses dynamic dispatch to call Child's display() method. Output is "Child".

---

##### MCQ 12 (Advanced)
##### Which of the following rules applies when overriding a method in Java?
##### A) The overriding method can throw any exception
##### B) The overriding method must have the same return type
##### C) The overriding method cannot have a less restrictive access modifier
##### D) The overriding method cannot throw new or broader checked exceptions than the parent
###### Answer: D) The overriding method cannot throw new or broader checked exceptions than the parent
###### Explanation: When overriding, the child method cannot throw new or broader checked exceptions than the parent method, though it can throw fewer, narrower, or unchecked exceptions. Option B is incorrect because covariant return types are allowed. Option C is incorrect because the override can have less restrictive access. Option A is incorrect due to the exception restrictions.

---

##### MCQ 13 (Advanced)
##### What is stored in the vtable (virtual method table) in Java?
##### A) Instance variables of the class
##### B) Static methods and variables
##### C) References to virtual (non-static, non-final, non-private) methods
##### D) Object instances
###### Answer: C) References to virtual (non-static, non-final, non-private) methods
###### Explanation: The vtable is a data structure in Metaspace that stores pointers/references to all virtual methods of a class. Virtual methods are those that can be overridden: non-static, non-final, and non-private methods. The vtable is used by the JVM during dynamic method dispatch to find the correct method implementation at runtime.


---

##### MCQ 14 (Advanced)
##### In the method resolution priority for overloading, which comes first?
##### A) Varargs matching
##### B) Autoboxing/Unboxing
##### C) Exact type match
##### D) Widening primitive conversion
###### Answer: C) Exact type match
###### Explanation: The compiler follows a specific priority: (1) Exact type match, (2) Widening primitive conversion, (3) Autoboxing/Unboxing, (4) Widening reference conversion, (5) Varargs. If an exact match is found, the compiler selects it immediately without checking other options.

---

##### MCQ 15 (Advanced - JVM Behavior)
##### Which JVM bytecode instruction is used for dynamic method dispatch?
##### A) invokespecial
##### B) invokestatic
##### C) invokevirtual
##### D) invokedynamic
###### Answer: C) invokevirtual
###### Explanation: The invokevirtual instruction is used by the JVM for dynamic method dispatch on instance methods. It performs vtable lookup to find the correct method implementation based on the actual object type at runtime. invokespecial is for constructors and private methods, invokestatic for static methods, and invokedynamic for lambda expressions and method handles.

---

##### MCQ 16 (Advanced - Production Scenario)
##### You are reviewing a payment processing system where payments sometimes fail unexpectedly. The code looks like this:

```java
class PaymentProcessor {
    public void processPayment(Payment payment) {
        validatePayment(payment);
        deductAmount(payment);
    }
    
    protected void validatePayment(Payment payment) {
        // Base validation
    }
}

class EnhancedPaymentProcessor extends PaymentProcessor {
    @Override
    protected void validatePayment(Payment payment) {
        super.validatePayment(payment);
        // Additional fraud checks
    }
}
```

A colleague instantiates it as: PaymentProcessor processor = new EnhancedPaymentProcessor();
Which method's validation will execute?

##### A) Only PaymentProcessor's validation
##### B) Only EnhancedPaymentProcessor's validation
##### C) First PaymentProcessor, then EnhancedPaymentProcessor
##### D) Compile error - method overriding not allowed
###### Answer: C) First PaymentProcessor, then EnhancedPaymentProcessor
###### Explanation: The EnhancedPaymentProcessor's validatePayment() calls super.validatePayment() first, then adds additional checks. Due to dynamic method dispatch, when processPayment() calls validatePayment(), it executes the EnhancedPaymentProcessor version (runtime polymorphism), which in turn calls the parent version via super. This is the Template Method pattern in action, ensuring base validation always happens plus any additional validation in subclasses.

Production Insight: This pattern is common in frameworks where base classes provide essential functionality and subclasses enhance it. Always check if super is called when debugging unexpected behavior.

---

##### MCQ 17 (Advanced - JVM Internals)
#####  A senior engineer claims: "Using interfaces instead of abstract classes hurts performance because of polymorphic dispatch overhead."
Is this statement correct?

##### A) Yes, interfaces are slower than abstract classes
##### B) No, both use the same vtable mechanism
##### C) Yes, interfaces require invokeinterface bytecode which is slower
##### D) No, modern JVMs optimize both identically after warmup
###### Answer: D) No, modern JVMs optimize both identically after warmup
###### Explanation: While it's true that historically invokeinterface bytecode had slight overhead compared to invokevirtual, modern JVMs (HotSpot, GraalVM) optimize both identically after JIT compilation and warmup. The JIT compiler performs inline caching and devirtualization regardless of whether the polymorphism comes from an interface or abstract class. After warmup, both have virtually identical performance. Design decisions should be based on API design needs, not performance myths.
Production Insight: Profile before optimizing. In a microservice handling 1000 req/sec, network and database latency (50-200ms) dwarf any polymorphic dispatch overhead (0.0003ms).

---

##### MCQ 18 (Expert - Design Decision)
##### You're designing a plugin system for an IDE. Which approach provides the best balance of flexibility and safety?

```java
// Option A
interface Plugin {
    void execute();
}

// Option B
abstract class Plugin {
    public final void execute() {
        initialize();
        doExecute();
        cleanup();
    }
    protected abstract void initialize();
    protected abstract void doExecute();
    protected abstract void cleanup();
}

// Option C
abstract class Plugin {
    public void execute() {
        doExecute();
    }
    protected abstract void doExecute();
}

// Option D
class Plugin {
    public void execute() { }
}
```

##### A) Option A - Maximum flexibility
##### B) Option B - Template Method with guaranteed lifecycle
##### C) Option C - Balance of flexibility and structure
##### D) Option D - Most performant (no polymorphism)
###### Answer: B) Option B - Template Method with guaranteed lifecycle
###### Explanation: Option B uses the Template Method pattern with a final execute() method that enforces a mandatory lifecycle (initialize → execute → cleanup). This prevents plugin developers from forgetting critical setup/teardown steps, which is essential for system stability. Option A offers flexibility but no safety guarantees. Option C is better than A but doesn't enforce lifecycle. Option D eliminates polymorphism entirely, defeating the purpose of a plugin system.
Production Insight: IntelliJ IDEA, VS Code, and Eclipse all use Template Method patterns for plugin lifecycles to prevent resource leaks and ensure proper initialization/cleanup. Flexibility without safety leads to production bugs.

---