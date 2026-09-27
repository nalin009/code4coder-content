## MODULE 10: Methods

---

##### MCQ 1 (Beginner)
##### What is the correct syntax to define a method in Java?
##### A) method int calculate() { }  
##### B) public int calculate() { }  
##### C) calculate() int public { }  
##### D) int calculate public() { } 
###### Answer: B) public int calculate() { } 
###### Explanation: The correct syntax is `<access-modifier> <return-type> <method-name>(<parameters>) { }`. Option B follows this structure. Option A uses an invalid keyword "method", while C and D have incorrect ordering of elements.

---

##### MCQ 2 (Beginner)
##### Which of the following is the correct way to call a method named `display()` that takes no parameters?
##### A) call display();  
##### B) display[];  
##### C) display();  
##### D) execute display(); 
###### Answer: C) display();
###### Explanation: Methods are called using their name followed by parentheses. Even if a method has no parameters, parentheses are mandatory. Option C is the correct syntax.

---

##### MCQ 3 (Beginner)
##### What will be the output of the following code?

```java
public static void main(String[] args) {
    int x = 5;
    modify(x);
    System.out.println(x);
}

public static void modify(int a) {
    a = 10;
}
```

##### A) 5  
##### B) 10  
##### C) Compile error  
##### D) Runtime error  
###### Answer: A) 5 
###### Explanation: Java is pass-by-value for primitives. The value 5 is copied into parameter `a`. Modifying `a` does not affect the original variable `x`. Output is 5.

---

##### MCQ 4 (Beginner)
##### What is the return type of the main() method?
##### A) int  
##### B) void  
##### C) String  
##### D) boolean 
###### Answer: B) void  
###### Explanation: The main() method must have a return type of `void`. It does not return any value to the JVM. This requirement has been unchanged since Java 1.0.

---

##### MCQ 5 (Beginner)
##### What is the purpose of the `return` statement in a method?
##### A) To end the method execution and optionally send a value back to the caller  
##### B) To declare the method's return type  
##### C) To call another method  
##### D) To create a loop  
###### Answer: A) To end the method execution and optionally send a value back to the caller  
###### Explanation: The `return` statement terminates method execution and optionally returns a value to the caller. The return type is declared in the method signature, not by the return statement itself.

---

##### MCQ 6 (Intermediate)
##### Which of the following method declarations demonstrates valid method overloading?
##### A) public int add(int a, int b) and public double add(int a, int b)  
##### B) public int add(int a, int b) and public int add(int x, int y)  
##### C) public int add(int a, int b) and public int add(double a, double b)  
##### D) public void add(int a, int b) and private void add(int a, int b)  
###### Answer: C) public int add(int a, int b) and public int add(double a, double b)  
###### Explanation: Method overloading requires the same method name with different parameter lists (type, number, or order). Option C has different parameter types (int vs double). Option A differs only in return type (invalid). Option B has identical signatures (invalid). Option D has identical signatures with different access modifiers (invalid).

---

##### MCQ 7 (Intermediate)
##### What happens when a recursive method does not have a base case?
##### A) Compilation error  
##### B) The method runs infinitely without error  
##### C) StackOverflowError at runtime  
##### D) NullPointerException  
###### Answer: C) StackOverflowError at runtime 
###### Explanation: Without a base case, recursion continues indefinitely, creating stack frames until the JVM stack memory is exhausted, resulting in StackOverflowError. The compiler cannot detect this logic error at compile-time.


---

##### MCQ 8 (Intermediate)
##### Given the following code, what will be printed?

```java
public static void main(String[] args) {
    int[] arr = {1, 2, 3};
    change(arr);
    System.out.println(arr[0]);
}

public static void change(int[] a) {
    a[0] = 99;
}
```

##### A) 1  
##### B) 99  
##### C) Compile error  
##### D) Runtime error
###### Answer: B) 99 
###### Explanation: Arrays are objects stored in heap memory. The reference to the array is passed by value, but both `arr` and `a` point to the same array object. Modifying `a[0]` affects the original array. Output is 99.


