## MODULE 11: Object-Oriented Programming (OOP) Concepts

---
---
### Question 1: What is Object-Oriented Programming, and why did Java adopt it as its primary paradigm?

**Answer:**

Object-Oriented Programming is a programming paradigm that organizes software design around objects rather than functions and logic. An object bundles related data (fields) and behavior (methods) into a single unit. Java adopted OOP as its primary paradigm to address the challenges of building large, maintainable software systems. OOP provides encapsulation (data hiding), inheritance (code reuse), polymorphism (flexibility), and abstraction (hiding complexity). Unlike C++, which supports both procedural and object-oriented styles, Java enforces OOP principles, ensuring consistency and making it easier for teams to collaborate on large projects. This design decision makes Java particularly suitable for enterprise applications where maintainability and scalability are critical.

---

### Question 2: Explain the difference between a class and an object. What happens in memory when an object is created?

**Answer:**

A class is a blueprint or template that defines the structure and behavior for objects, while an object is a runtime instance of that class. At compile-time, the class definition is converted to bytecode and stored in a `.class` file. At runtime, when an object is created using the `new` keyword, the JVM allocates memory in the heap for the object, initializes fields to default values, executes the constructor, and returns a reference to the newly created object. The reference variable (pointing to the object) is stored in the stack, while the actual object resides in the heap. Multiple reference variables can point to the same object, a concept called aliasing. This separation between blueprint (class) and instance (object) allows one class to create unlimited objects.

---

### Question 3: Why does Java automatically provide a default constructor only when no constructor is defined? What is the reasoning behind this design?

**Answer:**

Java provides a default no-arg constructor to ensure that every class can be instantiated, even if the developer forgets to define a constructor. However, once you define any constructor (parameterized or otherwise), Java assumes you want full control over object initialization and stops providing the default constructor. This design prevents accidental object creation without proper initialization. For example, if you define a constructor requiring critical parameters like database connection details, Java won't allow instantiation without those parameters, preventing partially initialized objects. This enforces better design practices by making developers explicitly handle all initialization scenarios. If you need both parameterized and no-arg constructors, you must define both explicitly, which makes the code's intent clearer.

---

### Question 4: Explain the `this` keyword and its three primary use cases with examples.

**Answer:**

The `this` keyword is a reference to the current object—the object whose method or constructor is currently executing. It has three primary uses. First, it disambiguates instance variables from parameters with the same name: `this.name = name` makes it clear that `this.name` refers to the field while `name` refers to the parameter. Second, it enables constructor chaining: `this(value)` calls another constructor in the same class, allowing code reuse and avoiding duplication. This call must be the first statement in the constructor. Third, it passes the current object as an argument to other methods: `system.register(this)` passes the current object to another class's method. At the JVM level, `this` is implicitly passed as a hidden first parameter to every instance method, which is why instance methods can access instance variables.

---

### Question 5: What is the difference between static and non-static (instance) members? Why can't static methods access instance variables directly?

**Answer:**

Static members belong to the class itself and are shared by all instances, while instance members belong to individual objects. Static variables are stored in Metaspace (Java 8+) and initialized when the class is first loaded. Instance variables are stored in the heap and created separately for each object. Static methods cannot access instance variables directly because they execute at the class level without any associated object. When you call a static method, no `this` reference exists—there's no object context. The JVM doesn't know which object's instance variable to access. However, static methods can access instance members by creating an object first: inside a static method, you can do `new MyClass().instanceMethod()`. This restriction enforces the logical separation between class-level and object-level behavior, preventing confusion about data scope.

---

### Question 6: Describe the memory layout when the following code executes: `Student s1 = new Student(); Student s2 = s1;`

**Answer:**

When `Student s1 = new Student()` executes, the JVM allocates memory in the heap for a `Student` object and stores the reference in stack variable `s1`. The object contains instance variables initialized to default values, and if a constructor is defined, it executes. When `Student s2 = s1` executes, no new object is created. Instead, `s2` becomes another reference pointing to the same heap object that `s1` points to. Both `s1` and `s2` are stack variables holding the same memory address. Any modification through `s1` or `s2` affects the same object. This demonstrates Java's reference semantics—variables hold references, not the actual objects. If you later set `s1 = null`, the object remains accessible through `s2`. The object becomes eligible for garbage collection only when no references point to it.

---

### Question 7: What are static blocks, and when are they used? In what order do static blocks execute?

**Answer:**

