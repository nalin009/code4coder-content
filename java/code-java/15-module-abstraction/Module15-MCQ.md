## Module 15: Abstraction

---

##### MCQ 1 (Beginner)
##### Which of the following statements about abstract classes is TRUE?
##### A) Abstract classes can be instantiated directly using the new keyword
##### B) Abstract classes must have at least one abstract method
##### C) Abstract classes can have constructors
##### D) Abstract classes cannot have concrete methods
###### Answer: C) Abstract classes can have constructors
###### Explanation: Abstract classes can have constructors, which are invoked when a concrete subclass object is created using super(). Option A is false because abstract classes cannot be instantiated directly. Option B is false; an abstract class can have zero abstract methods. Option D is false; abstract classes can have both abstract and concrete methods.

---

##### MCQ 2 (Beginner)
##### What happens if a concrete class implements an interface but does not implement all of its abstract methods?
##### A) The code compiles successfully
##### B) The class must be declared abstract
##### C) The compiler issues a warning but compiles
##### D) The JVM throws an exception at runtime
###### Answer: B) The class must be declared abstract
###### Explanation: If a class implements an interface but does not provide implementations for all abstract methods, it must be declared abstract. Otherwise, the compiler produces an error. Option A is incorrect; the code will not compile. Options C and D are incorrect; this is a compile-time check, not a runtime or warning scenario.

---

##### MCQ 3 (Beginner)
##### Which keyword is used to implement an interface in Java?
##### A) extends
##### B) implements
##### C) inherits
##### D) uses
###### Answer: B) implements
###### Explanation: The implements keyword is used to implement an interface in Java. extends is used for class inheritance and interface-to-interface inheritance. Options C and D are not valid Java keywords for this purpose.

---

##### MCQ 4 (Beginner)
##### Can an interface extend another interface?
##### A) No, interfaces cannot extend anything
##### B) Yes, using the implements keyword
##### C) Yes, using the extends keyword
##### D) Only if both interfaces are functional interfaces
###### Answer: C) Yes, using the extends keyword
###### Explanation: Interfaces can extend other interfaces using the extends keyword (not implements). This allows interface inheritance. Option D is false; there is no restriction based on functional interfaces.

---

##### MCQ 5 (Beginner)
##### What is the access modifier of all abstract methods in an interface (before Java 9)?
##### A) private
##### B) protected
##### C) public
##### D) default (package-private)
###### Answer: C) public
###### Explanation: All abstract methods in interfaces are implicitly public (before Java 9, when private methods were introduced). Options A, B, and D are incorrect; interface methods are part of a public contract.

---

##### MCQ 6 (Intermediate)
##### Can an abstract class have a final method?
##### A) No, because abstract classes cannot have concrete methods
##### B) Yes, final methods in abstract classes cannot be overridden by subclasses
##### C) No, final and abstract are mutually exclusive
##### D) Yes, but only if the method is also static
###### Answer: B) Yes, final methods in abstract classes cannot be overridden by subclasses
###### Explanation: Abstract classes can have final methods, which are concrete methods that cannot be overridden by subclasses. Option A is false; abstract classes can have concrete methods. Option C is false for methods (though a class cannot be both abstract and final). Option D is false; final methods don't need to be static.

---

##### MCQ 7 (Intermediate)
##### What is the output of the following code?

```java
abstract class Animal {
    abstract void sound();
    
    void sleep() {
        System.out.println("Sleeping");
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
        a.sleep();
    }
}
```

##### A) Compile error
##### B) Bark Sleeping
##### C) Sleeping Bark
##### D) Runtime exception
###### Answer: B) Bark Sleeping
###### Explanation: The code compiles and runs successfully. Animal a = new Dog() is valid (polymorphism). a.sound() invokes Dog's implementation, printing "Bark". a.sleep() invokes the concrete method from Animal, printing "Sleeping". The output is "Bark" followed by "Sleeping" on the next line.

---

##### MCQ 8 (Intermediate)
##### Which of the following is TRUE about interfaces in Java 8+?
##### A) Interfaces can have constructors
##### B) Interfaces can have default methods with implementation
##### C) Interfaces can have instance variables
##### D) All methods in interfaces must be abstract
###### Answer: B) Interfaces can have default methods with implementation
###### Explanation: Java 8 introduced default methods in interfaces, which can have implementations. Option A is false; interfaces cannot have constructors. Option C is false; interfaces can only have constants (public static final), not instance variables. Option D is false; interfaces can have abstract, default, static, and (since Java 9) private methods.