---

##### MCQ 9 (Intermediate)
##### Which of the following is a valid signature for the main() method?
##### A) public void main(String[] args)  
##### B) public static void main(String args[])  
##### C) static public void main(String[] args)  
##### D) Both B and C 
###### Answer: D) Both B and C
###### Explanation: Both B and C are valid. The order of `public` and `static` can be interchanged. Array notation can be `String[]` or `String args[]`. However, option A is invalid because it's missing the `static` modifier, which the JVM requires.

---

##### MCQ 10 (Intermediate)
##### Consider the following code. What is the output?

```java
public static void main(String[] args) {
    System.out.println(factorial(3));
}

public static int factorial(int n) {
    if (n == 0) return 1;
    return n * factorial(n - 1);
}
```

##### A) 3  
##### B) 6  
##### C) 9  
##### D) StackOverflowError
###### Answer: B) 6
###### Explanation: The recursive factorial method correctly calculates 3! = 3 × 2 × 1 = 6. The base case (n == 0) prevents infinite recursion.

---

##### MCQ 11 (Intermediate)
##### What is the result of the following method call?

```java
public static void print(int... nums) {
    System.out.println(nums.length);
}

public static void main(String[] args) {
    print(1, 2, 3, 4);
}
```

##### A) 1  
##### B) 4  
##### C) Compile error  
##### D) 10  
###### Answer: B) 4
###### Explanation: Varargs (`int... nums`) allows passing a variable number of arguments. The arguments are internally treated as an array. Four arguments are passed, so `nums.length` is 4.

---

##### MCQ 12 (Advanced)
##### What will be the result of compiling and running the following code?

```java
public class Test {
    public static void main(String[] args) {
        System.out.println("Main with String[]");
    }
    
    public static void main(int x) {
        System.out.println("Main with int");
    }
}
```

##### A) Compile error: duplicate main methods  
##### B) "Main with String[]"  
##### C) "Main with int"  
##### D) Runtime error 
###### Answer: B) "Main with String[]"  
###### Explanation: Method overloading is allowed, including for main(). The JVM only recognizes `main(String[])` as the entry point. The overloaded `main(int)` is just a regular method that can be called explicitly but is not invoked automatically.


---

##### MCQ 13 (Advanced)
##### Which statement about method memory allocation is correct?
##### A) Method parameters are stored in heap memory  
##### B) Local variables of a method are stored in heap memory  
##### C) Each method call creates a new stack frame  
##### D) Static methods do not use stack memory 
###### Answer: C) Each method call creates a new stack frame  
###### Explanation: Each method invocation creates a new stack frame containing local variables, parameters, and return address. Parameters and local variables are stored in the stack, not the heap. Static methods also use stack frames like instance methods.

---

##### MCQ 14 (Advanced)
##### Given the following code, what will happen?

```java
public static void main(String[] args) {
    Person p = new Person("Alice");
    reassign(p);
    System.out.println(p.name);
}

public static void reassign(Person obj) {
    obj = new Person("Bob");
}
```

##### A) Prints "Alice"  
##### B) Prints "Bob"  
##### C) Compile error  
##### D) NullPointerException  
###### Answer: A) Prints "Alice"  
###### Explanation: Java passes references by value. The reference `obj` is a copy of `p`. Reassigning `obj` to a new object does not affect `p`. The original reference `p` still points to "Alice".

---

##### MCQ 15 (Advanced)
##### Which of the following scenarios will cause a compile-time error?

```java
public void show(int a, double b) { }
public void show(double a, int b) { }
```

**Method call:**

##### A) show(5, 10.5)  
##### B) show(5.5, 10)  
##### C) show(5, 10)  
##### D) All of the above compile successfully  
###### Answer: C) show(5, 10) 
###### Explanation: The call `show(5, 10)` is ambiguous. The compiler cannot determine whether to promote the first `int` to `double` (matching second method) or promote the second `int` to `double` (matching first method). This results in a compile-time ambiguity error.

---