## 7 Ternary Operator (? :)

---

#### 7.1 What is the Ternary Operator?
The ternary operator is a `compact`, `inline` way to write `simple` if-else logic. It's the only operator in Java that takes `three operands`, hence "`ternary`".

**Syntax:**

```java
condition ? expression1 : expression2;
```

---

#### 7.2 How It Works:
- If condition is `true`, returns expression1
- If condition is `false`, returns expression2
- Both expressions must be `compatible` types

**Example:**

```java
int age = 20;
String result = (age >= 18) ? "Adult" : "Minor";
System.out.println(result);
```

**Output:**

```java
Adult
```

**Equivalent if-else:**

```java
int age = 20;
String result;
if (age >= 18) {
    result = "Adult";
} else {
    result = "Minor";
}
System.out.println(result);
```

---

#### 7.3 When to Use Ternary Operator
##### Use Ternary When:
- Simple condition with `two` outcomes
- Assigning a value based on a `condition`
- Compact code is preferred (but still readable)
- `Initializing` variables conditionally

**Examples:**
**1.** Finding Maximum:

```java
int a = 10, b = 20;
int max = (a > b) ? a : b;
System.out.println("Max: " + max);
```

**2.** Setting Default Value:

```java
String username = getUserInput();
String displayName = (username != null) ? username : "Guest";
```

**3.** Conditional Calculation:

```java
int quantity = 50;
double price = (quantity > 100) ? 9.99 : 12.99;
```

**4.** Display Message:

```java
int score = 75;
System.out.println(score >= 50 ? "Pass" : "Fail");
```

---

#### 7.4 Nested Ternary Operator
You can nest ternary operators, but `avoid deep` nesting as it hurts readability.

**Example:**

```java
int marks = 85;
String grade = (marks >= 90) ? "A" :
               (marks >= 75) ? "B" :
               (marks >= 60) ? "C" : "F";
System.out.println("Grade: " + grade);
```

**Output:**

```java
Grade: B
```

**Better Approach for Complex Logic:**
Use `if-else` ladder or `switch` for better readability:

```java
String grade;
if (marks >= 90) {
    grade = "A";
} else if (marks >= 75) {
    grade = "B";
} else if (marks >= 60) {
    grade = "C";
} else {
    grade = "F";
}
```

---

#### 7.5 Ternary Operator vs if-else

|**Feature**|**Ternary Operator**|**if-else**|
|-----------|--------------------|-----------|
| **Compactness** | More compact | More verbose |
| **Readability** | Good for simple conditions | Better for complex logic |
| **Returns a value** | Yes (expression) | No (statement) |
| **Multiple statements** | Not supported | Supported |
| **Best for** | Assignment, simple choice | Complex logic, multiple actions |

---

#### 7.6 When NOT to Use Ternary:

```java
// BAD: Complex logic, hard to read
String result = (user != null && user.isActive() && user.hasPermission("read")) 
                ? "Access granted" 
                : "Access denied";

// BETTER: Use if-else
String result;
if (user != null && user.isActive() && user.hasPermission("read")) {
    result = "Access granted";
} else {
    result = "Access denied";
}
```

---

#### 7.7 Common Mistakes with Ternary Operator
##### 1. Type Mismatch:

```java
// Error: incompatible types
String result = (true) ? 1 : "Hello";  // int vs String
```

##### 2. Using Ternary for Side Effects:

```java
// BAD: Ternary is for returning values, not side effects
(score > 50) ? System.out.println("Pass") : System.out.println("Fail");

// GOOD: Use if-else for side effects
if (score > 50) {
    System.out.println("Pass");
} else {
    System.out.println("Fail");
}
```

##### 3. Excessive Nesting:

```java
// BAD: Hard to read
String grade = (m >= 90) ? "A" : (m >= 80) ? "B" : (m >= 70) ? "C" : (m >= 60) ? "D" : "F";

// GOOD: Use if-else or switch
```

---

#### 7.8 Real-World Use Cases
##### 1. Setting Configuration:

```java
boolean isProduction = true;
String apiUrl = isProduction ? "https://api.prod.com" : "https://api.dev.com";
```

##### 2. Null Safety:

```java
String name = user.getName();
String displayName = (name != null && !name.isEmpty()) ? name : "Anonymous";
```

##### 3. Conditional CSS Class:

```java
String cssClass = isActive ? "btn-primary" : "btn-disabled";
```

##### 4. Math Operations:

```java
int abs = (number >= 0) ? number : -number;  // Absolute value
```