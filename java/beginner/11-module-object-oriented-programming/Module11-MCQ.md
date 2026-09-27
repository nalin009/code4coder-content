## MODULE 11: Object-Oriented Programming (OOP) Concepts

---

##### MCQ 1 (Beginner)
##### What will happen if you try to compile and run the following code?

```java
class Test {
    int x;
    
    void display() {
        System.out.println(x);
    }
    
    public static void main(String[] args) {
        Test t = new Test();
        t.display();
    }
}
```

##### A) Compilation error
##### B) Prints 0
##### C) Prints null
##### D) Runtime exception
###### Answer: B) Prints 0
###### Explanation: Instance variables are initialized to default values when an object is created. For numeric types like int, the default value is 0. Therefore, x is automatically initialized to 0, and the program prints 0.

---

##### MCQ 2 (Beginner)
##### Which of the following statements about constructors is TRUE?
##### A) Constructors must have a return type  
##### B) Constructors can be inherited  
##### C) Constructors have the same name as the class  
##### D) Constructors can be abstract  
###### Answer: C) Constructors have the same name as the class 
###### Explanation:  Constructors must have the same name as the class. They do not have a return type (not even void), cannot be inherited, and cannot be abstract or static.

---

##### MCQ 3 (Beginner)
##### What is the output of the following code?

```java
class Counter {
    static int count = 0;
    
    Counter() {
        count++;
    }
}

class Test {
    public static void main(String[] args) {
        Counter c1 = new Counter();
        Counter c2 = new Counter();
        System.out.println(Counter.count);
    }
}
```

##### A) 0
##### B) 1
##### C) 2
##### D) Compilation error
###### Answer: C) 2
###### Explanation: Static variables are shared by all instances of a class. Each time a Counter object is created, the static variable count is incremented. After creating two objects, count becomes 2.

---

##### MCQ 4 (Beginner)
##### If a class does not have any constructor defined, what does the Java compiler do?
##### A) Throws a compilation error
##### B) Provides a default no-arg constructor
##### C) Creates a parameterized constructor 
##### D) Leaves the class without any constructor
###### Answer: B) Provides a default no-arg constructor
###### Explanation: If no constructor is explicitly defined, the Java compiler automatically provides a default no-arg constructor that initializes fields to their default values.

---

##### MCQ 5 (Beginner)
##### Where are objects stored in memory?
##### A) Stack  
##### B) Heap  
##### C) Metaspace  
##### D) Method Area 
###### Answer: B) Heap
###### Explanation: Objects are always stored in the heap memory. Reference variables (which point to objects) are stored in the stack if they are local variables.

---

##### MCQ 6 (Intermediate)
##### What will be the output of the following code?

```java
class Test {
    int x = 10;
    
    Test() {
        this(20);
        System.out.println(x);
    }
    
    Test(int x) {
        this.x = x;
    }
    
    public static void main(String[] args) {
        Test t = new Test();
    }
}
```

##### A) 10
##### B) 20
##### C) Compilation error
##### D) Runtime exception
###### Answer: B) 20
###### Explanation: The no-arg constructor calls this(20), which invokes the parameterized constructor. The parameterized constructor sets this.x = 20. Then control returns to the no-arg constructor, which prints the value 20.

---

##### MCQ 7 (Intermediate)
##### Which of the following is NOT allowed in a static method?
##### A) Calling another static method
##### B) Accessing a static variable 
##### C) Using the this keyword
##### D) Creating an object of the class
###### Answer: C) Using the this keyword
###### Explanation: Static methods cannot use the this keyword because this refers to the current object, and static methods do not belong to any object—they belong to the class itself.

---

##### MCQ 8 (Intermediate)
##### What is the output of the following code?

```java
class Test {
    static int x = 10;
    int y = 20;
    
    void display() {
        System.out.println(x + " " + y);
    }
    
    public static void main(String[] args) {
        Test t1 = new Test();
        Test t2 = new Test();
        t1.x = 30;
        t2.y = 40;
        t1.display();
    }
}
```