Static blocks are initialization blocks prefixed with the `static` keyword. They execute once when the class is first loaded into memory, before any object is created or any static method is called. Static blocks are used for complex initialization of static variables, such as loading configuration files, establishing database connections, or initializing static collections. If a class has multiple static blocks, they execute in the order they appear in the source code. Static variable declarations also execute in order with static blocks. For example, if you have `static int x = 10;` followed by a static block that modifies `x`, the variable is first initialized to 10, then the static block executes. If an exception occurs in a static block, it's wrapped in an `ExceptionInInitializerError`, causing the class to fail to load.

---

### Question 8: What is constructor chaining, and why is it useful? What are the rules for using `this()` and `super()` in constructors?

**Answer:**

Constructor chaining is the technique of calling one constructor from another in the same class (using `this()`) or from a parent class (using `super()`). It's useful for avoiding code duplication when multiple constructors share initialization logic. For example, if one constructor initializes all fields and others provide default values, the simpler constructors can delegate to the main one using `this()`. The key rules are: (1) `this()` or `super()` must be the first statement in a constructor—you cannot have both, and nothing can precede them. (2) You cannot have circular constructor invocation; Java detects this at compile-time. (3) If you don't explicitly call `super()`, Java implicitly inserts `super()` (no-arg) as the first statement, calling the parent class's no-arg constructor. This ensures proper initialization order up the inheritance hierarchy.

---

### Question 9: Explain a real-world scenario where improper use of static variables can cause a memory leak in a production application.

**Answer:**

Consider a web application where a static `Map` is used to cache user session data: `static Map<String, UserSession> cache = new HashMap<>();`. If user sessions are added to this cache but never removed (for example, when users log out), the cache grows indefinitely. Since static variables are held by the class and classes remain loaded as long as the application runs, these `UserSession` objects are never garbage collected, even after users have logged out. Over time, the heap fills up, causing `OutOfMemoryError`. This is a classic static memory leak. The solution is to use weak references (`WeakHashMap`), time-based expiration, or instance-level caching with proper lifecycle management. Production applications must be extremely careful with static collections and ensure they have cleanup mechanisms, especially in long-running server applications where classes are loaded once and remain in memory indefinitely.

---

### Question 10: Why can't you use the `this` keyword in a static context? Explain from the JVM's perspective.

**Answer:**

The `this` keyword represents the current object instance. Static methods and static blocks execute at the class level, not the instance level. When you call a static method, no object exists—you can call it directly on the class: `ClassName.staticMethod()`. From the JVM's perspective, instance methods receive an implicit hidden parameter: the `this` reference, which points to the object on which the method was invoked. Static methods do not receive this parameter because they're not invoked on an object. If Java allowed `this` in static methods, the JVM wouldn't know which object's `this` to provide—there might be zero, one, or thousands of instances. This restriction enforces logical correctness: class-level operations (static) remain separate from instance-level operations (non-static). If a static method needs to access instance members, it must first create or receive an object reference explicitly.

---

### Question 11: What happens if you declare a variable with the same name as a parameter in a constructor but don't use the `this` keyword? Provide an example with explanation.

**Answer:**

If you don't use `this`, the parameter shadows the instance variable, and the instance variable never gets initialized. For example: `class Test { int x; Test(int x) { x = x; } }` In this case, the statement `x = x` refers to the parameter on both sides—you're assigning the parameter to itself. The instance variable `x` remains at its default value of 0. To fix this, you must use `this.x = x`, where `this.x` refers to the instance variable and `x` refers to the parameter. This is called variable shadowing. The compiler uses the closest scope first: the parameter is in the local scope, so it takes precedence. Using `this` explicitly tells the compiler to access the instance scope. This is a common source of bugs, especially for beginners, and modern IDEs often warn about such assignments.

---

### Question 12: Compare and contrast static methods and instance methods in terms of memory, performance, and use cases.

**Answer:**

Static methods belong to the class and can be called without creating an object. They're stored in Metaspace along with class metadata. Instance methods belong to objects and require an object to be invoked. In terms of memory, static methods have a single copy per class, while instance methods exist once per class but are invoked through object references. Performance-wise, static methods are marginally faster because they avoid the indirection of accessing through an object reference, but this difference is negligible in modern JVMs. Static methods are ideal for utility functions (like `Math.sqrt()`), factory methods, or operations that don't depend on object state. Instance methods are used when behavior depends on or modifies object state. A key limitation of static methods is they cannot be overridden (they can be hidden but not polymorphically overridden), while instance methods support full polymorphism. In production, excessive static state can lead to testing difficulties and concurrency issues, so instance methods are preferred when state management is involved.