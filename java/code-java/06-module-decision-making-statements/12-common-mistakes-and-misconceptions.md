## 12. Common Mistakes & Misconceptions

---

#### 12.1. Using = Instead of ==

```java
int x = 10;
if (x = 5) {  // Compilation error: incompatible types
    System.out.println("Test");
}
```

###### Correct:

```java
if (x == 5) {  // Comparison operator
    System.out.println("Test");
}
```

###### Why This Happens:
In C/C++, assignment returns the assigned value, allowing if (x = 5). Java prevents this by requiring boolean expressions.

---

#### 12.2. Forgetting break in Switch

```java
int x = 2;
switch (x) {
    case 1:
        System.out.println("One");
    case 2:
        System.out.println("Two");  // Executes
    case 3:
        System.out.println("Three");  // Also executes (fallthrough)
}
```

###### Output:

```java
Two
Three
```

**Fix:** Always add break or use switch expressions (Java 14+).

---

#### 12.3. Comparing Strings with ==

```java
String s1 = new String("Hello");
String s2 = new String("Hello");
if (s1 == s2) {  // False - compares references, not content
    System.out.println("Equal");
}
```

###### Correct:

```java
if (s1.equals(s2)) {  // True - compares content
    System.out.println("Equal");
}
```

---

#### 12.4. Not Checking for null Before Method Calls

```java
String name = null;
if (name.equals("John")) {  // NullPointerException
    System.out.println("Match");
}
```

###### Correct:

```java
if (name != null && name.equals("John")) {  // Short-circuit prevents NPE
    System.out.println("Match");
}
```

###### Better (Yoda Conditions):

```java
if ("John".equals(name)) {  // Safe even if name is null
    System.out.println("Match");
}
```

---

#### 12.5. Using Float/Double in Switch

```java
double x = 3.14;
switch (x) {  // Compilation error: incompatible types
    case 3.14:
        System.out.println("Pi");
}
```

**Fix:** Use if-else for floating-point comparisons.

---

#### 12.6. Scope Confusion

```java
if (true) {
    int x = 10;
}
System.out.println(x);  // Error: x out of scope
```

Fix: Declare variable outside if block if needed later.

---

#### 12.7. Missing default in Switch

```java
int x = 10;
switch (x) {
    case 1:
        System.out.println("One");
        break;
    case 2:
        System.out.println("Two");
        break;
    // No default - if x is 10, nothing happens
}
```

Best Practice: Always include default for safety.

---

#### 12.8. Complex Boolean Expressions Without Parentheses

```java
if (a > 5 && b < 10 || c == 20) {  // Confusing precedence
    // Code
}
```

###### Better:

```java
if ((a > 5 && b < 10) || c == 20) {  // Clear intent
    // Code
}
```

---

#### 12.9. Ternary Operator Type Mismatch

```java
String result = (true) ? 1 : "Hello";  // Error: incompatible types
```

Fix: Both expressions must return compatible types.

---

#### 12.10. Deep Nesting

```java
if (condition1) {
    if (condition2) {
        if (condition3) {
            if (condition4) {
                // Hard to read and maintain
            }
        }
    }
}
```

###### Better (Early Returns):

```java
if (!condition1) return;
if (!condition2) return;
if (!condition3) return;
if (!condition4) return;
// Code here
```