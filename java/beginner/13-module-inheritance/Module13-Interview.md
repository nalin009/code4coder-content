## MODULE 13: Inheritance

---
---

### Question 1: What is inheritance in Java, and why is it important?

**Answer:**  
Inheritance is an object-oriented programming mechanism that allows a class (child/subclass) to acquire properties and behaviors from another class (parent/superclass) using the `extends` keyword. It establishes an IS-A relationship and promotes code reusability, reducing redundancy. For example, if multiple classes share common attributes like `name` and `age`, we can define them in a parent class and inherit them, avoiding duplication. Inheritance also enables polymorphism, allowing objects to be treated as instances of their parent type. It's crucial for building scalable, maintainable codebases and is a foundational concept in framework design (e.g., Spring, Hibernate).

---

### Question 2: Explain the memory model when a child class object is created. How many objects are created in the heap?

**Answer:**  
When you create a child class object, **only one object** is created in the heap, not separate parent and child objects. This single object contains all non-private fields from the entire inheritance hierarchy (grandparent → parent → child). For example, if `Animal` has a field `species` and `Dog` extends `Animal` with field `breed`, creating `new Dog()` results in one object with both `species` and `breed`. The object's memory layout includes an object header (JVM metadata), followed by parent class fields, then child class fields, and a vtable pointer for method resolution. Private fields from the parent class exist in the object but are not directly accessible from the child class.

---

### Question 3: What is the difference between method overriding and method hiding?

**Answer:**  
**Method overriding** occurs with instance methods where a child class provides a specific implementation for a method inherited from the parent class. The method to call is determined at **runtime** based on the actual object type (dynamic method dispatch). For example, `Animal a = new Dog(); a.eat();` calls Dog's `eat()` method. **Method hiding** occurs with static methods where both parent and child have static methods with the same signature. Here, the method to call is determined at **compile time** based on the reference type, not the object type. For example, `Parent p = new Child(); p.staticMethod();` calls Parent's static method. The key difference is runtime vs compile-time resolution, driven by the fact that static methods belong to the class, not instances.

---

### Question 4: Why can't we call `super.super.method()` in Java?

**Answer:**  
Java does not allow `super.super.method()` because the `super` keyword only refers to the **immediate parent class**, not grandparents or further ancestors. This design decision maintains encapsulation and prevents tight coupling across multiple levels of inheritance. If you need to access grandparent functionality, the proper approach is to have the parent class expose that functionality through its own methods or to refactor the inheritance hierarchy. Allowing direct access to grandparent methods would violate encapsulation, making the code fragile and difficult to maintain. This restriction has been consistent throughout Java's evolution and remains unchanged till Java 25.

---

### Question 5: What happens during constructor chaining, and why is the parent constructor called first?

**Answer:**  
Constructor chaining is the process where constructors in the inheritance hierarchy are invoked in sequence from top (parent) to bottom (child) when a child object is created. The parent constructor is called first because the parent class must be fully initialized before the child class can safely use inherited members. Java automatically inserts `super()` as the first statement in the child constructor if not explicitly called. For example, creating `new Dog()` first executes `Animal()` constructor, then `Dog()` constructor. This ensures proper initialization order: object header allocation → parent fields initialization → child fields initialization. If the parent has only parameterized constructors, the child **must** explicitly call `super(args)`.

---

### Question 6: When would you prefer composition over inheritance in real-world applications?

