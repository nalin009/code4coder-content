## 9. Common Mistakes & Misconceptions

---

#### Mistake 1: Missing Semicolons

```java
// WRONG
int x = 10
System.out.println(x)

// CORRECT
int x = 10;
System.out.println(x);
```

**Why it happens:** Forgetting that Java requires explicit statement terminators.

---

#### Mistake 2: Case Sensitivity

```java
// WRONG
system.out.println("Hello"); // 'system' not recognized
String Name = "Java"; // Legal but violates convention

// CORRECT
System.out.println("Hello");
String name = "Java"; // Lowercase for variables
```

**Why it happens:** Java is case-sensitive; `System ≠ system`.

---

#### Mistake 3: Misplaced Curly Braces

```java
// WRONG
public class Test
    public static void main(String[] args) { // Missing class opening brace
        System.out.println("Hello");
    }
}

// CORRECT
public class Test {
    public static void main(String[] args) {
        System.out.println("Hello");
    }
}
```

**Why it happens:** Not tracking opening and closing braces properly.

---

#### Mistake 4: Accessing Out-of-Scope Variables

```java
// WRONG
if (true) {
    int x = 10;
}
System.out.println(x); // ERROR: x is out of scope

// CORRECT
int x;
if (true) {
    x = 10;
}
System.out.println(x); // OK (but x might be uninitialized)
```

**Why it happens:** Misunderstanding block scope boundaries.

---

#### Mistake 5: Invalid Escape Sequences

```java
// WRONG
String path = "C:\Users\file"; // \U and \f are invalid escape sequences

// CORRECT
String path = "C:\\Users\\file";
```

**Why it happens:** Not escaping backslashes in strings.

---

#### Mistake 6: Confusing `print` and `println`

```java
System.out.print("Hello");
System.out.print("World");
// Output: HelloWorld (no space or newline)

System.out.println("Hello");
System.out.println("World");
// Output:
// Hello
// World
```

**Why it happens:** Not understanding when newlines are added.

---

#### Misconception 1: "Indentation Affects Code Execution"
**Reality:** Indentation is purely cosmetic. The compiler ignores whitespace.

```java
// This compiles and runs identically:
public class Test{public static void main(String[] args){System.out.println("Hello");}}
```

However, it's unreadable. Always use proper indentation.

---

#### Misconception 2: "Comments Slow Down Programs"
**Reality:** Comments are completely removed during compilation. They have zero runtime impact.

---

#### Misconception 3: "You Must Use Javadoc for All Comments"
**Reality:** Javadoc is specifically for documenting public APIs. Use regular comments for internal logic.