## MODULE 13: Inheritance

---

##### MCQ 1 (Beginner)

```java
class Animal {
    void sound() {
        System.out.println("Animal sound");
    }
}

class Dog extends Animal {
    void sound() {
        System.out.println("Bark");
    }
}

public class Test {
    public static void main(String[] args) {
        Animal a = new Dog();
        a.sound();
    }
}
```

##### What is the output?
##### A) Animal sound  
##### B) Bark  
##### C) Compilation error  
##### D) Runtime error
###### Answer: B) Bark 
###### Explanation: This demonstrates **dynamic method dispatch**. Although the reference type is `Animal`, the actual object is `Dog`. At runtime, the JVM uses the Dog's vtable to resolve the `sound()` method, executing the overridden version. This is method overriding in action.

---

##### MCQ 2 (Beginner)
##### Which keyword is used to inherit a class in Java?
##### A) implements  
##### B) inherits  
##### C) extends  
##### D) import  
###### Answer: C) extends  
###### Explanation: The `extends` keyword establishes inheritance relationship between classes. `implements` is used for interfaces, `inherits` is not a Java keyword, and `import` is for including packages/classes.

---

##### MCQ 3 (Beginner)
##### Which of the following represents a HAS-A relationship?
##### A) Dog extends Animal  
##### B) Car extends Vehicle  
##### C) Car contains Engine  
##### D) Manager extends Employee
###### Answer: C) Car contains Engine  
###### Explanation: HAS-A relationship is **composition**, where one class contains a reference to another class. A Car HAS-A Engine. Options A, B, and D represent IS-A relationships (inheritance).

---

##### MCQ 4 (Beginner)
##### How many classes can a Java class directly extend?
##### A) 0  
##### B) 1  
##### C) 2  
##### D) Unlimited 
###### Answer: B) 1  
###### Explanation: Java supports **single inheritance** for classes to avoid the diamond problem. A class can extend only one parent class. However, a class can implement multiple interfaces (interface inheritance).

---

##### MCQ 5 (Beginner)
##### Which keyword is used to call the parent class constructor?
##### A) this()  
##### B) super()  
##### C) parent()  
##### D) base()  
###### Answer: B) super() 
###### Explanation: `super()` calls the parent class constructor and must be the first statement in the child constructor. `this()` calls another constructor in the same class. `parent()` and `base()` are not Java keywords.

---

##### MCQ 6 (Intermediate)

```java
class Parent {
    Parent() {
        System.out.println("Parent constructor");
    }
}

class Child extends Parent {
    Child() {
        System.out.println("Child constructor");
    }
}

public class Test {
    public static void main(String[] args) {
        Child c = new Child();
    }
}
```

##### What is the output?
##### A) Child constructor  
##### B) Parent constructor  
##### C) Parent constructor<br>Child constructor  
##### D) Compilation error
###### Answer: C) Parent constructor<br>Child constructor  
###### Explanation: This demonstrates **constructor chaining**. Java implicitly inserts `super()` as the first statement in the Child constructor, invoking the Parent constructor first. Constructors execute from top (parent) to bottom (child) in the inheritance hierarchy.

---

##### MCQ 7 (Intermediate)

```java
class Animal {
    private void eat() {
        System.out.println("Eating");
    }
}

class Dog extends Animal {
    public void eat() {
        System.out.println("Dog eating");
    }
}
```

##### Is this valid method overriding?
##### A) Yes, valid overriding  
##### B) No, compilation error  
##### C) No, this is method hiding  
##### D) No, private methods are not inherited
###### Answer: D) No, private methods are not inherited
###### Explanation: Private methods are not inherited by child classes. The `eat()` method in Dog is a completely new method, not an override. This code compiles successfully because there's no conflict—the two methods exist independently in their respective classes.

---

##### MCQ 8 (Intermediate)

```java
class Parent {
    public void display() {
        System.out.println("Parent");
    }
}

class Child extends Parent {
    @Override
    private void display() {  // Line X
        System.out.println("Child");
    }
}
```

##### What happens at Line X?
##### A) Compiles successfully  
##### B) Compilation error: cannot reduce visibility  
##### C) Runtime error  
##### D) Compiles but runtime error 
###### Answer: B) Compilation error: cannot reduce visibility
###### Explanation: When overriding, the child method **cannot have more restrictive access** than the parent. Parent's `display()` is `public`, so Child's version cannot be `private` (more restrictive). Valid transitions: private → default → protected → public.

---

##### MCQ 9 (Intermediate)

```java
class A {
    A() {
        System.out.println("A");
    }
}

class B extends A {
    B() {
        super();
        super();  // Line X
    }
}
```

