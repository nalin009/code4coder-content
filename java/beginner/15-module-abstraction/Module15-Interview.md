## Module 15: Abstraction

---
---

Question 1: What is abstraction, and why is it important in object-oriented programming?
Answer:
Abstraction is an OOP principle that hides implementation complexity and exposes only essential features to the user. It allows developers to focus on what an object does rather than how it does it, promoting code modularity, reusability, and maintainability. Abstraction enables different implementations of the same contract, supporting polymorphism and making systems more flexible and easier to extend. For example, a PaymentProcessor interface defines processPayment(), but implementations like CreditCardProcessor and PayPalProcessor handle the details differently.

Question 2: What is the difference between an abstract class and an interface? When would you use each?
Answer:
An abstract class provides partial abstraction with shared implementation (state, constructors, concrete methods) and supports single inheritance, making it suitable for IS-A relationships where subclasses share common behavior. An interface provides a contract (traditionally complete abstraction) with no state, supports multiple inheritance, and is ideal for defining capabilities (CAN-DO relationships) across unrelated classes. Use abstract classes when you need shared code among related classes (e.g., Vehicle with common fields). Use interfaces when defining behaviors that unrelated classes can implement (e.g., Flyable for Bird and Airplane).

Question 3: Can an abstract class have a constructor? If yes, what is its purpose?
Answer:
Yes, abstract classes can have constructors. The constructor is used to initialize fields common to all subclasses and is invoked via super() when a concrete subclass object is created. Since abstract classes cannot be instantiated directly, the constructor ensures that shared state is properly initialized before the subclass-specific initialization occurs. For example, an abstract Animal class might have a constructor to set the name field, which every subclass (e.g., Dog, Cat) needs.

Question 4: Explain the diamond problem in Java and how Java resolves it in the context of interfaces with default methods.
Answer:
The diamond problem occurs when a class implements multiple interfaces that have the same default method signature, creating ambiguity about which implementation to use. Java resolves this by requiring the implementing class to explicitly override the conflicting method. Within this override, the class can choose which interface's default method to call using InterfaceName.super.methodName() syntax, or provide a completely new implementation. This explicit resolution prevents ambiguity and gives the developer control over the behavior.

Question 5: What are default methods in interfaces? Why were they introduced in Java 8?
Answer:
Default methods are concrete methods in interfaces (introduced in Java 8) that provide a default implementation using the default keyword. They were introduced to solve the backward compatibility problem: when adding new methods to existing interfaces (like Collection.forEach()), all existing implementations would break. Default methods allow interfaces to evolve without breaking existing code, as classes implementing the interface automatically inherit the default implementation. If needed, classes can override the default method to provide custom behavior.

Question 6: Can you have private methods in an interface? If yes, when were they introduced and why?
Answer:
Yes, private methods in interfaces were introduced in Java 9. They allow code reuse within default and static methods without exposing helper methods to implementing classes. Private methods prevent code duplication when multiple default methods share common logic. For example, if two default methods need to perform logging, a private method can contain the logging logic, keeping the interface clean and maintainable. Private methods can be either instance methods (used by default methods) or static methods (used by static methods).

Question 7: What is a functional interface? How does it relate to lambda expressions?
Answer:
A functional interface is an interface with exactly one abstract method (SAM - Single Abstract Method), optionally annotated with @FunctionalInterface for compile-time verification. Functional interfaces enable lambda expressions and method references, as the single abstract method provides a clear target for the lambda. Examples include Runnable, Callable, and Comparator. Lambda expressions provide concise syntax for implementing functional interfaces: Runnable r = () -> System.out.println("Running");. Functional interfaces are the foundation of Java's functional programming features introduced in Java 8.

Question 8: Explain the concept of marker interfaces with examples. How do they differ from regular interfaces?
Answer:
Marker interfaces are empty interfaces with no methods, used to signal special behavior or capabilities to the JVM or frameworks. Examples include Serializable (enables object serialization), Cloneable (allows cloning via Object.clone()), and Remote (marks objects for RMI). Unlike regular interfaces that define contracts with methods, marker interfaces serve as metadata or tags. The JVM or frameworks check for marker interfaces using instanceof and apply special treatment. Modern practice often replaces marker interfaces with annotations (e.g., @Deprecated), but marker interfaces remain for legacy reasons.

Question 9: What happens at the JVM level when you call a method on an abstract class reference pointing to a concrete subclass object?
Answer:
At the JVM level, method invocation uses dynamic dispatch via the virtual method table (vtable). When an abstract class reference points to a concrete subclass object, the JVM looks at the object's actual runtime type (the subclass), follows the vtable pointer in the object header, and finds the appropriate method implementation entry. For abstract methods, the vtable entry points to the subclass's implementation. The invokevirtual bytecode instruction is used for this dispatch. This mechanism enables polymorphism and is unchanged through Java 25.

Question 10: Can an interface extend multiple interfaces? Provide an example and explain the implications.
Answer:
Yes, an interface can extend multiple interfaces using the extends keyword, enabling interface inheritance. For example, interface ReadWritable extends Readable, Writable { } inherits all methods from both parent interfaces. Implementing classes must provide implementations for all inherited abstract methods from all parent interfaces. This creates a combined contract. If parent interfaces have conflicting default methods with the same signature, the child interface must either override the method or cause a compile error when a class implements it without resolution.

Question 11: Describe a real-world scenario where you would prefer an abstract class over an interface.
Answer:
I would use an abstract class when designing a framework where multiple related classes share significant common implementation. For example, in a document processing system, an abstract class DocumentProcessor might have concrete methods for loadDocument(), validateFormat(), and fields like fileName and fileSize, while leaving parseContent() abstract. Concrete subclasses like PDFProcessor, WordProcessor, and ExcelProcessor inherit the common logic and only implement document-specific parsing. This avoids code duplication while maintaining a clear IS-A relationship. An interface wouldn't be ideal here because it cannot hold state or provide shared implementation (beyond default methods).

Question 12: How does the introduction of default methods in Java 8 blur the distinction between abstract classes and interfaces? How do you decide between them now?
Answer:
Default methods allow interfaces to provide concrete implementations, which was previously exclusive to abstract classes. This makes interfaces more powerful and reduces the clear separation between the two. However, key differences remain: abstract classes can have state (instance variables), constructors, and any access modifiers, while interfaces cannot. When deciding, consider: use abstract classes for IS-A relationships with shared state and implementation; use interfaces for CAN-DO capabilities, multiple inheritance needs, or when no state is required. The decision now depends more on design intent and flexibility requirements than technical limitations.