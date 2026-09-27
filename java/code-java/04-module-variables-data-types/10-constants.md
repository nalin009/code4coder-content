## 10. Constants (Using final Keyword)

---

**Definition:** A variable whose value cannot be changed after initialization.

**Syntax:**

```java
final int MAX_USERS = 100;
```

**Naming Convention:** Use `UPPER_SNAKE_CASE` for constants.

**Example:**

```java
public class Config {
    public static final int TIMEOUT_SECONDS = 30;
    public static final String APP_NAME = "MyApp";
}
```

#### 10.1. Why Use Constants:
- **Readability:** TIMEOUT_SECONDS is clearer than 30
- **Maintainability:** Change the value in one place
- **Type safety:** Better than magic numbers

---

#### 10.2. Interview Insight:
- **Compile-time constants:** If a final variable is initialized with a literal, the compiler inlines it (replaces the variable with the value in bytecode). This is slightly faster but means changing the constant requires recompiling dependent classes.
- **Runtime constants:** If a final variable is initialized at runtime (e.g., final int x = calculate();), it's not inlined.

**Example:**

```java
public class A {
    public static final int X = 10; // Compile-time constant
}

public class B {
    int y = A.X; // Compiler inlines: int y = 10;
}
```

If you change A.X to 20 and recompile only A, class B still uses 10 unless you recompile it.