##### What happens at Line X?
##### A) Prints "A" twice  
##### B) Compilation error  
##### C) Runtime error  
##### D) No output
###### Answer: B) Compilation error 
###### Explanation: `super()` (or `this()`) can be called **only once** as the first statement in a constructor. Calling it twice violates Java's constructor chaining rules. The compiler will reject this code.

---

##### MCQ 10 (Intermediate)

```java
final class ImmutableClass {
    void display() {
        System.out.println("Immutable");
    }
}

class MyClass extends ImmutableClass {  // Line X
}
```

##### What happens at Line X?
##### A) Compiles successfully  
##### B) Compilation error: cannot extend final class  
##### C) Runtime error  
##### D) Only a warning, no error 
###### Answer: B) Compilation error: cannot extend final class 
###### Explanation: A `final` class **cannot be extended**. This is enforced at compile time. Java's `String`, `Integer`, and `Math` classes are examples of final classes. This design prevents modification of critical behavior.

---

##### MCQ 11 (Intermediate)
##### What is the primary purpose of the `@Override` annotation?
##### A) Required for method overriding  
##### B) Compile-time verification that method is actually being overridden  
##### C) Improves runtime performance  
##### D) Makes the method final 
###### Answer: B) Compile-time verification that method is actually being overridden  
###### Explanation: `@Override` is **not mandatory** but highly recommended. It instructs the compiler to verify that you're actually overriding a parent method. If there's a typo or signature mismatch, the compiler will catch it, preventing subtle bugs.

---

##### MCQ 12 (Advanced)

```java
class Parent {
    static void print() {
        System.out.println("Parent");
    }
}

class Child extends Parent {
    static void print() {
        System.out.println("Child");
    }
}

public class Test {
    public static void main(String[] args) {
        Parent p = new Child();
        p.print();
    }
}
```

##### What is the output?
##### A) Child  
##### B) Parent  
##### C) Compilation error  
##### D) Runtime error  
###### Answer: B) Parent 
###### Explanation: This is **method hiding**, not overriding. Static methods are resolved at **compile time** based on the reference type (Parent), not at runtime based on object type. Since `p` is of type Parent, `Parent.print()` is called.

---

##### MCQ 13 (Advanced)
##### Which statement about the memory model of inheritance is TRUE?
##### A) Two separate objects (parent and child) are created  
##### B) One object is created containing only child class fields  
##### C) One object is created containing both parent and child class fields  
##### D) Parent object is created first, then child object references it
###### Answer: C) One object is created containing both parent and child class fields
###### Explanation: When you create a child class object, **only one object** is created in the heap. This single object contains all non-private fields from the entire inheritance hierarchy (grandparent → parent → child). This is a critical JVM-level understanding for experienced developers.

---

##### MCQ 14 (Advanced)

```java
class Parent {
    void process() throws IOException {
        // code
    }
}

class Child extends Parent {
    @Override
    void process() throws Exception {  // Line X
        // code
    }
}
```

##### What happens at Line X?
##### A) Compiles successfully  
##### B) Compilation error: broader exception not allowed  
##### C) Runtime error  
##### D) Warning only 
###### Answer: B) Compilation error: broader exception not allowed  
###### Explanation: When overriding, the child method can throw **same, subclass, or no exception**, but **cannot throw a broader checked exception** than the parent. `Exception` is broader than `IOException`, so this violates the overriding rule. However, throwing `FileNotFoundException` (subclass of IOException) would be valid.

---

##### MCQ 15 (Advanced)
##### In which memory area is the vtable (virtual method table) stored?
##### A) Heap  
##### B) Stack  
##### C) Metaspace (Method Area)  
##### D) Native memory 
###### Answer: C) Metaspace (Method Area)  
###### Explanation: The vtable is part of **class metadata** stored in Metaspace (Method Area in Java 7 and earlier). Each class has its own vtable containing pointers to method implementations. The actual object in the heap has a pointer to its class's vtable, enabling dynamic method dispatch. This is JVM-implementation-specific but consistent across modern JVMs. Unchanged till Java 25.

---

##### MCQ 16 (Advanced)

```java
class A {
    public A() {
        method();
    }
    
    public void method() {
        System.out.println("A");
    }
}

class B extends A {
    private int value = 10;
    
    @Override
    public void method() {
        System.out.println("B: " + value);
    }
}

public class Test {
    public static void main(String[] args) {
        A obj = new B();
    }
}
```

