## 7. Real-World Use Cases

---

#### 7.1. Beginner Use Cases
##### Use Case 1: Calculator Application

```java
public class Calculator {
    public static void main(String[] args) {
        int a = 10, b = 5;
        
        System.out.println("Addition: " + (a + b));
        System.out.println("Subtraction: " + (a - b));
        System.out.println("Multiplication: " + (a * b));
        System.out.println("Division: " + (a / b));
        System.out.println("Modulus: " + (a % b));
    }
}
```

##### Use Case 2: Grade Evaluation

```java
public class GradeChecker {
    public static void main(String[] args) {
        int marks = 75;
        String grade = (marks >= 90) ? "A" : (marks >= 75) ? "B" : (marks >= 60) ? "C" : "F";
        System.out.println("Grade: " + grade);  // Output: Grade: B
    }
}
```

---

#### 7.2. Interview Use Cases
##### Use Case 1: Swap Without Temp Variable (Bitwise XOR)

```java
public class SwapWithoutTemp {
    public static void main(String[] args) {
        int a = 5, b = 10;
        
        a = a ^ b;  // a = 5 ^ 10 = 15 (binary: 0101 ^ 1010 = 1111)
        b = a ^ b;  // b = 15 ^ 10 = 5
        a = a ^ b;  // a = 15 ^ 5 = 10
        
        System.out.println("a = " + a + ", b = " + b);  // a = 10, b = 5
    }
}
```

**Interview Insight:** This demonstrates understanding of bitwise operations, though in production, using a temp variable is clearer and equally efficient.

##### Use Case 2: Check Even/Odd (Bitwise AND)

```java
public class EvenOddChecker {
    public static boolean isEven(int number) {
        return (number & 1) == 0;  // Checks if least significant bit is 0
    }
    
    public static void main(String[] args) {
        System.out.println(isEven(4));  // true
        System.out.println(isEven(7));  // false
    }
}
```

**Why This Works:** Even numbers have LSB = 0, odd numbers have LSB = 1.

---

#### 7.3. Production Use Cases
##### Use Case 1: Permissions/Flags Management

```java
public class FilePermissions {
    public static final int READ = 1 << 0;    // 0001 = 1
    public static final int WRITE = 1 << 1;   // 0010 = 2
    public static final int EXECUTE = 1 << 2; // 0100 = 4
    
    public static void main(String[] args) {
        int permissions = READ | WRITE;  // Grant read and write: 0011 = 3
        
        // Check if has read permission
        boolean canRead = (permissions & READ) != 0;  // true
        
        // Check if has execute permission
        boolean canExecute = (permissions & EXECUTE) != 0;  // false
        
        // Grant execute permission
        permissions |= EXECUTE;  // 0111 = 7
        
        // Revoke write permission
        permissions &= ~WRITE;  // 0101 = 5
        
        System.out.println("Final permissions: " + permissions);
    }
}
```

**Production Insight:** This pattern is used in file systems (Unix permissions), GUI frameworks (event flags), and game engines (entity component flags).

##### Use Case 2: Null-Safe Chaining with Short-Circuit

```java
public class FilePermissions {
    public static final int READ = 1 << 0;    // 0001 = 1
    public static final int WRITE = 1 << 1;   // 0010 = 2
    public static final int EXECUTE = 1 << 2; // 0100 = 4
    
    public static void main(String[] args) {
        int permissions = READ | WRITE;  // Grant read and write: 0011 = 3
        
        // Check if has read permission
        boolean canRead = (permissions & READ) != 0;  // true
        
        // Check if has execute permission
        boolean canExecute = (permissions & EXECUTE) != 0;  // false
        
        // Grant execute permission
        permissions |= EXECUTE;  // 0111 = 7
        
        // Revoke write permission
        permissions &= ~WRITE;  // 0101 = 5
        
        System.out.println("Final permissions: " + permissions);
    }
}
```

**Production Insight:** Before Java 8's Optional, this was the standard null-safe access pattern. Short-circuit evaluation prevents null pointer exceptions.

##### Use Case 3: Fast Multiplication/Division by Powers of 2

```java
public class BitwiseOptimization {
    public static void main(String[] args) {
        int x = 10;
        
        int multiply_by_4 = x << 2;  // x * 4 = 40
        int multiply_by_8 = x << 3;  // x * 8 = 80
        
        int divide_by_2 = x >> 1;  // x / 2 = 5
        int divide_by_4 = x >> 2;  // x / 4 = 2
        
        System.out.println("x * 4 = " + multiply_by_4);
        System.out.println("x / 2 = " + divide_by_2);
    }
}
```

**Production Insight:** Modern JVMs optimize this automatically, but in performance-critical embedded systems or manual JIT tuning, this can matter. More importantly, it demonstrates low-level understanding in interviews.