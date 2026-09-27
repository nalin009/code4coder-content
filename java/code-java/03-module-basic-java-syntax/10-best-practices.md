## 10. Best Practices (5+ YOE Expectation)

---

#### Practice 1: Write Self-Documenting Code

```java
// BAD
int d; // days
d = calculateDays(startDate, endDate);

// GOOD
int daysBetweenDates = calculateDays(startDate, endDate);
```

**Why:** Reduces need for comments; code is clearer.

---

#### Practice 2: Use Javadoc for Public APIs

```java
/**
 * Calculates the area of a rectangle.
 * 
 * @param length the length of the rectangle (must be positive)
 * @param width the width of the rectangle (must be positive)
 * @return the area as length × width
 * @throws IllegalArgumentException if length or width is negative
 */
public double calculateArea(double length, double width) {
    if (length < 0 || width < 0) {
        throw new IllegalArgumentException("Dimensions must be positive");
    }
    return length * width;
}
```

---

#### Practice 3: Minimize Variable Scope

```java
// BAD
public void process() {
    int x = 0; // Declared too early
    // 50 lines of code
    x = computeValue();
    System.out.println(x);
}

// GOOD
public void process() {
    // 50 lines of code
    int x = computeValue(); // Declare close to usage
    System.out.println(x);
}
```

---

#### Practice 4: Use Constants for Magic Numbers

```java
// BAD
if (age > 18) { }

// GOOD
private static final int LEGAL_AGE = 18;
if (age > LEGAL_AGE) { }
```

---

#### Practice 5: Follow Java Naming Conventions
- **Classes:** UpperCamelCase (e.g., StudentRecord)
- **Methods/Variables:** lowerCamelCase (e.g., calculateTotal)
- **Constants:** UPPER_SNAKE_CASE (e.g., MAX_VALUE)
- **Packages:** lowercase (e.g., com.company.project)

---

#### Practice 6: Avoid Deep Nesting

```java
// BAD
if (condition1) {
    if (condition2) {
        if (condition3) {
            if (condition4) {
                // Code here
            }
        }
    }
}

// GOOD (early returns)
if (!condition1) return;
if (!condition2) return;
if (!condition3) return;
if (!condition4) return;
// Code here
```

---

#### Practice 7: Use Logging Frameworks in Production

```java
// BAD (production code)
System.out.println("User logged in: " + username);

// GOOD
logger.info("User logged in: {}", username); // SLF4J
```

**Why:** Logging frameworks offer log levels, formatting, file output, and performance optimizations.

---

#### Practice 8: Keep Methods Short and Focused
- **Single Responsibility Principle:** One method, one purpose
- **Typical length:** 10-20 lines (guideline, not rule)
- **Extract helper methods:** Break complex logic into smaller methods