##### A) 10 20
##### B) 30 20
##### C) 30 40
##### D) 10 40
###### Answer: B) 30 20
###### Explanation: x is a static variable, so when t1.x = 30 is executed, it changes the class-level variable affecting all instances. y is an instance variable, so t2.y = 40 only affects t2, not t1. Therefore, t1.display() prints 30 (modified static variable) and 20 (t1's instance variable).

---

##### MCQ 9 (Intermediate)
##### Which of the following statements about the this keyword is FALSE?
##### A) this can be used to refer to instance variables
##### B) this can be used to call another constructor 
##### C) this can be used in static methods
##### D) this represents the current object
###### Answer: C) this can be used in static methods
###### Explanation: The this keyword cannot be used in static methods because static methods do not have an associated object instance. this refers to the current object, which doesn't exist in a static context.

---

##### MCQ 10 (Intermediate)
##### What will be the result of compiling the following code?

```java
class Test {
    Test(int x) {
        System.out.println(x);
    }
    
    public static void main(String[] args) {
        Test t = new Test();
    }
}
```

##### A) Prints 0  
##### B) Runtime exception  
##### C) Compilation error  
##### D) No output
###### Answer: C) Compilation error 
###### Explanation: Once a parameterized constructor is defined, Java does not provide a default no-arg constructor. Since `Test()` (no-arg) is called but not defined, this results in a compilation error.

---

##### MCQ 11 (Intermediate)
##### Which of the following can access both static and non-static members?
##### A) Static method  
##### B) Instance method  
##### C) Static block  
##### D) None of the above
###### Answer: B) Instance method 
###### Explanation: Instance methods can access both static members (because they belong to the class) and non-static members (because the instance method belongs to an object). Static methods can only directly access other static members.

---

##### MCQ 12 (Advanced)
##### What will happen when the following code is executed?

```java
class Test {
    Test() {
        display();
    }
    
    void display() {
        System.out.println("Display");
    }
    
    public static void main(String[] args) {
        Test t = new Test();
    }
}
```

##### A) Compilation error
##### B) Prints "Display"
##### C) Runtime exception
##### D) No output
###### Answer: B) Prints "Display"
###### Explanation: There is no issue with calling an instance method from a constructor. The constructor executes, calls display(), and "Display" is printed. This is valid Java code.

---

##### MCQ 13 (Advanced)
##### What is the output of the following code?

```java
class Test {
    static {
        System.out.println("Static block");
    }
    
    Test() {
        System.out.println("Constructor");
    }
    
    public static void main(String[] args) {
        Test t1 = new Test();
        Test t2 = new Test();
    }
}

```
##### A) Static block, Constructor, Constructor  
##### B) Static block, Static block, Constructor, Constructor  
##### C) Constructor, Constructor, Static block  
##### D) Static block, Constructor, Static block, Constructor  
###### Answer: A) Static block, Constructor, Constructor  
###### Explanation: Static blocks execute once when the class is first loaded into memory, before any object is created. The constructor executes each time an object is created. So the output is: Static block (once), Constructor (for t1), Constructor (for t2).

---

##### MCQ 14 (Advanced)
##### What is the output of the following code?

```java
class Test {
    int x;
    
    Test(int x) {
        x = x;
    }
    
    public static void main(String[] args) {
        Test t = new Test(10);
        System.out.println(t.x);
    }
}
```

##### A) 10  
##### B) 0  
##### C) Compilation error  
##### D) Runtime exception
###### Answer: B) 0
###### Explanation: Without using `this.x`, the statement `x = x` assigns the parameter to itself, not to the instance variable. The instance variable `x` remains at its default value of 0.

---

##### MCQ 15 (Advanced)
##### What will happen when the following code is compiled?

```java
class Test {
    Test() {
        this(10);
        System.out.println("No-arg");
    }
    
    Test(int x) {
        this();
        System.out.println(x);
    }
    
    public static void main(String[] args) {
        Test t = new Test();
    }
}
```

##### A) Prints "No-arg" and 10  
##### B) Compilation error  
##### C) Infinite loop  
##### D) Runtime exception 
###### Answer: B) Compilation error 
###### Explanation: This creates a circular constructor invocation. The no-arg constructor calls `this(10)`, which calls the parameterized constructor, which calls `this()`, which calls the no-arg constructor again. Java detects this at compile-time and produces a compilation error: "recursive constructor invocation.

---