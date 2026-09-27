## 8. First Java Program

---

#### 8.1 Writing the Program
###### **Create a file named `HelloWorld.java:`**

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

---

#### 8.2 Compiling the Program

```java
javac HelloWorld.java
```

###### **What Happens:**
- javac reads `HelloWorld.java`.
- Checks `syntax` and `types`.
- Generates `HelloWorld.class` (bytecode).

###### **Common Errors:**
- `javac: command not found` → `PATH` not set.
- `class HelloWorld is public, should be declared in a file named HelloWorld.java` → Filename must match `public class` name.

---

#### 8.3 Running the Program

```java
java HelloWorld
```

**What Happens**:
- JVM loads `HelloWorld.class`.
- Finds `main()` method (entry point).
- Executes instructions.

**Output**:

```java
Hello, World!
```

###### **Common Errors:**
- `Error: Could not find or load main class HelloWorld `→ CLASSPATH issue or wrong directory.
- `NoClassDefFoundError` → `.class` file not found.