---

##### MCQ 9 (Intermediate)
##### What is the diamond problem in Java, and how is it resolved?
##### A) Multiple classes extending one abstract class; resolved by compiler error
##### B) Multiple interfaces with same default method; resolved by explicit override in implementing class
##### C) Circular inheritance; resolved by JVM at runtime
##### D) Interface inheriting from abstract class; resolved by Java's type system
###### Answer: B) Multiple interfaces with same default method; resolved by explicit override in implementing class
###### Explanation: The diamond problem occurs when a class implements multiple interfaces that have the same default method. Java resolves this by requiring the implementing class to explicitly override the method and optionally use InterfaceName.super.methodName() to call a specific interface's implementation. Option A describes single inheritance limitation. Options C and D are incorrect scenarios.

---

##### MCQ 10 (Intermediate)
##### Which of the following is a valid marker interface in Java?
##### A) Runnable
##### B) Serializable
##### C) Comparable
##### D) Cloneable
###### Answer: B and D (Both are marker interfaces)
###### For MCQ purposes, if only one option is allowed: B (Serializable) or D (Cloneable)
###### Explanation: Marker interfaces have no methods. Serializable and Cloneable are marker interfaces used by the JVM for special treatment. Runnable has one method (run()), and Comparable has one method (compareTo()), so they are not marker interfaces. If the question allows multiple correct answers, both B and D are correct; otherwise, B is the most commonly referenced marker interface.

---

##### MCQ 11 (Intermediate)
##### What is the purpose of the @FunctionalInterface annotation?
##### A) To mark an interface that can only be implemented once
##### B) To ensure an interface has exactly one abstract method
##### C) To enable multiple inheritance
##### D) To make all methods in the interface default methods
###### Answer: B) To ensure an interface has exactly one abstract method
###### Explanation: The @FunctionalInterface annotation is a compile-time check ensuring that an interface has exactly one abstract method, making it eligible for lambda expressions. Options A, C, and D are incorrect descriptions of this annotation's purpose.

---

##### MCQ 12 (Intermediate)
##### Can an interface have a private method?
##### A) No, interfaces cannot have private methods
##### B) Yes, since Java 8
##### C) Yes, since Java 9
##### D) Yes, but only if the method is static
###### Answer: C) Yes, since Java 9
###### Explanation: Java 9 introduced private methods in interfaces to enable code reuse within default and static methods. Option B is incorrect; Java 8 introduced default and static methods, but not private methods. Option D is partially true but incomplete; both private instance and private static methods are allowed in interfaces since Java 9.

---

##### MCQ 13 (Advanced)
##### What will be the output of the following code?

```java
interface A {
    default void show() {
        System.out.println("A");
    }
}

interface B {
    default void show() {
        System.out.println("B");
    }
}

class C implements A, B {
    public void show() {
        A.super.show();
    }
}

public class Test {
    public static void main(String[] args) {
        C c = new C();
        c.show();
    }
}
```

##### A) Compile error
##### B) A
##### C) B
##### D) Runtime exception
###### Answer: B) A
###### Explanation: The code resolves the diamond problem by explicitly overriding show() in class C and calling A.super.show(), which invokes interface A's default method. The output is "A". Without the explicit override, the code would not compile.

---

##### MCQ 14 (Advanced)
##### Which of the following statements about sealed classes (Java 17+) is TRUE?
##### A) Sealed classes can be extended by any subclass
##### B) Sealed classes restrict which classes can extend them using the permits clause
##### C) Sealed classes cannot be abstract
##### D) Sealed classes are a replacement for abstract classes
###### Answer: B) Sealed classes restrict which classes can extend them using the permits clause
###### Explanation: Sealed classes (introduced in Java 17) use the permits clause to explicitly specify which classes can extend them. Option A is false; sealed classes restrict inheritance. Option C is false; sealed classes can be abstract. Option D is false; sealed classes complement, not replace, abstract classes.

---

##### MCQ 15 (Advanced)
##### Which bytecode instruction is used for interface method invocation?
##### A) invokevirtual
##### B) invokeinterface
##### C) invokestatic
##### D) invokedynamic
###### Answer: B) invokeinterface
###### Explanation: The JVM uses the invokeinterface instruction for calling interface methods. invokevirtual is used for instance methods in classes. invokestatic is for static methods. invokedynamic is primarily for dynamic language support and lambda expressions. This is a JVM-level implementation detail and is unchanged through Java 25.

---