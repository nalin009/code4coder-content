## MODULE 4: Variables & Data Types

---

##### MCQ 1 (Beginner)
##### What is the default value of a local variable in Java?
##### A) 0  
##### B) null  
##### C) undefined  
##### D) Local variables have no default value
###### Answer: D) Local variables have no default value
###### Explanation: Local variables are not initialized by the JVM. You must explicitly initialize them before use, or you'll get a compile-time error.

---

##### MCQ 2 (Beginner)
##### Which of the following is NOT a primitive data type in Java?
##### A) int  
##### B) char  
##### C) String  
##### D) boolean
###### Answer: C) String
###### Explanation: `String` is a reference type (a class), not a primitive. The 8 primitives are: `byte`, `short`, `int`, `long`, `float`, `double`, `char`, `boolean`.

---

##### MCQ 3 (Beginner)
##### What is the size of the `int` data type in Java?
##### A) 2 bytes  
##### B) 4 bytes  
##### C) 8 bytes  
##### D) Depends on the JVM
###### Answer: B) 4 bytes
###### Explanation: `int` is always 4 bytes (32 bits) in Java, regardless of platform. This has been consistent since Java 1.0 and remains unchanged till Java 25.

---

##### MCQ 4 (Beginner)
##### What will be the output of the following code?

```java
byte b = 127;
b++;
System.out.println(b);
```

##### A) 128  
##### B) 127  
##### C) -128  
##### D) Compile-time error
###### Answer: C) -128 
###### Explanation: `byte` range is -128 to 127. When you increment 127, it overflows and wraps around to -128.

---

##### MCQ 5 (Beginner)
##### Which keyword is used to define a constant in Java?
##### A) const  
##### B) final  
##### C) static  
##### D) constant
###### Answer: B) final  
###### Explanation: The `final` keyword makes a variable immutable (constant). `const` is a reserved keyword but not used in Java.

---

##### MCQ 6 (Beginner)
##### What is the default value of a boolean instance variable?
##### A) true  
##### B) false  
##### C) 0  
##### D) null
###### Answer: B) false 
###### Explanation: Boolean instance variables are initialized to `false` by default.

---

##### MCQ 7 (Intermediate)
##### What is the result of the following code?

```java
Integer a = 100;
Integer b = 100;
System.out.println(a == b);
```

##### A) true  
##### B) false  
##### C) Compile-time error  
##### D) Runtime exception
###### Answer: A) true  
###### Explanation: Integer values from -128 to 127 are cached. Both `a` and `b` reference the same cached object, so `a == b` is `true`.

---

##### MCQ 8 (Intermediate)
##### What happens when you unbox a null Integer?

```java
Integer num = null;
int value = num;
```

##### A) value is 0  
##### B) Compile-time error  
##### C) NullPointerException at runtime  
##### D) value is null
###### Answer: C) NullPointerException at runtime
###### Explanation: Unboxing `null` calls `num.intValue()`, which throws `NullPointerException` because you're calling a method on a null reference.

---

##### MCQ 9 (Intermediate)
##### Which of the following is an example of implicit casting?
##### A) int x = (int) 3.14;  
##### B) double d = 10;  
##### C) byte b = (byte) 130;  
##### D) char c = (char) 65;
###### Answer: B) double d = 10;
###### Explanation: `int` → `double` is implicit (widening). All others require explicit casting (narrowing).

---

##### MCQ 10 (Intermediate)
##### What is autoboxing in Java?
##### A) Converting a primitive to its wrapper class automatically  
##### B) Converting a wrapper class to its primitive automatically  
##### C) Storing objects in a box  
##### D) A feature for encrypting data
###### Answer: A) Converting a primitive to its wrapper class automatically  
###### Explanation: Autoboxing is the automatic conversion from primitive to wrapper (e.g., `int` → `Integer`).

---

##### MCQ 11 (Intermediate)
##### What will be the output?

```java
int x = 10;
double y = 5.5;
System.out.println(x + y);
```

##### A) 15  
##### B) 15.5  
##### C) 15.0  
##### D) Compile-time error
###### Answer: B) 15.5  
###### Explanation: `int` is implicitly promoted to `double`, and `10 + 5.5 = 15.5`.

---

##### MCQ 12 (Intermediate)
##### Which of the following statements about static variables is TRUE?
##### A) Static variables are stored on the stack  
##### B) Each object has its own copy of static variables  
##### C) Static variables are shared across all instances of a class  
##### D) Static variables must be initialized at declaration
###### Answer: C) Static variables are shared across all instances of a class
###### Explanation: Static variables belong to the class, not individual objects, and are stored in Metaspace. They are shared by all instances.

---

##### MCQ 13 (Advanced)
##### Consider the following code:

```java
Integer a = 200;
Integer b = 200;
System.out.println(a == b);
```

**What is the output and why?**

##### A) true, because both have the same value  
##### B) false, because 200 is outside the Integer cache range  
##### C) true, because autoboxing uses the same object  
##### D) Compile-time error
###### Answer: B) false, because 200 is outside the Integer cache range
###### Explanation: Integer caching applies only to -128 to 127. For 200, two separate objects are created, so `a == b` is `false`. Use `.equals()` for value comparison.

---

##### MCQ 14 (Advanced)
##### What is the output of the following code?

```java
byte a = 10;
byte b = 20;
byte c = a + b;
System.out.println(c);
```

##### A) 30  
##### B) Compile-time error  
##### C) Runtime error  
##### D) 0
###### Answer: B) Compile-time error
###### Explanation: In the expression `a + b`, both `byte` operands are promoted to `int`. You cannot assign an `int` to a `byte` without explicit casting.

**Fix**: `byte c = (byte) (a + b);`

---

##### MCQ 15 (Advanced)
##### Which of the following is a valid use of the `var` keyword?
##### A) var x;  
##### B) var y = null;  
##### C) var z = 10;  
##### D) var name = "Java"; var name = 100;
###### Answer: C) var z = 10;
###### Explanation: `var` requires initialization at declaration. Option A is missing initialization, B cannot infer type from `null`, and D tries to redeclare `name`.


---