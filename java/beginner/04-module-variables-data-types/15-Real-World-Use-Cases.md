## 15. Real-World Use Cases

---

#### 15.1. Beginner Use Cases

**15.1.1.** **Storing user input:**

```java
  Scanner sc = new Scanner(System.in);
  int age = sc.nextInt();    
```

**15.1.2.** **Simple calculations:**

```java
double total = price * quantity;
```

**15.1.3.** **Flags and conditions:**

```java
   boolean isLoggedIn = true;
```

---


#### 15.2. Interview Use Cases
**15.2.1.** **Wrapper class caching**:
   - "Explain why `Integer a = 100; Integer b = 100;` results in `a == b` being `true`, but not for 200."

**15.2.2.** **Autoboxing performance**:
   - "What's wrong with `Integer sum = 0; for (int i = 0; i < 1_000_000; i++) sum += i;`?"

**15.2.3.** **Type casting precision loss**:
   - "What happens when you cast a large `int` to `byte`?"

---

#### 15.3. Production Use Cases (3–5+ YOE)

**15.3.1.** **Database results**: Use wrappers (`Integer`, `Double`) to handle `NULL` values from databases.

```java
   Integer count = resultSet.getInt("count"); // Can be null
```

**15.3.2.** **Configuration management**: Use `final` constants for environment settings.

```java
   public static final int MAX_RETRIES = 3;
```

**15.3.3.** **Performance optimization**: Avoid autoboxing in hot loops (loops executed millions of times).

**15.3.4.** **Thread-safe counters**: Use `AtomicInteger` instead of `static int` for concurrent increments.