**Answer:**  
Composition (HAS-A) should be preferred over inheritance (IS-A) when the relationship is not a true specialization or when you need flexibility and loose coupling. For example, a `Car` should not inherit from `Engine`; instead, it should **have an** Engine as a member variable. Composition is better when you need to change behavior at runtime, want to avoid deep inheritance hierarchies, or need multiple "parent-like" behaviors (since Java doesn't support multiple inheritance for classes). Real-world example: In Spring Framework, dependency injection uses composition extensively. A `UserService` has a `UserRepository` (composition), rather than extending it (inheritance), allowing easy swapping of implementations and better testability. The principle "favor composition over inheritance" is a cornerstone of modern Java design.

---

### Question 7: What are the rules for method overriding in Java?

**Answer:**  
Method overriding must follow these rules: (1) The method signature (name and parameters) must match exactly. (2) The return type must be the same or a **covariant return type** (subclass of parent's return type). (3) The access modifier cannot be more restrictive (e.g., parent's `public` cannot become child's `protected`). (4) For checked exceptions, the child can throw same, subclass, or no exception, but not broader exceptions. (5) Static methods cannot be overridden (they are hidden). (6) Final and private methods cannot be overridden. (7) The `@Override` annotation is optional but recommended for compile-time verification. These rules ensure that a child object can always substitute for its parent (Liskov Substitution Principle), maintaining polymorphic behavior safely.

---

### Question 8: How does the JVM resolve which method to call at runtime (dynamic method dispatch)?

**Answer:**  
The JVM uses a **vtable (virtual method table)** stored in Metaspace to resolve method calls at runtime. Each class has its own vtable containing pointers to method implementations. When an object is created, it has a pointer to its class's vtable. At runtime, when a method is invoked, the JVM follows this pointer to the vtable and looks up the method's entry. If the child class overrode the method, the vtable entry points to the child's implementation; otherwise, it points to the parent's. This mechanism enables **O(1) method lookup** regardless of inheritance depth. For example, `Animal a = new Dog(); a.eat();` compiles against Animal's interface but at runtime uses Dog's vtable to call Dog's `eat()` method. This is the foundation of polymorphism in Java.

---

### Question 9: What is the diamond problem, and how does Java avoid it?

**Answer:**  
The diamond problem occurs in multiple inheritance when two parent classes inherit from a common grandparent and both override the same method, causing ambiguity about which version the child should inherit. Java avoids this for classes by supporting **only single inheritance**—a class can extend only one parent class. However, Java allows multiple inheritance for **interfaces**. Since Java 8, interfaces can have default methods, potentially reintroducing the diamond problem. Java resolves this by requiring the implementing class to **explicitly override** the conflicting method if two interfaces provide the same default method. For example, if `Flyable` and `Swimmable` both have `default void move()`, a class implementing both must provide its own `move()` implementation, eliminating ambiguity.

---

### Question 10: Explain the difference between `super()` and `this()` in constructors.

**Answer:**  
`super()` calls the parent class constructor and must be the first statement in the child constructor, establishing constructor chaining up the inheritance hierarchy. It's used to initialize inherited fields or invoke parent class setup logic. `this()` calls another constructor in the **same class** (constructor overloading), enabling constructor delegation within one class. Both must be the first statement, so you **cannot use both** in the same constructor. For example, if a class has multiple constructors, `this(args)` can delegate to a primary constructor, which then calls `super(args)`. If neither `super()` nor `this()` is explicitly called, Java implicitly inserts `super()`, calling the parent's no-arg constructor. If the parent doesn't have a no-arg constructor, you **must** explicitly call `super(args)`.

---

### Question 11: Why is the String class declared as final in Java?

**Answer:**  
The `String` class is final to ensure **immutability** and **security**. Making it final prevents subclassing, which could otherwise compromise immutability (a subclass could add mutable behavior). String immutability enables critical optimizations like string interning (reusing identical strings in the string pool), making string operations memory-efficient and thread-safe without synchronization. Additionally, strings are used in security-sensitive contexts like class loading, file paths, and database queries. If String could be extended, malicious code could override methods to alter behavior, creating security vulnerabilities. By making String final, Java guarantees consistent, predictable behavior across the entire platform. This design has been fundamental since Java 1.0 and remains unchanged till Java 25.

---

### Question 12: What are sealed classes, and how do they improve inheritance design? (Java 17+)

**Answer:**  
Sealed classes (introduced in Java 17) restrict which classes can extend them using the `sealed`, `permits`, and `final`/`non-sealed` keywords. For example, `sealed class Shape permits Circle, Rectangle, Triangle` means only those three classes can extend Shape, and each must be declared as `final`, `sealed`, or `non-sealed`. This provides **explicit control** over inheritance hierarchies, preventing unexpected subclasses. Benefits include: (1) **Better design clarity** by documenting extension points. (2) **Improved pattern matching** (Java 21+) where the compiler knows all possible subtypes. (3) **Domain modeling** where a finite set of subclasses is meaningful (e.g., payment types, HTTP methods). Sealed classes offer a middle ground between open inheritance (anyone can extend) and final classes (no one can extend), giving architects precise control. This feature has been stable and unchanged till Java 25.

### Question 13: Explain the difference between IS-A and HAS-A relationships with code examples. When would you choose one over the other?

**Answer:**  
**IS-A relationship** represents inheritance where a subclass is a specialized version of the superclass (e.g., `Dog IS-A Animal`). It's implemented using the `extends` keyword and enables code reuse through polymorphism. **HAS-A relationship** represents composition where one class contains a reference to another class as a member variable (e.g., `Car HAS-A Engine`). The key decision factor is: use IS-A when there's true specialization and you need polymorphic behavior (substitutability); use HAS-A when you need flexible object relationships, loose coupling, or when multiple "parent-like" behaviors are needed. For example, `Stack extends ArrayList` is a design flaw (Stack has different semantics), whereas `Stack HAS-A List` properly encapsulates the underlying storage. Modern Java development heavily favors composition because it provides runtime flexibility, easier testing (dependency injection), and avoids fragile base class problems.

---

### Question 14: What happens in memory when you create an object of a child class? Walk through the entire process from JVM perspective.

**Answer:**  
When executing `Dog myDog = new Dog()`, the JVM performs: (1) **Memory Allocation**: JVM allocates contiguous memory in the heap for ONE object containing space for object header (mark word, class pointer), parent class fields (Animal's fields), child class fields (Dog's fields), and padding for alignment. (2) **Constructor Chaining Initiation**: JVM invokes Dog's constructor. (3) **Implicit super() Call**: Java compiler inserted `super()` as first statement, so Animal's constructor is called. (4) **Recursive Parent Chain**: Animal's constructor calls `super()` reaching Object's constructor. (5) **Bottom-Up Execution**: Object() executes first (initializes object header), then Animal() executes (initializes Animal fields), finally Dog() executes (initializes Dog fields). (6) **Vtable Setup**: Object's class pointer is set to point to Dog's vtable in Metaspace. (7) **Reference Assignment**: Stack variable `myDog` receives the heap address. Critical insight: There's ONE object, not separate parent/child objects, enabling efficient polymorphism through vtable-based method dispatch.

---

### Question 15: How does the JVM optimize method calls in inheritance hierarchies? What is method inlining and when does it happen?

**Answer:**  
The JVM uses several optimization techniques: (1) **Vtable Indexing**: For virtual (overridable) methods, the JVM uses the vtable for O(1) lookup regardless of hierarchy depth. Each method has a fixed vtable index, making lookups constant time. (2) **Method Inlining**: The JIT compiler inlines frequently-called methods (especially small methods) directly into the caller's bytecode, eliminating method call overhead entirely. This works best for `final` methods (non-overridable) and methods in `final` classes. (3) **Monomorphic Call Sites**: If a call site consistently calls the same implementation (e.g., always calls Dog.eat() and never Cat.eat()), the JVM inlines it speculatively with a guard check. (4) **Devirtualization**: If the JVM proves through escape analysis that an object's type cannot change, it converts virtual calls to direct calls. For deep inheritance (5+ levels), the overhead is still negligible—real performance issues come from cache misses due to large object sizes, not method dispatch. Modern JVMs (HotSpot, GraalVM) are highly optimized, making premature optimization of inheritance hierarchies counterproductive.

---

### Question 16: Explain constructor chaining in detail. What happens if the parent class only has a parameterized constructor?

**Answer:**  
Constructor chaining is the mechanism ensuring all constructors in the inheritance hierarchy are invoked in top-down order (parent first) during object creation. When you create a child object, Java implicitly inserts `super()` as the first statement in the child constructor if not explicitly provided. The chain continues recursively until reaching Object's constructor. Execution happens bottom-up: Object → GrandParent → Parent → Child. If the parent class ONLY has parameterized constructors (no no-arg constructor), the child class MUST explicitly call `super(args)` with appropriate arguments as the first statement—otherwise, compilation fails with "implicit super constructor is undefined". This design ensures proper initialization order where parent state is fully set up before child code runs. The `super()` or `this()` call must be first because allowing other code first could try accessing uninitialized parent state, causing undefined behavior. You cannot call both `super()` and `this()` in the same constructor—they're mutually exclusive because each must be first statement.

---

### Question 17: What is the fragile base class problem, and how can you prevent it?

**Answer:**  
The fragile base class problem occurs when changes to a parent class break child classes unexpectedly, even when the parent's public API hasn't changed. This happens because child classes depend on parent's implementation details, not just its interface. Example: if a parent class's method A() internally calls method B(), and a child overrides B() assuming it's only called externally, updating parent's A() to stop calling B() breaks the child's assumptions. Prevention strategies: (1) **Design for Inheritance or Prohibit It**: Document which methods are safe to override (using `@implSpec` JavaDoc tag) or make the class `final`. (2) **Use Template Method Pattern**: Make public methods `final` that orchestrate behavior, allowing overriding only of specific `protected abstract` "hook" methods. (3) **Favor Composition**: Use composition instead of inheritance when possible, avoiding the problem entirely. (4) **Document Internal Calls**: If a public method calls another overridable method internally, document this clearly. (5) **Package-Private Implementation**: Keep implementation details package-private so external subclasses can't depend on them. This problem is why frameworks like Spring often use composition and interfaces rather than deep inheritance hierarchies.

---

### Question 18: How do sealed classes (Java 17+) improve inheritance design? Provide a real-world use case.

**Answer:**  
Sealed classes provide explicit control over inheritance hierarchies using the `sealed`, `permits`, and `final`/`non-sealed` keywords. They allow you to restrict which classes can extend a parent, creating a closed set of known subclasses. Real-world use case: **Payment Method Hierarchy** in an e-commerce system: `sealed class PaymentMethod permits CreditCard, DebitCard, UPI, NetBanking`. Benefits: (1) **Domain Modeling**: Represents finite sets naturally (payment types, HTTP methods, order statuses). (2) **Exhaustiveness Checking**: With pattern matching (Java 21+), the compiler ensures you've handled all possible subtypes in switch expressions. (3) **Security**: Prevents external code from creating unexpected subtypes that might bypass validation. (4) **Performance**: JVM can optimize more aggressively knowing the complete type hierarchy at compile time. (5) **Documentation**: Makes design intent explicit—readers know this is a closed hierarchy. Implementation: `sealed class PaymentMethod permits ... { }`, then each permitted class must be `final`, `sealed`, or `non-sealed`. Sealed classes bridge the gap between fully open inheritance (anyone can extend) and final classes (no one can extend), providing precise architectural control. Status: Stable since Java 17, unchanged till Java 25.

---

### Question 19: Compare inheritance in Java vs C++. What are the key differences?

**Answer:**  
Key differences: (1) **Multiple Inheritance**: Java supports single inheritance for classes (avoiding diamond problem) but multiple inheritance for interfaces. C++ supports multiple inheritance for classes, requiring complex resolution rules. (2) **Virtual Methods**: In Java, all non-static, non-final, non-private methods are virtual by default (overridable). In C++, methods must be explicitly declared `virtual`. (3) **Object Slicing**: C++ has object slicing when passing derived objects by value to base class parameters—the derived part is "sliced off". Java doesn't have this problem because objects are always accessed via references. (4) **Constructor Chaining**: Java automatically chains constructors with implicit `super()`. C++ requires explicit base class initialization in the member initializer list. (5) **Abstract Classes**: Java uses `abstract` keyword; C++ uses pure virtual functions (`virtual void func() = 0`). (6) **Access Control**: Java has `protected` meaning same package OR subclasses; C++ `protected` means only subclasses. (7) **Memory Management**: Java's automatic GC handles object lifetimes; C++ requires manual destruction considerations with virtual destructors for polymorphic classes. Java's simpler inheritance model (single inheritance + interfaces) avoids many C++ pitfalls while maintaining most benefits through composition and interface-based design.

---

### Question 20: In a production system, you have a deep inheritance hierarchy (7 levels) causing maintenance issues. How would you refactor it?

**Answer:**  
Refactoring approach: (1) **Identify Core Abstractions**: Analyze what each level adds—often you'll find levels that don't add meaningful specialization, just incremental fields. (2) **Extract Interfaces**: Convert behavior-defining levels into interfaces. If Level 3 adds "Flyable" behavior, make it an `interface Flyable` instead. (3) **Favor Composition**: Replace "HAS-A disguised as IS-A" relationships with actual composition. If Level 5 adds database functionality, inject a `DatabaseService` dependency instead. (4) **Flatten the Hierarchy**: Merge levels that only add fields/minor behavior into a single class using builder pattern for complex construction. Target: 2-3 levels maximum. (5) **Use Strategy Pattern**: If multiple levels represent algorithmic variations, extract algorithms into separate strategy classes. (6) **Apply Template Method**: Keep one abstract base with `final` template methods calling `protected abstract` hooks that subclasses implement. (7) **Introduce Polymorphism via Interfaces**: Replace type checks (`instanceof`) with interface-based polymorphism. Real example: Legacy framework had `BaseServlet → AbstractHttpServlet → GenericServlet → SpecificServlet → ProjectServlet → FeatureServlet → MyServlet`. Refactored to: `Servlet` (interface) ← `MyServlet implements Servlet` + injected dependencies (RequestHandler, ResponseBuilder, Security Service). Result: From 7 levels to 1 class + interfaces, reducing coupling, improving testability, and enabling runtime behavior composition. Key principle: **Inheritance is not for code reuse—composition is**.