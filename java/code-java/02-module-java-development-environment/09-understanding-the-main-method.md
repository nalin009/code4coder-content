## 9. Understanding the main() Method

---

#### 9.1 Syntax Breakdown

```java
public static void main(String[] args) {
    // Code here
}
```

##### Each Keyword Explained:

###### public
- **Access Modifier:** Makes `main()` accessible from anywhere.
- **Why Needed:** The JVM (an external entity) must access `main()` to start execution.
- **Compiler Behavior:** If `main()` is private, code compiles but JVM throws runtime error: `Main method not found in class HelloWorld`.

###### static
- Belongs to the class, not an instance.
- **Why Needed:** JVM calls `main()` without creating an object. If `main()` were non-static, JVM would need to instantiate the class first (which creates a circular dependency problem).
- **Memory Behavior:** Static methods reside in Metaspace (Java 8+) or Method Area (Java 7 and earlier).

###### void
- Return Type: `main()` returns nothing.
- **Why Needed:** The JVM doesn't expect a return value. The program's exit status is controlled via `System.exit(int)`.

###### main
- **Method Name:** JVM specifically looks for a method named `main`.
- **Convention:** Must be exactly `main` (case-sensitive).

###### String[] args
- **Parameter:** `Array of String` arguments passed from the `command line`.
- **Why Needed:** Allows passing `input` to the program at `runtime`.

**Examples**

```java
java HelloWorld arg1 arg2 arg3
```

###### **Inside main():**

```java
args[0] = "arg1"
args[1] = "arg2"
args[2] = "arg3"
```

---

#### 9.2 JVM-Level Behavior
When you run `java HelloWorld`, the JVM:
1. Loads `HelloWorld.class` into memory (Heap).
2. Searches for `public static void main(String[] args)`.
3. If found, execution begins from the first line inside `main()`.
4. If NOT found, JVM throws: `Error: Main method not found in class HelloWorld`.

**Note:** Unchanged till Java 25: The signature of main() must be exactly as shown. Any deviation (like public void main(String[] args)) causes runtime error.