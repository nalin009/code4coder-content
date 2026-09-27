## 4. Core Concept Explanation

---

#### 4.1. How Variables Work in Java
##### When you declare a variable:

```java
int age;
```

###### At compile-time:
- The compiler checks that age is used correctly (type-safe)
- The compiler doesn't allocate memory yet (for local variables)

###### At runtime:
- Primitive variables (like int age) are stored on the stack (for local variables) or heap (for instance variables)
- Reference variables (like String name) store a memory address pointing to an object on the heap

##### Variable Declaration vs Initialization
**Declaration:** Telling the compiler the variable's name and type. 

```java
int count; // Declaration only
```

**Initialization:** Assigning a value for the first time.

```java
count = 10; // Initialization
```

**Combined:**

```java
int count = 10; // Declaration + Initialization
```

**Critical Rule:** Local variables must be initialized before use, or you'll get a compile-time error. Instance and static variables are auto-initialized to default values (0, null, false).

---

#### 4.2. Why Java Designed It This Way
- **Type safety:** Declaring types prevents bugs (e.g., accidentally storing text in a number variable)
- **Memory efficiency:** Primitives are stored directly, avoiding object overhead
- **Performance:** Stack allocation is faster than heap allocation
- **Predictability:** Default initialization prevents garbage values (unlike C/C++)