##### What is the output?
##### A) A
##### B) B: 10
##### C) B: 0
##### D) NullPointerException
###### Answer: B) B: 10
###### Explanation: This demonstrates a critical pitfall: calling overridable methods from constructors. When new B() is called, constructor chaining happens: B() → A(). Inside A's constructor, method() is called. Since the actual object is type B, Java calls B's method(). However, B's fields haven't been initialized yet (constructor body hasn't run), so value has its default value 0, not 10. Best practice: Never call overridable methods from constructors.

---

##### MCQ 17 (Intermediate)
##### Which statement about sealed classes (Java 17+) is correct?
##### A) Sealed classes can be extended by any class
##### B) A sealed class must list all permitted subclasses using permits
##### C) Sealed classes cannot have abstract methods
##### D) Sealed classes are implicitly final
###### Answer: B) A sealed class must list all permitted subclasses using permits
###### Explanation: Sealed classes (introduced in Java 17, unchanged till Java 25) restrict which classes can extend them. The permits clause explicitly lists allowed subclasses. Permitted subclasses must be declared as final, sealed, or non-sealed. Sealed classes CAN have abstract methods and are NOT implicitly final—they can be extended by permitted classes.

---

##### MCQ 18 (Advanced)

```java
class Parent {
    protected int x = 10;
}

class Child extends Parent {
    private int x = 20;
    
    public void display() {
        System.out.println(x);
        System.out.println(super.x);
        System.out.println(this.x);
    }
}
```

##### What is the output of `new Child().display()`?
##### A) 10 10 10  
##### B) 20 10 20  
##### C) 20 20 20  
##### D) Compilation error 
###### Answer: B) 20 10 20
###### Explanation: This demonstrates **field hiding** (not overriding—fields cannot be overridden). The Child class has its own `x` field, hiding the parent's `x`. When you access `x` or `this.x`, you get Child's version (20). `super.x` explicitly accesses the parent's field (10). Both fields exist in the object, occupying separate memory. This is different from method overriding where only one implementation executes.

---

##### MCQ 19 (Beginner)
##### What happens if a child class constructor doesn't explicitly call `super()` or `this()`?
##### A) Compilation error  
##### B) Java implicitly inserts `super()` as the first statement  
##### C) Parent constructor is not called  
##### D) Runtime error 
###### Answer: B) Java implicitly inserts `super()` as the first statement
###### Explanation: If the child constructor doesn't explicitly call `super()` or `this()`, Java automatically inserts `super()` (no-arg) as the first statement. This ensures parent class initialization before child initialization. If the parent class has no no-arg constructor, you MUST explicitly call a parameterized parent constructor, otherwise compilation fails.

---

##### MCQ 20 (Advanced - JVM Internals)
##### Where is the vtable (virtual method table) stored in the JVM?
##### A) Heap  
##### B) Stack  
##### C) Metaspace (Method Area)  
##### D) Native memory 
###### Answer: C) Metaspace (Method Area)  
###### Explanation: The vtable is part of **class metadata** stored in Metaspace (called Method Area in Java 7 and earlier). Each class has one vtable containing pointers to method implementations. Objects in the heap have a pointer to their class's vtable, enabling O(1) method lookup during dynamic dispatch. This has been consistent across JVM implementations and unchanged till Java 25. Understanding this is crucial for 5+ YOE interviews.

---

##### MCQ 6
#####
##### A) 
##### B) 
##### C) 
##### D) 
###### Answer: 
###### Explanation:

---

##### MCQ 7
#####
##### A) 
##### B) 
##### C) 
##### D) 
###### Answer: 
###### Explanation:

---

##### MCQ 8
#####
##### A) 
##### B) 
##### C) 
##### D) 
###### Answer: 
###### Explanation:

---

##### MCQ 9
#####
##### A) 
##### B) 
##### C) 
##### D) 
###### Answer: 
###### Explanation:

---

##### MCQ 10
#####
##### A) 
##### B) 
##### C) 
##### D) 
###### Answer: 
###### Explanation:

---

##### MCQ 11
#####
##### A) 
##### B) 
##### C) 
##### D) 
###### Answer: 
###### Explanation:

---

##### MCQ 12
#####
##### A) 
##### B) 
##### C) 
##### D) 
###### Answer: 
###### Explanation:

---

##### MCQ 13
#####
##### A) 
##### B) 
##### C) 
##### D) 
###### Answer: 
###### Explanation:

---

##### MCQ 14
#####
##### A) 
##### B) 
##### C) 
##### D) 
###### Answer: 
###### Explanation:

---

##### MCQ 15
#####
##### A) 
##### B) 
##### C) 
##### D) 
###### Answer: 
###### Explanation:

---

