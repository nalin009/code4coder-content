## MODULE 12: Encapsulation

---
---

Q1: What is encapsulation and why is it important in Java?
Answer:
Encapsulation is the OOP principle of bundling data (fields) and behavior (methods) within a class while restricting direct access to internal state using access modifiers. It is important because it maintains data integrity by enforcing validation, hides implementation details enabling code evolution without breaking clients, reduces coupling between components, and provides a clear contract for how objects should be used. Encapsulation is fundamental to building maintainable, testable, and secure software systems.

Q2: Explain the difference between private, default, protected, and public access modifiers with examples.
Answer:
Private members are accessible only within the same class. Default (package-private) members are accessible within the same package only—Java has no nested package concept, so com.example and com.example.util are separate. Protected members are accessible within the same package and by subclasses in different packages, but only through the subclass type. Public members are accessible everywhere without restriction. For example, a private double balance in a BankAccount class can only be accessed via methods within BankAccount, ensuring validation and preventing external manipulation.

Q3: How can reflection bypass encapsulation, and what are the implications?
Answer:
Reflection can bypass encapsulation using setAccessible(true) on Field, Method, or Constructor objects, suppressing access control checks at runtime. This allows frameworks like Spring and Hibernate to inject dependencies or map database rows to private fields without public setters. The implications are that reflection should be used judiciously—it's powerful for frameworks but dangerous in regular application code because it breaks compile-time safety, reduces maintainability, and can violate class invariants. Modern module systems (JPMS) require explicit opens directives to allow deep reflection across module boundaries.

Q4: What is defensive copying and when should you use it?
Answer:
Defensive copying is the practice of creating a new copy of mutable objects when passing them into or out of a class, preventing external code from modifying internal state. You should use it when your class stores references to mutable objects like arrays, Date, or collections. For example, in a constructor accepting an int[] parameter, use Arrays.copyOf() to store a copy rather than the original reference. In getters, return a copy or an unmodifiable view to prevent external modification. This is critical for maintaining encapsulation and class invariants.

Q5: How does the Java Platform Module System (JPMS) enhance encapsulation?
Answer:
JPMS (introduced in Java 9) enhances encapsulation by adding strong encapsulation at the module level. A module explicitly declares which packages are accessible to other modules using the exports directive for compile-time access and the opens directive for runtime reflection. Without these declarations, other modules cannot access the package even with reflection, throwing InaccessibleObjectException. This prevents accidental dependencies on internal implementation packages and allows libraries to evolve without breaking clients. The --add-opens JVM argument can override this for compatibility.

Q6: Why should you prefer immutability over providing setters?
Answer:
Immutability (final fields with no setters) provides several advantages: objects are inherently thread-safe without synchronization, they're simpler to reason about because state never changes, they can be safely shared across threads and cached, and they prevent temporal coupling bugs. For example, a Money class representing currency should be immutable—operations like add() return new instances rather than modifying state. Immutability is especially important for value objects, keys in hash maps, and objects shared across threads, reducing complexity and eliminating entire categories of bugs.

Q7: What is the "Tell, Don't Ask" principle and how does it relate to encapsulation?
Answer:
"Tell, Don't Ask" means you should tell an object what to do rather than querying its state and making decisions externally. This relates to encapsulation because it keeps business logic and invariants within the object rather than scattering them across clients. For example, instead of if (account.getBalance() >= amount) { account.setBalance(account.getBalance() - amount); } which exposes and manipulates state externally, use account.withdraw(amount) which encapsulates the validation and state change. This prevents duplication, enforces invariants in one place, and makes the object's API more meaningful.

Q8: How do you handle encapsulation in a multi-threaded environment?
Answer:
In multi-threaded environments, encapsulation alone is insufficient—you need thread-safe internal data structures or synchronization. Use ConcurrentHashMap instead of HashMap, AtomicInteger instead of int for counters, or synchronize methods accessing shared mutable state. Even with private fields, concurrent access can cause race conditions. For example, a cache class should use ConcurrentHashMap for internal storage and AtomicInteger for access counts to ensure thread safety. Alternatively, make objects immutable to eliminate the need for synchronization entirely.

Q9: What are the performance trade-offs of defensive copying?
Answer:
Defensive copying creates additional objects in the heap, increasing memory usage and GC pressure. Each copy operation has CPU overhead for array/object duplication. The trade-off is between safety and performance—defensive copying prevents bugs but at a cost. Mitigation strategies include: using immutable objects (like Java 8+ date/time classes) which don't need copying, returning unmodifiable wrappers (`Collections.unmodifiableContinueJan 6*`) instead of copies, providing indexed access methods rather than full collection access, or caching copies if repeatedly accessed. For performance-critical code, profile to determine if defensive copying is a bottleneck before optimizing.

Q10: When would you use package-private (default) access instead of private or public?
Answer:
Package-private access is ideal for internal APIs shared among closely related classes within a package but hidden from external packages. Use it for helper classes, utility methods used across package classes, or when implementing design patterns like Strategy or Factory within a package. For example, in a database access layer package, internal connection pooling classes might be package-private while the main repository classes are public. This provides better encapsulation than public while allowing collaboration among related classes, preventing external packages from depending on internal implementation details.

Q11: Explain how frameworks like Spring and Hibernate work with private fields despite encapsulation.
Answer:
Frameworks like Spring (dependency injection) and Hibernate (ORM) use reflection to access and modify private fields at runtime. They call Field.setAccessible(true) to bypass access checks, then use Field.set() to inject dependencies or populate database-mapped fields. This happens through annotations like @Autowired (Spring) or @Column (Hibernate). In module-based applications, the opens directive in module-info.java is required to allow deep reflection. While this technically breaks encapsulation, it's acceptable because frameworks provide legitimate infrastructure concerns (injection, persistence) that shouldn't require manual setter methods for every field.

Q12: What design mistakes indicate poor encapsulation, and how would you refactor them?
Answer:
Common mistakes include: exposing mutable collections or arrays directly (fix: return unmodifiable views or copies), using public fields instead of private with accessors (fix: make fields private, add validation), creating anemic domain models with only getters/setters and no behavior (fix: move business logic into the domain class), allowing invalid object states through unrestricted setters (fix: validate in constructor and setters, use Builder pattern), and over-encapsulation with unnecessary getters for every field (fix: provide meaningful domain operations instead). Good encapsulation balances protection with usability, keeping objects in valid states while providing clear, purposeful APIs.