## MODULE 12: Encapsulation

---

##### MCQ 1 (Beginner)
##### What is the default access modifier for a class member when no modifier is specified?
##### A) private
##### B) protected
##### C) public
##### D) package-private (default)
###### Answer: D) package-private (default)
###### Explanation: When no access modifier is specified, the member has package-private (default) access, meaning it is accessible only within the same package. This is distinct from private (same class only), protected (same package + subclasses), and public (everywhere).

---

##### MCQ 2 (Beginner)
##### Which access modifier provides the most restrictive access?
##### A) public
##### B) protected
##### C) default
##### D) private
###### Answer: D) private
###### Explanation: The private modifier is the most restrictive—members are accessible only within the same class. No other class, even subclasses, can access private members directly without reflection.

---

##### MCQ 3 (Beginner)
##### What is the primary purpose of getter and setter methods?
##### A) To make code longer
##### B) To provide controlled access to private fields with validation
##### C) To bypass encapsulation
##### D) To improve compilation speed
###### Answer: B) To provide controlled access to private fields with validation
###### Explanation: Getter and setter methods provide controlled access to private fields, allowing validation, computed values, and maintaining class invariants. They are the core mechanism for implementing encapsulation.

---

##### MCQ 4  (Beginner)
##### Can a subclass access the private fields of its parent class directly?
##### A) Yes, always
##### B) Yes, but only if they're in the same package
##### C) No, private members are not inherited
##### D) Yes, using the super keyword
###### Answer: C) No, private members are not inherited
###### Explanation: Private members are not inherited by subclasses. While subclasses contain those fields in memory, they cannot access them directly—they must use public or protected methods provided by the parent.
 
---

##### MCQ 5 (Intermediate)
##### What is the result of calling setAccessible(true) on a Field object in reflection?
##### A) Compilation error
##### B) Suppresses Java access control checks for that field
##### C) Makes the field permanently public
##### D) Has no effect in modern Java
###### Answer: B) Suppresses Java access control checks for that field
###### Explanation: setAccessible(true) suppresses access control checks at runtime, allowing reflection to access private fields and methods. It does not change the field's declared access modifier—it only affects the reflective access operation.

---

##### MCQ 6 (Intermediate)
##### Which statement about protected access is TRUE when accessing from a subclass in a different package?
##### A) Protected members can be accessed through any reference type
##### B) Protected members can only be accessed through the subclass type
##### C) Protected members cannot be accessed at all
##### D) Protected access is the same as public access
###### Answer: B) Protected members can only be accessed through the subclass type
###### Explanation: In a subclass in a different package, protected members can only be accessed through the subclass type (via this or subclass references), not through superclass references. This prevents unrelated subclasses from accessing each other's protected members.

---

##### MCQ 7 (Intermediate)
##### What happens when you return a reference to a mutable object from a getter without defensive copying?
##### A) Compilation error
##### B) External code can modify the internal state
##### C) The JVM throws a SecurityException
##### D) Nothing—Java automatically makes it immutable
###### Answer: B) External code can modify the internal state
###### Explanation: Returning a direct reference to a mutable object (like an array or ArrayList) allows external code to modify the object, breaking encapsulation. Defensive copying or returning an unmodifiable view prevents this.

---

##### MCQ 8 (Intermediate)
##### Which Java feature can bypass encapsulation and access private fields?
##### A) Inheritance
##### B) Polymorphism
##### C) Reflection
##### D) Method overloading
###### Answer: C) Reflection
###### Explanation: Reflection (using setAccessible(true)) can bypass access modifiers and access/modify private fields and methods at runtime. This is used by frameworks like Spring and Hibernate.

---

##### MCQ 9 (Intermediate)
##### What is the purpose of defensive copying in encapsulation?
##### A) To improve performance
##### B) To prevent external modification of mutable internal objects
##### C) To reduce memory usage
##### D) To speed up garbage collection
###### Answer: B) To prevent external modification of mutable internal objects
###### Explanation: Defensive copying creates a new copy of mutable objects (like arrays or dates) when passing them to or from a class, preventing external code from modifying the internal state.

---

##### MCQ 10 (Intermediate)
##### Which statement about package-private (default) access is TRUE?
##### A) Classes in com.example can access default members in com.example.util
##### B) Classes in com.example.util can access default members in com.example
##### C) Classes in the same package can access default members
##### D) Default access is the same as protected access
###### Answer: C) Classes in the same package can access default members
###### Explanation: Package-private (default) access allows access only within the same package. Java has no notion of nested packages—com.example and com.example.util are completely separate packages despite their naming.

---

##### MCQ 11 (Advanced)
##### Which design pattern is best suited for creating objects with many optional fields while maintaining encapsulation?
##### A) Singleton
##### B) Factory
##### C) Builder
##### D) Observer
###### Answer: C) Builder
###### Explanation: The Builder pattern provides a fluent API for constructing objects with many optional fields, maintaining encapsulation by using private constructors and validating state before object creation. It avoids "telescoping constructors."


---

##### MCQ 12  (Advanced)
##### In the Java Platform Module System (JPMS), which directive allows runtime reflection on private members of a package?
##### A) exports
##### B) requires
##### C) opens
##### D) provides
###### Answer: C) opens
###### Explanation: The opens directive in module-info.java allows runtime reflection (deep reflection) on private members of a package, which frameworks like Hibernate and Jackson need. The exports directive only provides compile-time access.

---

##### MCQ 13 (Advanced)
##### Which of the following is TRUE about the SecurityManager and reflection in modern Java (Java 17+)?
##### A) SecurityManager is required for reflection
##### B) SecurityManager was deprecated in Java 17 and provides no protection against reflection
##### C) SecurityManager is enabled by default
##### D) SecurityManager cannot be bypassed
###### Answer: B) SecurityManager was deprecated in Java 17 and provides no protection against reflection
###### Explanation: The SecurityManager was deprecated for removal in Java 17 and is no longer an effective protection mechanism. Modern Java relies on the module system (JPMS) for encapsulation, but within the same module, reflection can still bypass access control.

---

##### MCQ 14 (Advanced)
##### What is the memory location of a private static field in Java 8+?
##### A) Stack
##### B) Heap
##### C) Metaspace
##### D) Thread-local storage
###### Answer: C) Metaspace
###### Explanation: Static fields (regardless of access modifier) are stored in Metaspace (Java 8+) or PermGen (Java 7-), which is part of native memory. Instance fields are in the heap, and local variables are on the stack.

---

##### MCQ 15 (Advanced)
##### Which of the following is the BEST practice for returning a collection from a getter?
##### A) Return the collection directly
##### B) Return Collections.unmodifiableList(collection)
##### C) Return null if empty
##### D) Return a new ArrayList with one element
###### Answer: B) Return Collections.unmodifiableList(collection)
###### Explanation: Returning Collections.unmodifiableList(collection) (or similar wrappers) prevents external modification while avoiding the overhead of defensive copying. It maintains encapsulation by providing a read-only view of the internal collection.

---