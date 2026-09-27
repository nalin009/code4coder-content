## 11. Wrapper Classes

---

**Definition:** Wrapper classes provide an object representation of primitive types.

#### 11.1. Why Wrapper Classes Exist:

1. **Collections:** Collections (like ArrayList, HashMap) can only store objects, not primitives.

```java
  // ArrayList<int> list; // Error: primitives not allowed
  ArrayList<Integer> list = new ArrayList<>(); // OK
```

2. **Null values:** Primitives cannot be null, but wrappers can.

```java
  Integer age = null; // Allowed
  // int age = null; // Error
```

3. **Utility methods:** Wrappers provide methods like `parseInt`, `toString`, `compareTo`.

---

#### 11.2. Wrapper Classes Table:

|**Primitive**|**Wrapper Class**|
|-------------|-----------------|
| byte | Byte |
| short | Short |
| int | Integer |
| long | Long |
| float | Float |
| double | Doble |
| char | Character |
| boolean | Boolean |

---

#### 11.3. Creating Wrapper Objects
##### Method 1: Using Constructor (Deprecated since Java 9)

```java
Integer num = new Integer(10); // Deprecated
```

##### Method 2: Using valueOf (Recommended)

```java
Integer num = Integer.valueOf(10); // Recommended
```

##### Method 3: Autoboxing (See next section)

```java
Integer num = 10; // Autoboxing
```

**Why Constructors Are Deprecated:** They always create a new object, even if an equivalent object exists in the cache. `valueOf` uses caching for better performance.

---

#### 11.4. Wrapper Class Caching
**Key Insight:** Wrapper classes cache frequently used values for performance.

##### Cached Ranges (JVM-dependent, but common across implementations):
- **Integer, Short, Byte, Long:** -128 to 127
- **Character:** 0 to 127
- **Boolean:** TRUE and FALSE (only two objects)

**Example:**

```java
Integer a = 100;
Integer b = 100;
System.out.println(a == b); // true (cached)

Integer c = 200;
Integer d = 200;
System.out.println(c == d); // false (not cached, different objects)
```

**Interview Insight:** Always use `.equals()` to compare wrapper objects, not `==`.

```java
Integer x = 200;
Integer y = 200;
System.out.println(x.equals(y)); // true (correct comparison)
```

**Note: The upper limit (127) can be increased using the JVM flag `-XX:AutoBoxCacheMax=<size>` (applicable only to Integer, not other wrappers). This is rarely used in production but is an interview edge case.**