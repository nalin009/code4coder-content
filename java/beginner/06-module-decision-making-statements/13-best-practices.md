## 13. Best Practices (5+ YOE Expectation)

---

#### 13.1. Always Use Braces

```java
// BAD
if (condition)
    statement;

// GOOD
if (condition) {
    statement;
}
```

Why: Prevents bugs when adding more statements later.

---

#### 13.2. Prefer Switch Expressions Over Traditional Switch (Java 14+)

```java
// OLD
String day;
switch (num) {
    case 1: day = "Monday"; break;
    case 2: day = "Tuesday"; break;
    default: day = "Invalid";
}

// MODERN
String day = switch (num) {
    case 1 -> "Monday";
    case 2 -> "Tuesday";
    default -> "Invalid";
};
```

---

#### 13.3. Use Switch for 5+ Discrete Values

```java
// Less efficient
if (status == 200) { }
else if (status == 201) { }
else if (status == 400) { }
else if (status == 401) { }
else if (status == 404) { }
else if (status == 500) { }

// Better
switch (status) {
    case 200, 201 -> handleSuccess();
    case 400, 401, 404 -> handleClientError();
    case 500 -> handleServerError();
}
```

---

#### 13.4. Use Ternary for Simple Assignments Only

```java
// GOOD: Simple, readable
int max = (a > b) ? a : b;

// BAD: Too complex
String result = (user != null && user.isActive() && user.hasRole("admin")) 
                ? "Full access" 
                : (user != null && user.isActive()) 
                  ? "Limited access" 
                  : "No access";

// BETTER: Use if-else
```

---

#### 13.5. Always Include default in Switch

```java
switch (value) {
    case 1 -> handle1();
    case 2 -> handle2();
    default -> logUnexpectedValue(value);  // Defensive programming
}
```

---

#### 13.6. Use Short-Circuit Evaluation for Safety

```java
// GOOD: Prevents NullPointerException
if (obj != null && obj.isValid()) { }

// BAD: Can throw NPE
if (obj.isValid() && obj != null) { }
```

---

#### 13.7. Avoid Magic Numbers - Use Constants

```java
// BAD
if (status == 200) { }

// GOOD
private static final int HTTP_OK = 200;
if (status == HTTP_OK) { }
```

---

#### 13.8. Document Intentional Fallthrough

```java
switch (x) {
    case 1:
        // Fallthrough intentional - shared logic for 1 and 2
    case 2:
        handleBoth();
        break;
}
```

---

#### 13.9. Prefer Positive Conditions

```java
// LESS READABLE
if (!isInvalid) {
    process();
}

// MORE READABLE
if (isValid) {
    process();
}
```

---

#### 13.10. Extract Complex Conditions to Methods

```java
// BAD
if (user != null && user.getAge() >= 18 && user.hasLicense() && user.getExperience() > 2) {
    allowDriving();
}

// GOOD
if (canDrive(user)) {
    allowDriving();
}

private boolean canDrive(User user) {
    return user != null 
        && user.getAge() >= 18 
        && user.hasLicense() 
        && user.getExperience() > 2;
}
```