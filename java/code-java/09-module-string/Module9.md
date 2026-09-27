## Strings

---
---

### Summary
Strings are the most frequently used reference type in Java programming, present in virtually every application. Understanding how strings work at both the language level and JVM level is critical for writing efficient, maintainable code.

**Key takeaways**:

1. **Immutability is foundational** - it enables String Pooling, thread safety, and security. Every "modification" creates a new object.

2. **String Pool optimization** - Java's design minimizes memory usage by reusing string literals, but this requires understanding when strings are pooled versus heap-allocated.

3. **Performance matters** - in loops or high-frequency operations, choosing `StringBuilder` over naive string concatenation can mean the difference between milliseconds and seconds of execution time.

4. **Reference vs content comparison** - `==` checks memory addresses, `.equals()` checks content. This distinction causes countless bugs in production code.

5. **JVM evolution** - from Java 7's String Pool migration to the heap, to Java 9's concatenation improvements, the JVM continues to optimize string handling. These optimizations remain effective through Java 25.

For beginners, mastering string fundamentals means understanding immutability and common methods. For intermediate developers, it means knowing when to use `StringBuilder` and how the String Pool works. For senior developers (3-5+ years), it means understanding JVM internals, performance implications, memory management, and making architecture-level decisions about string handling in large-scale systems.

Whether you're building a simple console application or a high-throughput web service, proper string handling is non-negotiable. The concepts in this chapter form the foundation for text processing, data parsing, user interface development, API design, and countless other programming tasks.

---
---

### 1. Introduction

#### Why This Topic Exists
Text manipulation is one of the most fundamental operations in programming. Nearly every application—from web servers to mobile apps—processes user input, displays messages, logs information, or communicates with external systems using text. Java introduced the String class to provide a robust, secure, and efficient way to handle textual data.
Unlike primitive types such as int or char, strings are objects in Java, which means they come with powerful built-in methods for manipulation, comparison, and transformation. The String class is immutable by design, meaning once created, its content cannot be changed. This immutability provides thread safety, security, and performance optimizations like string pooling.

#### What Problem Java Is Solving
Before Java's String class and string pooling mechanism, handling text was error-prone and memory-intensive. Java addresses several key challenges:
- Memory Efficiency: Java uses a String Pool (a special memory region in the heap) to store string literals. When you create multiple string literals with the same content, Java reuses the same object, saving memory.
- Thread Safety: Since strings are immutable, they can be safely shared across multiple threads without synchronization overhead.
- Security: Immutability prevents malicious code from modifying strings used in security-sensitive operations like file paths, database connections, or network URLs.
- Performance: String interning and pooling reduce memory allocation overhead and enable fast string comparison using reference equality.

#### Why Beginners Struggle With This Topic
Beginners often find strings confusing because:
1. Immutability is counterintuitive: When you "modify" a string, you're actually creating a new object. This leads to confusion about memory consumption.
2. String Pool vs Heap confusion: Understanding when strings go into the pool versus the regular heap requires knowledge of JVM internals.
3. Multiple ways to create strings: Using literals ("hello"), the new keyword, concatenation, or StringBuilder creates strings differently, with different memory implications.
4. Reference vs value comparison: Using == compares references (memory addresses), while .equals() compares content. This distinction trips up many beginners.
5. Performance pitfalls: String concatenation in loops creates many unnecessary objects, causing performance degradation that isn't immediately obvious.

#### Why Interviewers Ask This (Especially 3–5+ Years Experience)
For experienced developers, string-related questions reveal:
- JVM Understanding: Questions about String Pool, intern() method, and memory allocation assess deep JVM knowledge.
- Performance Optimization Skills: Knowing when to use String, StringBuilder, or StringBuffer demonstrates awareness of performance implications in production code.
- Thread Safety Awareness: Understanding why StringBuffer is synchronized and when to use it shows knowledge of concurrent programming.
- Memory Management: String-related questions expose understanding of heap memory, garbage collection, and memory leaks caused by excessive string creation.
- Code Quality: Proper string handling indicates attention to code efficiency, maintainability, and best practices.
In production systems, inefficient string handling can cause memory bloat, slow response times, and even OutOfMemoryError crashes. Senior developers are expected to write code that scales.

---
---

### 2. Clear Definitions
#### What is a String?
**Simple Definition:** A String is a sequence of characters treated as a single unit in Java. It is an object of the String class, which is part of the java.lang package.

**Technical Definition:** A String is an immutable object that represents a character array internally. Once a String object is created, its value cannot be changed. Any operation that appears to modify a string actually creates a new String object.

**Interview-Safe Wording:** "A String in Java is an immutable sequence of characters represented by the java.lang.String class. It is stored as an object in the heap memory and provides numerous methods for text manipulation. String literals are stored in a special memory area called the String Pool for memory optimization."

#### Key Characteristics
- Immutable: Content cannot be changed after creation
- Final class: Cannot be subclassed (the String class is declared as final)
- Thread-safe: Can be safely shared across threads without synchronization
- Implements interfaces: Implements Serializable, Comparable, and CharSequence
- Backed by char array: Internally uses a character array (or byte array in Java 9+)

---
---

### 3. Core Concept Explanation
#### 3.1 String Creation Methods
There are two primary ways to create strings in Java:

##### Method 1: String Literal

```java
String s1 = "Hello";
```

###### What happens at compile time:
- The compiler identifies "Hello" as a string literal
- The literal is added to the class file's constant pool

###### What happens at runtime:
- The JVM checks the String Pool (a special area in heap memory) to see if "Hello" already exists
- If it exists, s1 references the existing object
- If it doesn't exist, a new String object is created in the String Pool, and s1 references it

Why Java designed it this way: String literals are common in code. By pooling them, Java saves memory and enables fast equality checks using reference comparison.

##### Method 2: Using new Keyword

```java
String s2 = new String("Hello");
```

###### What happens at runtime:
- First, "Hello" (the literal inside new String()) is checked in the String Pool (created if not present)
- Then, a new String object is explicitly created in the heap memory (outside the pool)
- s2 references this new heap object, not the pooled one
- Result: Two objects exist—one in the pool, one in the heap

**Why this matters:** Using new bypasses string pooling and creates duplicate objects, consuming more memory. This is rarely necessary in production code.

#### 3.2 String Pool (String Constant Pool)
**What it is:** The String Pool is a special memory region in the Java heap that stores string literals to optimize memory usage.

##### JVM-level behavior:
- Prior to Java 7: String Pool was in PermGen (Permanent Generation) space
- From Java 7 onwards: String Pool is in the heap memory
- This remains unchanged till Java 25

##### How it works:
1. When you create a string literal, the JVM first checks if an identical string exists in the pool
2. If found, it returns a reference to the existing object (no new object created)
3. If not found, it creates a new string in the pool

##### Memory benefit example:

```java
String s1 = "Java";
String s2 = "Java";
String s3 = "Java";
// Only ONE object created in String Pool
// s1, s2, s3 all point to the same object
```

Without string pooling, three separate objects would be created, tripling memory usage.

#### 3.3 String Immutability
**What immutability means:** Once a String object is created, its internal character array cannot be modified.

##### Why Java made Strings immutable:
1. String Pool optimization: If strings were mutable, changing one reference would affect all references pointing to the same pooled object, breaking the pool's reliability.
2. Thread Safety: Immutable objects are inherently thread-safe. Multiple threads can access the same string without synchronization.
3. Security: Strings are used in sensitive operations (file paths, database connections, network URLs). Immutability prevents malicious modification.
4. Hashcode caching: Since strings are immutable, their hashcode can be calculated once and cached, making them ideal for use as HashMap keys.

##### Example demonstrating immutability:

```java
String s = "Hello";
s.concat(" World");  // Creates a new string, but we don't store it
System.out.println(s);  // Output: Hello (unchanged)

s = s.concat(" World");  // Now we store the new string
System.out.println(s);  // Output: Hello World
```

##### What happens in memory:
- Original string "Hello" remains unchanged in memory
- concat() creates a new String object "Hello World"
- If we don't assign the result, the new object becomes eligible for garbage collection
- When we assign s = s.concat(" World"), s now references the new object

#### 3.4 Compiler Optimization for String Literals
##### Compile-time concatenation:

```java
String s1 = "Hello" + " " + "World";  // Compile-time
String s2 = "Hello World";
System.out.println(s1 == s2);  // true
```

**Why this is true:** The Java compiler optimizes string literal concatenation at compile time. It converts "Hello" + " " + "World" into "Hello World" before the bytecode is generated. Both s1 and s2 reference the same pooled object.

##### Runtime concatenation (no optimization):

```java
String part = "Hello";
String s3 = part + " World";  // Runtime concatenation
System.out.println(s3 == s2);  // false
```

Here, s3 is created at runtime (not in the pool initially), so it's a different object.

#### 3.5 String Comparison

Using == (Reference Comparison)

Compares memory addresses (references), not content.

```java
String s1 = "Java";
String s2 = "Java";
String s3 = new String("Java");

System.out.println(s1 == s2);  // true (same pool object)
System.out.println(s1 == s3);  // false (different objects)
```

Using .equals() (Content Comparison)

Compares the actual character sequence.

```java
System.out.println(s1.equals(s3));  // true (same content)
```

**Interview insight:** Always use .equals() for string comparison in production code. Using == is a common source of bugs.

---
---

### 4. String Methods
The String class provides over 60 methods. Here are the most important ones:

#### 4.1 Length and Character Access
int length(): Returns the number of characters in the string.

```java
String s = "Hello";
System.out.println(s.length());  // 5
```

char charAt(int index): Returns the character at the specified index (0-based).

```java
System.out.println(s.charAt(0));  // 'H'
System.out.println(s.charAt(4));  // 'o'
// s.charAt(5) throws StringIndexOutOfBoundsException
```


#### 4.2 String Comparison Methods
boolean equals(Object obj): Compares content (case-sensitive).

```java
String s1 = "Java";
String s2 = "Java";
String s3 = "java";
System.out.println(s1.equals(s2));  // true
System.out.println(s1.equals(s3));  // false
```

boolean equalsIgnoreCase(String another): Compares content (case-insensitive).

```java
System.out.println(s1.equalsIgnoreCase(s3));  // true
```

int compareTo(String another): Lexicographically compares strings.
- Returns 0 if equal
- Returns negative if current string comes before
- Returns positive if current string comes after

```java
String s1 = "Apple";
String s2 = "Banana";
System.out.println(s1.compareTo(s2));  // Negative (Apple < Banana)
System.out.println(s2.compareTo(s1));  // Positive (Banana > Apple)
System.out.println(s1.compareTo("Apple"));  // 0 (equal)
```

#### 4.3 Searching Methods
boolean contains(CharSequence seq): Checks if string contains a sequence.

```java
String s = "Hello World";
System.out.println(s.contains("World"));  // true
System.out.println(s.contains("world"));  // false (case-sensitive)
```

boolean startsWith(String prefix): Checks if string starts with prefix.

```java
System.out.println(s.startsWith("Hello"));  // true
```

boolean endsWith(String suffix): Checks if string ends with suffix.

```java
System.out.println(s.endsWith("World"));  // true
```

int indexOf(String str): Returns first occurrence index (or -1 if not found)

```java
System.out.println(s.indexOf("o"));  // 4 (first 'o')
System.out.println(s.indexOf("World"));  // 6
System.out.println(s.indexOf("xyz"));  // -1
```

int lastIndexOf(String str): Returns last occurrence index.

```java
System.out.println(s.lastIndexOf("o"));  // 7 (last 'o')
```

#### 4.4 Substring Methods
String substring(int beginIndex): Returns substring from beginIndex to end.

```java
String s = "Hello World";
System.out.println(s.substring(6));  // "World"
```

String substring(int beginIndex, int endIndex): Returns substring from beginIndex to endIndex-1.

```java
System.out.println(s.substring(0, 5));  // "Hello"
System.out.println(s.substring(6, 11));  // "World"
```

Important: endIndex is exclusive. The character at endIndex is NOT included.

#### 4.5 Modification Methods (Return New Strings)
String concat(String str): Concatenates strings.

```java
String s1 = "Hello";
String s2 = s1.concat(" World");
System.out.println(s2);  // "Hello World"
System.out.println(s1);  // "Hello" (unchanged)
```

String replace(char oldChar, char newChar): Replaces all occurrences.

```java
String s = "Hello";
System.out.println(s.replace('l', 'p'));  // "Heppo"
```

String replace(CharSequence target, CharSequence replacement): Replaces substring.

```java
String s = "Java is great. Java is powerful.";
System.out.println(s.replace("Java", "Python"));
// "Python is great. Python is powerful."
```

String toLowerCase(): Converts to lowercase.

```java
String s = "Hello World";
System.out.println(s.toLowerCase());  // "hello world"
```

String toUpperCase(): Converts to uppercase.

```java
System.out.println(s.toUpperCase());  // "HELLO WORLD"
```

String trim(): Removes leading and trailing whitespace.

```java
String s = "  Hello World  ";
System.out.println(s.trim());  // "Hello World"
```

Note: trim() only removes ASCII whitespace (space, tab, newline). For Unicode whitespace, use strip() (Java 11+).

#### 4.6 Splitting and Joining (Java 8+)
String[] split(String regex): Splits string by delimiter.

```java
String s = "Java,Python,C++";
String[] languages = s.split(",");
// languages = ["Java", "Python", "C++"]
```

static String join(CharSequence delimiter, CharSequence... elements): Joins strings.

```java
String joined = String.join("-", "Java", "Python", "C++");
System.out.println(joined);  // "Java-Python-C++"
```

#### 4.7 Type Conversion Methods
static String valueOf(int i): Converts primitive to string.

```java
String s1 = String.valueOf(100);  // "100"
String s2 = String.valueOf(true);  // "true"
String s3 = String.valueOf(3.14);  // "3.14"
```

char[] toCharArray(): Converts string to character array.

```java
String s = "Hello";
char[] chars = s.toCharArray();
// chars = ['H', 'e', 'l', 'l', 'o']
```

byte[] getBytes(): Converts string to byte array (useful for encoding).

```java
String s = "Hello";
byte[] bytes = s.getBytes();
```

#### 4.8 Modern String Methods (Java 11+)
Java 11 introduced several convenient string methods that enhance text processing capabilities. These methods remain available through Java 25.
boolean isBlank() (Java 11)
Checks if a string is empty or contains only whitespace characters.

```java
String s1 = "";
String s2 = "   ";
String s3 = "  \t  \n  ";
String s4 = "Hello";

System.out.println(s1.isBlank());  // true (empty)
System.out.println(s2.isBlank());  // true (only spaces)
System.out.println(s3.isBlank());  // true (whitespace: spaces, tabs, newlines)
System.out.println(s4.isBlank());  // false (has content)
```

Difference from isEmpty():

```java
String s = "   ";
System.out.println(s.isEmpty());   // false (has characters, even if spaces)
System.out.println(s.isBlank());   // true (whitespace considered blank)
```

Use case: Form validation where whitespace-only input should be rejected.

```java
public boolean isValidInput(String userInput) {
    return userInput != null && !userInput.isBlank();
}
```

Stream<String> lines() (Java 11)
Returns a stream of lines extracted from the string, split by line terminators (\n, \r, or \r\n).

```java
String multiLine = "First line\nSecond line\nThird line";

multiLine.lines()
         .forEach(System.out::println);
/*
Output:
First line
Second line
Third line
*/

// Count non-empty lines
long count = multiLine.lines()
                      .filter(line -> !line.isBlank())
                      .count();
System.out.println("Non-empty lines: " + count);
```

Use case: Processing log files, configuration files, or CSV data.

```java
public List<String> parseConfigFile(String content) {
    return content.lines()
                  .map(String::trim)
                  .filter(line -> !line.isEmpty() && !line.startsWith("#"))
                  .collect(Collectors.toList());
}
```

String strip(), String stripLeading(), String stripTrailing() (Java 11)
Removes whitespace from string, with support for Unicode whitespace characters (unlike trim() which only handles ASCII).

```java
String s = "  Hello World  ";

// All three methods:
System.out.println(s.trim());           // "Hello World" (ASCII whitespace)
System.out.println(s.strip());          // "Hello World" (Unicode whitespace)
System.out.println(s.stripLeading());   // "Hello World  " (left side only)
System.out.println(s.stripTrailing());  // "  Hello World" (right side only)
```

Unicode whitespace example:

```java
// Unicode whitespace: \u2000 (EN QUAD)
String unicode = "\u2000 Hello \u2000";

System.out.println("'" + unicode.trim() + "'");   // '  Hello  ' (doesn't remove Unicode spaces)
System.out.println("'" + unicode.strip() + "'");  // 'Hello' (removes Unicode spaces)
```

Use case: Internationalized applications where user input may contain Unicode whitespace.

```java
public String sanitizeInput(String input) {
    return input == null ? "" : input.strip();
}
```

String repeat(int count) (Java 11)
Returns a string whose value is the concatenation of this string repeated count times.

```java
String s = "Java";
System.out.println(s.repeat(3));  // "JavaJavaJava"

String dash = "-";
System.out.println(dash.repeat(50));  // "--------------------------------------------------"

String space = " ";
System.out.println("Hello" + space.repeat(5) + "World");  // "Hello     World"
```

Use case: Creating separators, padding, or patterns.

```java
public String createTableBorder(int width) {
    return "+" + "-".repeat(width) + "+";
}

public void printSeparator(int length) {
    System.out.println("=".repeat(length));
}

// Example:
System.out.println(createTableBorder(20));
// Output: +--------------------+

printSeparator(50);
// Output: ==================================================
```

Practical example - Creating formatted output:

```java
public String formatTableRow(String label, String value, int labelWidth, int valueWidth) {
    String paddedLabel = label + " ".repeat(labelWidth - label.length());
    String paddedValue = value + " ".repeat(valueWidth - value.length());
    return "| " + paddedLabel + " | " + paddedValue + " |";
}

// Usage:
System.out.println(formatTableRow("Name", "John Doe", 15, 20));
System.out.println(formatTableRow("Age", "30", 15, 20));
/*
Output:
| Name            | John Doe             |
| Age             | 30                   |
*/
```

String indent(int n) (Java 12)
Adjusts the indentation of each line by adding or removing leading whitespace.

```java
String text = "Line 1\nLine 2\nLine 3";

// Add 4 spaces indentation
String indented = text.indent(4);
System.out.println(indented);
/*
    Line 1
    Line 2
    Line 3
*/

// Remove 2 spaces indentation
String code = "    int x = 10;\n    int y = 20;";
String dedented = code.indent(-2);
System.out.println(dedented);
/*
  int x = 10;
  int y = 20;
*/
```

Use case: Formatting code output, generating configuration files.

```java
public String formatJavaMethod(String methodBody) {
    return "public void myMethod() {\n" +
           methodBody.indent(4) +
           "}";
}

// Usage:
String body = "int x = 10;\nSystem.out.println(x);";
System.out.println(formatJavaMethod(body));
/*
Output:
public void myMethod() {
    int x = 10;
    System.out.println(x);
}
*/
```

String transform(Function<String, R> f) (Java 12)
Applies a function to the string and returns the result. Useful for method chaining.

```java
String result = "  hello world  "
    .transform(String::strip)
    .transform(String::toUpperCase)
    .transform(s -> s.replace(" ", "_"));

System.out.println(result);  // "HELLO_WORLD"
```

Use case: Creating clean, readable transformation pipelines.

```java
public String processUserInput(String input) {
    return input.transform(s -> s == null ? "" : s)
                .transform(String::strip)
                .transform(String::toLowerCase)
                .transform(s -> s.replaceAll("[^a-z0-9]", ""));
}

// Usage:
System.out.println(processUserInput("  Hello@123!  "));  // "hello123"
```

##### Comparison Table: Old vs New Methods

|**Old Method**|**New Method (Java 11+)**|**Improvement**|
|--------------|-------------------------|---------------|
| trim() | strip() | Handles Unicode whitespace |
| N/A | stripLeading() | Remove left whitespace only |
| N/A | stripTrailing() | Remove Right whitespace only |
| isEmpty() | isBlank() | Considers whitespace as empty |
| split("\n") | lines() | Returns Stream, handles all line terminators |
| Manual loop | repeat(n) | Built-in string repetition |
| N/A | indent(n) | Easy indentation control |
| Manual chaining | transform() | Cleaner transformation pipeline |

##### Real-World Example: Processing Multi-line Text

```java
public class TextProcessor {
    public static String cleanAndFormat(String rawText) {
        if (rawText == null || rawText.isBlank()) {
            return "";
        }
        
        return rawText.lines()                          // Split into lines
                      .map(String::strip)                // Remove whitespace from each line
                      .filter(line -> !line.isBlank())   // Remove empty lines
                      .map(line -> "• " + line)          // Add bullet points
                      .collect(Collectors.joining("\n")) // Join back
                      .indent(2);                        // Indent the whole block
    }
    
    public static void main(String[] args) {
        String input = """
            First item
            
            Second item
            Third item
            
            """;
        
        System.out.println(cleanAndFormat(input));
        /*
        Output:
          • First item
          • Second item
          • Third item
        */
    }
}
```

##### Performance Note
These new methods are optimized at the JVM level and often perform better than manual implementations using loops or regular expressions. For example, repeat() is more efficient than using a loop to concatenate strings.


#### 4.9 String Formatting (String.format() and Printf-Style)
String formatting allows you to create formatted strings using placeholders and arguments, similar to C's printf function.

Basic Syntax

```java
String formatted = String.format(format_string, arguments);
```

##### Common Format Specifiers

|**Specifier**|**Type**|**Description**|**Example**|
|-------------|--------|---------------|-----------|
| **`%s`** | String | String value | String.format("Hello %s", "World") → "Hello World" |
| **`%d`** | Integer | Decimal integer | String.format("Age: %d", 25) → "Age: 25" |
| **`%f`** | Float/Double | Floating-point | String.format("Price: %.2f", 19.99) → "Price: 19.99" |
| **`%c`** | Character | Single character | String.format("Grade: %c", 'A') → "Grade: A" |
| **`%b`** | Boolean | Boolean value | String.format("Active: %b", true) → "Active: true" |
| **`%x`** | Integer | Hexadecimal | String.format("Hex: %x", 255) → "Hex: ff" |
| **`%o`** | Integer | Octal | String.format("Octal: %o", 8) → "Octal: 10" |
| **`%n`** | N/A | Platform line separator | String.format("Line1%nLine2") |

##### Basic Examples

```java
// String formatting
String name = "Alice";
int age = 30;
String message = String.format("Name: %s, Age: %d", name, age);
System.out.println(message);  // "Name: Alice, Age: 30"

// Floating-point precision
double price = 19.99;
System.out.println(String.format("Price: $%.2f", price));  // "Price: $19.99"

// Multiple arguments
String result = String.format("%s scored %d out of %d (%.1f%%)", 
                               "John", 85, 100, 85.0);
System.out.println(result);  // "John scored 85 out of 100 (85.0%)"
```

##### Width and Alignment
###### Right-aligned (default for numbers):

```java
System.out.println(String.format("|%10s|", "Hello"));      // "|     Hello|"
System.out.println(String.format("|%10d|", 42));           // "|        42|"
```
###### Left-aligned (use - flag):
```java
System.out.println(String.format("|%-10s|", "Hello"));     // "|Hello     |"
System.out.println(String.format("|%-10d|", 42));          // "|42        |"
```

###### Zero-padding:

```java
System.out.println(String.format("%05d", 42));             // "00042"
System.out.println(String.format("%08.2f", 123.4));        // "00123.40"
```

##### Precision Control
###### Decimal places for floating-point:

```java
double pi = 3.14159265359;
System.out.println(String.format("%.2f", pi));   // "3.14"
System.out.println(String.format("%.4f", pi));   // "3.1416"
System.out.println(String.format("%.0f", pi));   // "3"
```

###### Maximum width for strings:

```java
String longText = "This is a long string";
System.out.println(String.format("%.10s", longText));  // "This is a " (truncated)
```

##### Argument Indexing
###### Reuse or reorder arguments:

```java
// Reuse same argument
String s1 = String.format("%1$s is %1$s", "Java");
System.out.println(s1);  // "Java is Java"

// Reorder arguments
String s2 = String.format("%2$s, %1$s!", "World", "Hello");
System.out.println(s2);  // "Hello, World!"

// Mixed
String s3 = String.format("%1$s costs $%2$.2f. Buy %1$s now!", "Product", 29.99);
System.out.println(s3);  // "Product costs $29.99. Buy Product now!"
```

##### Flags Summary

|**Flag**|**Description**|**Example**|
|--------|---------------|-----------|
| **`-`** | Left-justify | "%-10s" |
| **`+`** | Include sign for numbers | "%+d" → "+42" |
| **`0`** | Zero-padding | "%05d" → "00042" |
| **`,`** | Grouping separator | "%,d" → "1,000,000" |
| **`(`** | Negative numbers in parentheses | "%(d" → "(42)" for -42 |

##### Real-World Examples
###### Example 1: Formatting currency:

```java
public String formatCurrency(double amount) {
    return String.format("$%,.2f", amount);
}

System.out.println(formatCurrency(1234567.89));  // "$1,234,567.89"
```

###### Example 2: Creating formatted tables:

```java
public void printTable(List<String[]> data) {
    // Header
    System.out.println(String.format("| %-15s | %-10s | %10s |", "Name", "Role", "Salary"));
    System.out.println(String.format("| %s | %s | %s |", 
                                      "-".repeat(15), "-".repeat(10), "-".repeat(10)));
    
    // Rows
    for (String[] row : data) {
        System.out.println(String.format("| %-15s | %-10s | $%,9.2f |", 
                                          row[0], row[1], Double.parseDouble(row[2])));
    }
}

// Usage:
List<String[]> employees = Arrays.asList(
    new String[]{"Alice Johnson", "Developer", "75000"},
    new String[]{"Bob Smith", "Designer", "65000"},
    new String[]{"Charlie Brown", "Manager", "95000"}
);

printTable(employees);
/*
Output:
| Name            | Role       |     Salary |
| --------------- | ---------- | ---------- |
| Alice Johnson   | Developer  | $75,000.00 |
| Bob Smith       | Designer   | $65,000.00 |
| Charlie Brown   | Manager    | $95,000.00 |
*/
```

###### Example 3: Formatted log messages:

```java
public String createLogEntry(String level, String module, String message) {
    LocalDateTime now = LocalDateTime.now();
    DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
    
    return String.format("[%s] [%-5s] [%-15s] %s", 
                         now.format(formatter), 
                         level, 
                         module, 
                         message);
}

// Usage:
System.out.println(createLogEntry("INFO", "AuthService", "User logged in"));
System.out.println(createLogEntry("ERROR", "Database", "Connection timeout"));
/*
Output:
[2026-02-24 10:30:45] [INFO ] [AuthService    ] User logged in
[2026-02-24 10:30:46] [ERROR] [Database       ] Connection timeout
*/
```

###### Example 4: Formatted reports:

```java
public void printSalesReport(String product, int unitsSold, double revenue) {
    String report = String.format("""
        ========== SALES REPORT ==========
        Product     : %s
        Units Sold  : %,d
        Revenue     : $%,.2f
        Avg Price   : $%.2f
        ==================================
        """,
        product,
        unitsSold,
        revenue,
        revenue / unitsSold
    );
    
    System.out.println(report);
}

// Usage:
printSalesReport("Laptop", 1250, 1562500.00);
/*
Output:
========== SALES REPORT ==========
Product     : Laptop
Units Sold  : 1,250
Revenue     : $1,562,500.00
Avg Price   : $1250.00
==================================
*/
```

System.out.printf() - Direct Console Formatting
Instead of creating a formatted string, you can print directly:

```java
String name = "Alice";
int age = 30;
double salary = 75000.50;

System.out.printf("Employee: %s, Age: %d, Salary: $%.2f%n", name, age, salary);
// Output: Employee: Alice, Age: 30, Salary: $75000.50
```
Note: printf() does not return a string; it directly outputs to the console. Use String.format() when you need to store or pass the formatted string.

##### Common Pitfalls
###### 1. Mismatched arguments:

```java
// WRONG - Runtime error: MissingFormatArgumentException
String.format("%s is %d years old", "Alice");  // Missing second argument

// CORRECT
String.format("%s is %d years old", "Alice", 30);
```

###### 2. Wrong type:

```java
// WRONG - Runtime error: IllegalFormatConversionException
String.format("%d", "123");  // String provided for %d (integer)

// CORRECT
String.format("%d", 123);
// OR convert first:
String.format("%d", Integer.parseInt("123"));
```

###### 3. Forgetting precision for floating-point:

```java
// May show unexpected precision
System.out.println(String.format("%f", 19.99));  // "19.990000"

// Better - specify precision
System.out.println(String.format("%.2f", 19.99));  // "19.99"
```

##### When to Use String.format()
###### Use it when:
- Creating formatted reports, tables, or logs
- Need consistent formatting across multiple strings
- Working with currency, percentages, or scientific notation
- Generating dynamic messages with multiple variables

###### Avoid it when:
- Simple concatenation is clearer: "Hello " + name is better than String.format("Hello %s", name)
- Performance is critical in tight loops (StringBuilder is faster)
- You only need to output once (use printf() instead)

#### 4.10 Regular Expressions (Regex) Basics
Regular expressions (regex) provide a powerful way to search, match, and manipulate strings based on patterns. Java provides regex support through the java.util.regex package and String methods.

String Methods Supporting Regex

```java
boolean matches(String regex)          // Check if entire string matches pattern
String replaceAll(String regex, String replacement)  // Replace all matches
String replaceFirst(String regex, String replacement)  // Replace first match
String[] split(String regex)           // Split string by pattern
```

##### Basic Regex Patterns

|**Pattern**|**Meaning**|**Example**|
|-----------|-----------|-----------|
| **`.`** | Any single character | "a.c" matches "abc", "a9c", "a c" |
| **`*`** | Zero or more of previous | "ab*c" matches "ac", "abc", "abbc" |
| **`+`** | One or more of previous | "ab+c" matches "abc", "abbc" (not "ac") |
| **`?`** | Zero or one of previous | "ab?c" matches "ac", "abc" |
| **`^`** | Start of string | "^Hello" matches strings starting with "Hello" |
| **`$`** | End of string | "world$" matches strings ending with "world" |
| **`[]`** | Character class | "[abc]" matches "a", "b", or "c" |
| **`[^]`** | Negated character class | "[^0-9]" matches non-digits |
| **`\d`** | Digit (0-9) | "\\d+" matches "123", "4567" |
| **`\D`** | Non-digit | "\\D+" matches "abc", "xyz" |
| **`\w`** | Word character (a-z, A-Z, 0-9, _) | "\\w+" matches "hello123" |
| **`\W`** | Non-word character | "\\W+" matches "@#$" |
| **`\s`** | Whitespace | "\\s+" matches spaces, tabs, newlines |
| **`\S`** | Non-whitespace | "\\S+" matches "text" |
| **`{n}`** | Exactly n occurrences | "\\d{3}" matches "123" |
| **`{n,}`** | At least n occurrences | "\\d{2,}" matches "12", "123", "1234" |
| **`{n,m}`** | Between n and m | "\\d{2,4}" matches "12", "123", "1234" |
| **`\|`** | OR |  |
| **`()`** | Grouping | "(ab)+" matches "ab", "abab", "ababab" |


##### Example 1: Validating Input with matches()
###### Email validation (simplified):

```java
public boolean isValidEmail(String email) {
    if (email == null) {
        return false;
    }
    
    // Simple pattern: username@domain.extension
    String emailPattern = "^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}$";
    return email.matches(emailPattern);
}

// Test:
System.out.println(isValidEmail("user@example.com"));     // true
System.out.println(isValidEmail("user.name@domain.co.in")); // true
System.out.println(isValidEmail("invalid.email"));        // false
System.out.println(isValidEmail("@example.com"));         // false
```

###### Phone number validation:

```java
public boolean isValidPhoneNumber(String phone) {
    if (phone == null) {
        return false;
    }
    
    // Pattern: (123) 456-7890 or 123-456-7890 or 1234567890
    String phonePattern = "^(\\(\\d{3}\\) |\\d{3}-)?\\d{3}-?\\d{4}$";
    return phone.matches(phonePattern);
}

// Test:
System.out.println(isValidPhoneNumber("(123) 456-7890"));  // true
System.out.println(isValidPhoneNumber("123-456-7890"));    // true
System.out.println(isValidPhoneNumber("1234567890"));      // true
System.out.println(isValidPhoneNumber("12-345-6789"));     // false
```

###### Password strength (at least one uppercase, one lowercase, one digit, min 8 characters):


```java
public boolean isStrongPassword(String password) {
    if (password == null) {
        return false;
    }
    
    // At least 8 chars, 1 uppercase, 1 lowercase, 1 digit
    String passwordPattern = "^(?=.*[a-z])(?=.*[A-Z])(?=.*\\d).{8,}$";
    return password.matches(passwordPattern);
}

// Test:
System.out.println(isStrongPassword("Pass1234"));     // true
System.out.println(isStrongPassword("password"));     // false (no uppercase/digit)
System.out.println(isStrongPassword("Pass"));         // false (too short)
```

##### Example 2: Replacing with replaceAll()
###### Remove all digits:

```java
String text = "User123 has 456 points";
String result = text.replaceAll("\\d+", "");
System.out.println(result);  // "User has  points"
```

###### Mask credit card number (show only last 4 digits):

```java
String cardNumber = "1234-5678-9012-3456";
String masked = cardNumber.replaceAll("\\d(?=\\d{4})", "*");
System.out.println(masked);  // "****-****-****-3456"
```

###### Replace multiple spaces with single space:

```java
String text = "Hello    World   !";
String normalized = text.replaceAll("\\s+", " ");
System.out.println(normalized);  // "Hello World !"
```

###### Remove HTML tags:

```java
String html = "<p>Hello <b>World</b>!</p>";
String plainText = html.replaceAll("<[^>]+>", "");
System.out.println(plainText);  // "Hello World!"
```

##### Example 3: Splitting with split()
###### Split by comma:

```java
String csv = "Java,Python,C++,JavaScript";
String[] languages = csv.split(",");
// Result: ["Java", "Python", "C++", "JavaScript"]
```

###### Split by multiple delimiters (comma, semicolon, or space):

```java
String data = "Java,Python;C++ JavaScript";
String[] parts = data.split("[,; ]+");
// Result: ["Java", "Python", "C++", "JavaScript"]
```

###### Split by whitespace:

```java
String sentence = "Hello   World   from    Java";
String[] words = sentence.split("\\s+");
// Result: ["Hello", "World", "from", "Java"]
```

##### Using Pattern and Matcher Classes (Advanced)
###### For more control, use Pattern and Matcher from java.util.regex:

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

// Find all email addresses in text
String text = "Contact us: support@example.com or sales@company.org";
Pattern pattern = Pattern.compile("[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}");
Matcher matcher = pattern.matcher(text);

while (matcher.find()) {
    System.out.println("Found: " + matcher.group());
}
/*
Output:
Found: support@example.com
Found: sales@company.org
*/
```

###### Extract phone numbers:

```java
String text = "Call us at (123) 456-7890 or 987-654-3210";
Pattern pattern = Pattern.compile("\\(?\\d{3}\\)?[- ]?\\d{3}-?\\d{4}");
Matcher matcher = pattern.matcher(text);

while (matcher.find()) {
    System.out.println("Phone: " + matcher.group());
}
/*
Output:
Phone: (123) 456-7890
Phone: 987-654-3210
*/
```

##### Common Regex Use Cases
###### 1. Username validation (alphanumeric, underscore, 3-16 chars):

```java
public boolean isValidUsername(String username) {
    return username != null && username.matches("^[a-zA-Z0-9_]{3,16}$");
}
```

###### 2. URL validation (simplified):

```java
public boolean isValidURL(String url) {
    String urlPattern = "^https?://[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}(/.*)?$";
    return url != null && url.matches(urlPattern);
}
```

###### 3. Date format validation (YYYY-MM-DD):

```java
public boolean isValidDate(String date) {
    String datePattern = "^\\d{4}-\\d{2}-\\d{2}$";
    return date != null && date.matches(datePattern);
}
```

###### 4. Extract numbers from text:

```java
public List<Integer> extractNumbers(String text) {
    List<Integer> numbers = new ArrayList<>();
    Pattern pattern = Pattern.compile("\\d+");
    Matcher matcher = pattern.matcher(text);
    
    while (matcher.find()) {
        numbers.add(Integer.parseInt(matcher.group()));
    }
    
    return numbers;
}

// Test:
List<Integer> nums = extractNumbers("I have 3 apples and 5 oranges");
System.out.println(nums);  // [3, 5]
```

##### Performance Tip
###### If you're using the same regex pattern multiple times, compile it once:

```java
// Inefficient - compiles pattern every time
for (String email : emails) {
    if (email.matches("^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}$")) {
        // process
    }
}

// Efficient - compile once
Pattern emailPattern = Pattern.compile("^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}$");
for (String email : emails) {
    if (emailPattern.matcher(email).matches()) {
        // process
    }
}
```

##### Important Notes
1. Escaping: In Java strings, backslash must be escaped. Use \\d not \d.
2. Greedy vs Lazy: By default, * and + are greedy (match as much as possible). Add ? to make them lazy:

```java
String html = "<div>Content</div>";
   html.replaceAll("<.*>", "");   // Removes entire string (greedy)
   html.replaceAll("<.*?>", "");  // Removes tags only (lazy) → "Content"
```
3. **Complex patterns**: For complex validation (like RFC-compliant email), use specialized libraries or pre-tested patterns.

4. **Testing**: Always test regex patterns thoroughly with edge cases.

##### When to Use Regex
**Use regex when**:
- Validating input formats (email, phone, URLs)
- Extracting data from unstructured text
- Replacing complex patterns
- Parsing simple structured data

**Avoid regex when**:
- Parsing HTML/XML (use proper parsers like JSoup)
- Simple string operations (use `contains()`, `startsWith()`, etc.)
- Performance is critical (regex has overhead)
- Pattern is extremely complex (hard to maintain)

---
---

### 5. String Concatenation (Performance Analysis)
#### 5.1 Using + Operator

```java
String s1 = "Hello";
String s2 = " World";
String s3 = s1 + s2;  // Creates new String object
```

##### What happens internally (before Java 9):
- The compiler converts this into StringBuilder operations
- Equivalent to: new StringBuilder().append(s1).append(s2).toString()

##### From Java 9 onwards:
- Uses invokedynamic and StringConcatFactory for optimization
- More efficient than manual StringBuilder for simple concatenations

#### 5.2 Concatenation in Loops (Performance Problem)
##### Bad practice:

```java
String result = "";
for (int i = 0; i < 10000; i++) {
    result += i;  // Creates 10,000 new String objects!
}
```

##### Why this is bad:
- Each += operation creates a new String object
- Old strings become garbage, causing memory pressure
- Time complexity: O(n²) due to repeated copying

##### Solution: Use StringBuilder:

```java
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 10000; i++) {
    sb.append(i);
}
String result = sb.toString();  // Only one String created
```

---
---

### 6. StringBuffer and StringBuilder
#### 6.1 Why Mutable String Classes Exist
Since String is immutable, every modification creates a new object. For scenarios involving frequent string modifications (concatenation in loops, building dynamic SQL queries, etc.), this is inefficient.

##### Java provides two mutable alternatives:
1. StringBuffer (Java 1.0) - Thread-safe, synchronized
2. StringBuilder (Java 5) - Not thread-safe, faster

#### 6.2 StringBuffer
Definition: A thread-safe, mutable sequence of characters.

##### Key characteristics:
- All methods are synchronized
- Thread-safe but slower than StringBuilder
- Suitable for multi-threaded environments

##### Common methods:

```java
StringBuffer sb = new StringBuffer("Hello");

sb.append(" World");  // "Hello World"
sb.insert(5, ",");    // "Hello, World"
sb.delete(5, 6);      // "Hello World"
sb.reverse();         // "dlroW olleH"
sb.replace(0, 5, "Hi");  // "Hi olleH"

String result = sb.toString();
```

##### Capacity management:
- Default capacity: 16 characters
- When capacity is exceeded, new capacity = (old capacity * 2) + 2
- You can specify initial capacity: new StringBuffer(100)

#### 6.3 StringBuilder
Definition: A mutable sequence of characters, not thread-safe.

##### Key characteristics:
- Methods are NOT synchronized
- Faster than StringBuffer (no synchronization overhead)
- Preferred in single-threaded scenarios (most common case)

##### Usage (same API as StringBuffer):

```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");
sb.insert(6, "Beautiful ");
System.out.println(sb.toString());  // "Hello Beautiful World"
```

#### 6.4 Difference Between String, StringBuffer, and StringBuilder

|**Feature**|**String**|**StringBuffer**|**StringBuilder**|
|-----------|----------|----------------|-----------------|
| Mutability | Immutable | Mutable | Mutable |
| Thread Safety | Thread-safe (immutable) | Thread-safe (synchronized) | Not thread-safe |
| Performance | Slow for modifications | Moderate (sync overhead) | Fast |
| Storage | String Pool + Heap | Heap only | Heap only |
| When to use | Static/fixed text | Multi-threaded modifications | Single-threaded modifications |
| Introduced | Java 1.0 | Java 1.0 | Java 1.5 |
| Memory | New object per modification | Expands dynamically | Expands dynamically |

Interview tip: In 99% of cases, use String for fixed text and StringBuilder for modifications. Use StringBuffer only when multiple threads modify the same string object (very rare).

---
---

### 7. String intern() Method (JVM Internals)
#### 7.1 What is intern()?
Definition: The intern() method is a native method that places a string into the String Pool if it doesn't exist, or returns a reference to the existing pooled string.

##### Method signature:

```java
public native String intern();
```

#### 7.2 How intern() Works
##### Case 1: String doesn't exist in pool

```java
String s1 = new String("Hello").intern();
```

1. new String("Hello") creates an object in heap
2. .intern() checks String Pool for "Hello"
3. If not found, places "Hello" in the pool
4. Returns reference to the pooled string
5. s1 points to the pooled object (heap object becomes eligible for GC)

##### Case 2: String already exists in pool

```java
String s2 = "Hello";  // Creates in pool
String s3 = new String("Hello").intern();
System.out.println(s2 == s3);  // true (both point to pool)
```

#### 7.3 JVM-Level Behavior of String Pool
##### Before Java 7:
- String Pool was in PermGen space (fixed size, rarely garbage collected)
- Excessive use of intern() could cause OutOfMemoryError: PermGen space

##### From Java 7 onwards:
- String Pool moved to heap memory
- Subject to garbage collection like other heap objects
- Safer to use intern() in production

#### 7.4 When to Use intern()
##### Use case 1: Memory optimization when dealing with many duplicate strings

```java
// Example: Reading 1 million user records where city names repeat
List<String> cities = new ArrayList<>();
for (User user : users) {
    cities.add(user.getCity().intern());  // Reuse pooled strings
}
```

##### Use case 2: Fast string comparison

```java
String s1 = getUserInput().intern();
String s2 = getConfigValue().intern();
if (s1 == s2) {  // Fast reference comparison
    // ...
}
```

##### When NOT to use intern():
- For unique or rarely repeated strings (wastes pool space)
- When dealing with very large strings (pools them unnecessarily)
- In memory-constrained environments

#### 7.5 Performance Implications
##### Pros:
- Reduces memory footprint for duplicate strings
- Enables fast == comparison
- Useful for string-heavy applications (parsers, data processing)

##### Cons:
- intern() is a relatively expensive operation (involves hash table lookup)
- Can increase String Pool size, impacting GC performance
- Overuse can lead to memory leaks (strings stay in pool longer than needed)

---
---

### 8. Memory and Performance Impact
#### 8.1 String Storage Areas
##### String Pool (Heap - special area):
- Stores string literals
- Shared across all references
- Garbage collected (from Java 7+)
- Optimized for memory reuse

##### Regular Heap:
- Stores strings created with new keyword
- Stores StringBuilder/StringBuffer objects
- Subject to normal GC cycles

##### Stack:
- Stores string reference variables (not the string content itself)
- Example: String s = "Hello"; → s is on stack, "Hello" is in String Pool

#### 8.2 Memory Overhead of String Operations
Scenario: Concatenating 1000 strings using + operator in a loop

```java
String result = "";
for (int i = 0; i < 1000; i++) {
    result += "item" + i;
}
```

##### Memory impact:
- Creates approximately 1000 intermediate String objects
- Each concatenation copies all previous content
- Memory usage: O(n²)
- Causes frequent GC cycles

##### Optimized version:

```java
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 1000; i++) {
    sb.append("item").append(i);
}
String result = sb.toString();
```

##### Memory impact:
- Only one StringBuilder object created
- Capacity expands dynamically (roughly doubles when full)
- Final toString() creates one String
- Memory usage: O(n)

#### 8.3 Garbage Collection Impact
##### String immutability and GC:
- Every string "modification" creates a new object
- Old strings become unreachable and eligible for GC
- Excessive string creation increases GC pressure
- In high-throughput applications, this can cause latency spikes

Best practice: Use StringBuilder for repeated modifications, especially in loops or recursive methods.

---
---

### 9. Real-World Use Cases
#### 9.1 Beginner Level
##### Use case 1: User input validation

```java
String username = scanner.nextLine().trim();
if (username.isEmpty()) {
    System.out.println("Username cannot be empty");
}
if (username.length() < 5) {
    System.out.println("Username must be at least 5 characters");
}
```

##### Use case 2: Simple string formatting

```java
String firstName = "John";
String lastName = "Doe";
String fullName = firstName + " " + lastName;
System.out.println("Welcome, " + fullName);
```

#### 9.2 Interview Level
##### Use case 1: Palindrome check

```java
public boolean isPalindrome(String s) {
    s = s.toLowerCase().replaceAll("[^a-z0-9]", "");
    int left = 0, right = s.length() - 1;
    while (left < right) {
        if (s.charAt(left) != s.charAt(right)) {
            return false;
        }
        left++;
        right--;
    }
    return true;
}
```

##### Use case 2: Anagram check

```java
public boolean areAnagrams(String s1, String s2) {
    if (s1.length() != s2.length()) return false;
    
    char[] chars1 = s1.toCharArray();
    char[] chars2 = s2.toCharArray();
    Arrays.sort(chars1);
    Arrays.sort(chars2);
    
    return Arrays.equals(chars1, chars2);
}
```

#### 9.3 Production Level (5+ Years)
##### Use case 1: Building dynamic SQL queries safely

```java
public String buildQuery(List<String> columns, String tableName, Map<String, String> filters) {
    StringBuilder query = new StringBuilder("SELECT ");
    query.append(String.join(", ", columns));
    query.append(" FROM ").append(tableName);
    
    if (!filters.isEmpty()) {
        query.append(" WHERE ");
        List<String> conditions = new ArrayList<>();
        for (Map.Entry<String, String> entry : filters.entrySet()) {
            conditions.add(entry.getKey() + " = ?");
        }
        query.append(String.join(" AND ", conditions));
    }
    
    return query.toString();
}
```

##### Use case 2: Log message formatting

```java
public String formatLogMessage(String level, String message, Object... args) {
    StringBuilder sb = new StringBuilder();
    sb.append("[").append(LocalDateTime.now()).append("] ");
    sb.append("[").append(level).append("] ");
    sb.append(String.format(message, args));
    return sb.toString();
}
```

##### Use case 3: CSV parsing

```java
public List<String[]> parseCSV(String csvContent) {
    List<String[]> records = new ArrayList<>();
    String[] lines = csvContent.split("\n");
    
    for (String line : lines) {
        String[] fields = line.split(",");
        for (int i = 0; i < fields.length; i++) {
            fields[i] = fields[i].trim();
        }
        records.add(fields);
    }
    
    return records;
}
```

---
---

### 10. Important Diagrams (Described in Words)
#### Diagram 1: String Pool vs Heap Memory
##### Scenario:

```java
String s1 = "Java";
String s2 = "Java";
String s3 = new String("Java");
```

##### Memory layout:

```java
STRING POOL (Special area in Heap)
┌─────────────────────────┐
│  "Java" object          │ ← s1 points here
│  (created once)         │ ← s2 points here
└─────────────────────────┘

REGULAR HEAP
┌─────────────────────────┐
│  String object          │ ← s3 points here
│  value: "Java"          │ (separate copy)
└─────────────────────────┘

STACK (Method Execution)
┌─────────────────────────┐
│  s1 → (reference to pool) │
│  s2 → (reference to pool) │
│  s3 → (reference to heap) │
└─────────────────────────┘
```

#### Diagram 2: String Immutability
##### Scenario:

```java
String s = "Hello";
s = s.concat(" World");
```

##### Memory changes:

```java
STEP 1: Initial creation
String Pool:
┌──────────────┐
│   "Hello"    │ ← s points here
└──────────────┘

STEP 2: After concat (before reassignment)
String Pool:
┌──────────────┐
│   "Hello"    │ ← s still points here
└──────────────┘

Heap (newly created):
┌──────────────────┐
│  "Hello World"   │ ← exists but not referenced yet
└──────────────────┘

STEP 3: After reassignment (s = s.concat(...))
String Pool:
┌──────────────┐
│   "Hello"    │ ← no reference (eligible for GC)
└──────────────┘

Heap:
┌──────────────────┐
│  "Hello World"   │ ← s now points here
└──────────────────┘

```


#### Diagram 3: StringBuilder Growth
##### Scenario: Appending to StringBuilder

```java
Initial capacity: 16 characters
┌────────────────────────────────┐
│ [empty 16 character buffer]    │
└────────────────────────────────┘

After append("Hello World!")  (12 chars)
┌────────────────────────────────┐
│ Hello World! [4 unused]        │
└────────────────────────────────┘

After append(" Java Programming")  (17 more chars needed)
Capacity exceeded! New capacity = (16 * 2) + 2 = 34
┌──────────────────────────────────────────────────────────┐
│ Hello World! Java Programming [5 unused]                 │
└──────────────────────────────────────────────────────────┘
```

---
---

### 11. Common Mistakes and Misconceptions
#### Mistake 1: Using == for String Comparison
**Wrong approach:**

```java
String s1 = "Java";
String s2 = getUserInput();  // returns "Java"
if (s1 == s2) {  // WRONG - compares references
    System.out.println("Equal");
}
```

Why it's wrong: == compares memory addresses, not content. s2 might be a different object with the same content.

**Correct approach:**

```java
if (s1.equals(s2)) {  // Compare content
    System.out.println("Equal");
}
```

#### Mistake 2: Assuming Strings Are Mutable
**Wrong approach:**

```java
String s = "Hello";
s.concat(" World");
System.out.println(s);  // Outputs: Hello (unchanged!)
```

Why it's wrong: String methods return new strings; they don't modify the original.

**Correct approach:**

```java
String s = "Hello";
s = s.concat(" World");  // Reassign to capture new string
System.out.println(s);  // Outputs: Hello World
```

#### Mistake 3: String Concatenation in Loops
**Wrong approach:**

```java
String result = "";
for (int i = 0; i < 10000; i++) {
    result += i;  // Creates 10,000 objects
```

**Why it's wrong**: Creates excessive objects, causing memory bloat and performance degradation.

**Correct approach**:

```java
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 10000; i++) {
    sb.append(i);
}
String result = sb.toString();
```

#### Mistake 4: NullPointerException Traps

**Wrong approach**:
```java
String s = null;
if (s.equals("Java")) {  // NullPointerException!
    // ...
}
```

**Correct approach (best practice)**:
```java
if ("Java".equals(s)) {  // Safe - literal first
    // ...
}
// Or use null check:
if (s != null && s.equals("Java")) {
    // ...
}
```

#### Mistake 5: Ignoring Case-Sensitivity

**Wrong approach**:
```java
String password = "Password123";
if (password.equals("password123")) {  // false - case mismatch
    System.out.println("Correct");
}
```

**Correct approach**:
```java
if (password.equalsIgnoreCase("password123")) {  // true
    System.out.println("Correct");
}
```

#### Misconception 1: "String Pool Only Stores Literals"
**Reality**: While literals automatically go to the pool, you can manually add strings using `intern()`.
```java
String s1 = new String("Hello").intern();  // Now in pool
String s2 = "Hello";
System.out.println(s1 == s2);  // true
```

#### Misconception 2: "StringBuilder is Always Faster"
**Reality**: For simple concatenations, modern JVM optimizations make `+` operator comparable to StringBuilder.
```java
// This is fine (compiler optimizes it):
String s = "Hello" + " " + "World";

// This needs StringBuilder (loop):
String result = "";
for (int i = 0; i < 1000; i++) {
    result += i;  // Bad
}
```

#### Misconception 3: "intern() Always Improves Performance"
**Reality**: `intern()` has overhead. Use only when dealing with many duplicate strings.

**Good use**:
```java
// Reading CSV with repeated city names
String city = record.getCity().intern();  // Reuse memory
```

**Bad use**:
```java
// Unique user IDs
String userId = UUID.randomUUID().toString().intern();  // Wastes pool space
```

---
---

### 11A Common String Programming Questions (With Solutions)
This section covers frequently asked string manipulation problems in interviews and exams. Each program includes multiple approaches with time and space complexity analysis.
Program 1: Reverse a String
Problem: Given a string, reverse it without using built-in reverse methods.
Approach 1: Using StringBuilder (Recommended)

```java
public class StringReversal {
    public static String reverseUsingStringBuilder(String str) {
        if (str == null || str.isEmpty()) {
            return str;
        }
        
        return new StringBuilder(str).reverse().toString();
    }
    
    public static void main(String[] args) {
        String original = "Hello World";
        String reversed = reverseUsingStringBuilder(original);
        System.out.println("Original: " + original);
        System.out.println("Reversed: " + reversed);
        // Output: dlroW olleH
    }
}
```

Time Complexity: O(n)
Space Complexity: O(n)
Best for: Production code - clean and efficient
Approach 2: Using Character Array (Manual)

```java
public static String reverseUsingCharArray(String str) {
    if (str == null || str.isEmpty()) {
        return str;
    }
    
    char[] chars = str.toCharArray();
    int left = 0;
    int right = chars.length - 1;
    
    while (left < right) {
        // Swap characters
        char temp = chars[left];
        chars[left] = chars[right];
        chars[right] = temp;
        
        left++;
        right--;
    }
    
    return new String(chars);
}
```

Time Complexity: O(n)
Space Complexity: O(n)
Best for: Interview discussions - shows algorithm understanding
Approach 3: Using Recursion

```java
public static String reverseUsingRecursion(String str) {
    if (str == null || str.isEmpty()) {
        return str;
    }
    
    // Base case: single character or empty
    if (str.length() == 1) {
        return str;
    }
    
    // Recursive case: last char + reverse of remaining
    return str.charAt(str.length() - 1) 
           + reverseUsingRecursion(str.substring(0, str.length() - 1));
}
```

Time Complexity: O(n²) - due to substring creation
Space Complexity: O(n) - recursion stack
Best for: Understanding recursion - not recommended for production
Approach 4: Using Stack (Data Structure Approach)

```java
import java.util.Stack;

public static String reverseUsingStack(String str) {
    if (str == null || str.isEmpty()) {
        return str;
    }
    
    Stack<Character> stack = new Stack<>();
    
    // Push all characters to stack
    for (char c : str.toCharArray()) {
        stack.push(c);
    }
    
    // Pop all characters (LIFO gives reversed order)
    StringBuilder reversed = new StringBuilder();
    while (!stack.isEmpty()) {
        reversed.append(stack.pop());
    }
    
    return reversed.toString();
}
```

Time Complexity: O(n)
Space Complexity: O(n)
Best for: Demonstrating stack usage - academic purposes

Program 2: Check if String is Palindrome
Problem: Determine if a string reads the same forwards and backwards (ignoring case and non-alphanumeric characters).
Approach 1: Two-Pointer Technique (Optimized)

```java
public class PalindromeChecker {
    public static boolean isPalindrome(String str) {
        if (str == null || str.isEmpty()) {
            return true;  // Empty string is palindrome
        }
        
        // Clean and normalize: remove non-alphanumeric, convert to lowercase
        str = str.replaceAll("[^a-zA-Z0-9]", "").toLowerCase();
        
        int left = 0;
        int right = str.length() - 1;
        
        while (left < right) {
            if (str.charAt(left) != str.charAt(right)) {
                return false;
            }
            left++;
            right--;
        }
        
        return true;
    }
    
    public static void main(String[] args) {
        System.out.println(isPalindrome("A man, a plan, a canal: Panama"));  // true
        System.out.println(isPalindrome("race a car"));  // false
        System.out.println(isPalindrome("Madam"));  // true
        System.out.println(isPalindrome("12321"));  // true
    }
}
```

Time Complexity: O(n)
Space Complexity: O(n) - due to replaceAll creating new string
Interview tip: This handles real-world cases with punctuation and spaces.
Approach 2: Without Extra Space (In-place Check)

```java
public static boolean isPalindromeOptimized(String str) {
    if (str == null || str.isEmpty()) {
        return true;
    }
    
    str = str.toLowerCase();
    int left = 0;
    int right = str.length() - 1;
    
    while (left < right) {
        // Skip non-alphanumeric from left
        while (left < right && !Character.isLetterOrDigit(str.charAt(left))) {
            left++;
        }
        
        // Skip non-alphanumeric from right
        while (left < right && !Character.isLetterOrDigit(str.charAt(right))) {
            right--;
        }
        
        // Compare
        if (str.charAt(left) != str.charAt(right)) {
            return false;
        }
        
        left++;
        right--;
    }
    
    return true;
}
```

Time Complexity: O(n)
Space Complexity: O(1) - if we ignore toLowerCase (or use charAt comparison)
Best for: Optimized interview solutions
Approach 3: Using StringBuilder Reverse

```java
public static boolean isPalindromeSimple(String str) {
    if (str == null) {
        return false;
    }
    
    String cleaned = str.replaceAll("[^a-zA-Z0-9]", "").toLowerCase();
    String reversed = new StringBuilder(cleaned).reverse().toString();
    
    return cleaned.equals(reversed);
}
```

Time Complexity: O(n)
Space Complexity: O(n)
Best for: Quick solution when space is not a constraint

Program 3: Check if Two Strings are Anagrams
Problem: Determine if two strings contain the same characters in different orders.
Approach 1: Using Sorting

```java
import java.util.Arrays;

public class AnagramChecker {
    public static boolean areAnagrams(String s1, String s2) {
        // Null or length check
        if (s1 == null || s2 == null) {
            return false;
        }
        
        if (s1.length() != s2.length()) {
            return false;
        }
        
        // Convert to lowercase and remove spaces
        s1 = s1.replaceAll("\\s", "").toLowerCase();
        s2 = s2.replaceAll("\\s", "").toLowerCase();
        
        // Sort characters and compare
        char[] chars1 = s1.toCharArray();
        char[] chars2 = s2.toCharArray();
        
        Arrays.sort(chars1);
        Arrays.sort(chars2);
        
        return Arrays.equals(chars1, chars2);
    }
    
    public static void main(String[] args) {
        System.out.println(areAnagrams("listen", "silent"));  // true
        System.out.println(areAnagrams("Triangle", "Integral"));  // true
        System.out.println(areAnagrams("hello", "world"));  // false
        System.out.println(areAnagrams("The Eyes", "They See"));  // true
    }
}
```

Time Complexity: O(n log n) - due to sorting
Space Complexity: O(n) - for character arrays
Best for: Simple, readable solution
Approach 2: Using HashMap (Character Frequency)

```java
import java.util.HashMap;
import java.util.Map;

public static boolean areAnagramsUsingMap(String s1, String s2) {
    if (s1 == null || s2 == null) {
        return false;
    }
    
    if (s1.length() != s2.length()) {
        return false;
    }
    
    // Remove spaces and convert to lowercase
    s1 = s1.replaceAll("\\s", "").toLowerCase();
    s2 = s2.replaceAll("\\s", "").toLowerCase();
    
    // Count character frequencies in first string
    Map<Character, Integer> charCount = new HashMap<>();
    for (char c : s1.toCharArray()) {
        charCount.put(c, charCount.getOrDefault(c, 0) + 1);
    }
    
    // Decrease count for second string
    for (char c : s2.toCharArray()) {
        if (!charCount.containsKey(c)) {
            return false;  // Character not in first string
        }
        
        charCount.put(c, charCount.get(c) - 1);
        
        if (charCount.get(c) < 0) {
            return false;  // More occurrences in s2
        }
    }
    
    // Check if all counts are zero
    for (int count : charCount.values()) {
        if (count != 0) {
            return false;
        }
    }
    
    return true;
}
```

Time Complexity: O(n)
Space Complexity: O(k) - where k is the number of unique characters
Best for: Optimized interview solutions, large strings
Approach 3: Using Character Array Count (For ASCII)

```java
public static boolean areAnagramsOptimized(String s1, String s2) {
    if (s1 == null || s2 == null || s1.length() != s2.length()) {
        return false;
    }
    
    s1 = s1.replaceAll("\\s", "").toLowerCase();
    s2 = s2.replaceAll("\\s", "").toLowerCase();
    
    // Frequency array for 26 lowercase letters
    int[] charCount = new int[26];
    
    for (int i = 0; i < s1.length(); i++) {
        charCount[s1.charAt(i) - 'a']++;
        charCount[s2.charAt(i) - 'a']--;
    }
    
    // Check if all counts are zero
    for (int count : charCount) {
        if (count != 0) {
            return false;
        }
    }
    
    return true;
}
```

Time Complexity: O(n)
Space Complexity: O(1) - fixed size array
Best for: When input is guaranteed to be lowercase English letters

Program 4: Count Vowels and Consonants
Problem: Count the number of vowels and consonants in a given string.

```java
public class VowelConsonantCounter {
    public static void countVowelsAndConsonants(String str) {
        if (str == null || str.isEmpty()) {
            System.out.println("Vowels: 0, Consonants: 0");
            return;
        }
        
        str = str.toLowerCase();
        int vowelCount = 0;
        int consonantCount = 0;
        
        for (int i = 0; i < str.length(); i++) {
            char c = str.charAt(i);
            
            // Check if character is a letter
            if (Character.isLetter(c)) {
                // Check if vowel
                if (c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u') {
                    vowelCount++;
                } else {
                    consonantCount++;
                }
            }
        }
        
        System.out.println("Vowels: " + vowelCount);
        System.out.println("Consonants: " + consonantCount);
    }
    
    // Alternative: Return as array [vowels, consonants]
    public static int[] countVowelsAndConsonantsArray(String str) {
        if (str == null) {
            return new int[]{0, 0};
        }
        
        str = str.toLowerCase();
        int vowels = 0;
        int consonants = 0;
        
        for (char c : str.toCharArray()) {
            if (Character.isLetter(c)) {
                if ("aeiou".indexOf(c) != -1) {
                    vowels++;
                } else {
                    consonants++;
                }
            }
        }
        
        return new int[]{vowels, consonants};
    }
    
    public static void main(String[] args) {
        String text = "Hello World! How are you?";
        countVowelsAndConsonants(text);
        // Output:
        // Vowels: 6
        // Consonants: 10
        
        int[] counts = countVowelsAndConsonantsArray("Java Programming");
        System.out.println("Vowels: " + counts[0] + ", Consonants: " + counts[1]);
        // Output: Vowels: 5, Consonants: 11
    }
}
```

Time Complexity: O(n)
Space Complexity: O(1)
Interview variations:

Count only vowels
Count each vowel separately
Count vowels, consonants, digits, and special characters


Program 5: Find First Non-Repeated Character
Problem: Find the first character in a string that doesn't repeat.
Approach 1: Using LinkedHashMap (Preserves Order)

```java
import java.util.LinkedHashMap;
import java.util.Map;

public class FirstNonRepeatedChar {
    public static Character findFirstNonRepeated(String str) {
        if (str == null || str.isEmpty()) {
            return null;
        }
        
        // LinkedHashMap preserves insertion order
        Map<Character, Integer> charCount = new LinkedHashMap<>();
        
        // Count occurrences
        for (char c : str.toCharArray()) {
            charCount.put(c, charCount.getOrDefault(c, 0) + 1);
        }
        
        // Find first character with count = 1
        for (Map.Entry<Character, Integer> entry : charCount.entrySet()) {
            if (entry.getValue() == 1) {
                return entry.getKey();
            }
        }
        
        return null;  // No non-repeated character found
    }
    
    public static void main(String[] args) {
        System.out.println(findFirstNonRepeated("stress"));  // t
        System.out.println(findFirstNonRepeated("aabbcc"));  // null
        System.out.println(findFirstNonRepeated("java"));    // j
        System.out.println(findFirstNonRepeated("swiss"));   // w
    }
}
```

Time Complexity: O(n)
Space Complexity: O(k) - where k is unique characters
Best for: Guaranteed correct order preservation
Approach 2: Two-Pass with Index Tracking

```java
public static Character findFirstNonRepeatedOptimized(String str) {
    if (str == null || str.isEmpty()) {
        return null;
    }
    
    // First pass: count frequencies
    int[] charCount = new int[256];  // ASCII characters
    for (char c : str.toCharArray()) {
        charCount[c]++;
    }
    
    // Second pass: find first with count = 1
    for (char c : str.toCharArray()) {
        if (charCount[c] == 1) {
            return c;
        }
    }
    
    return null;
}
```

Time Complexity: O(n)
Space Complexity: O(1) - fixed size array
Best for: Performance-critical scenarios
Approach 3: Return Index Instead of Character

```java
public static int findFirstNonRepeatedIndex(String str) {
    if (str == null || str.isEmpty()) {
        return -1;
    }
    
    for (int i = 0; i < str.length(); i++) {
        char c = str.charAt(i);
        
        // Check if character appears only once
        if (str.indexOf(c) == str.lastIndexOf(c)) {
            return i;
        }
    }
    
    return -1;  // Not found
}
```

Time Complexity: O(n²) - indexOf/lastIndexOf scan the string
Space Complexity: O(1)
Best for: When you need the index, not the character

Interview Tips for String Programs
1. Always handle edge cases:
  - Null strings
  - Empty strings
  - Single character strings
  - Strings with special characters

2. Ask clarifying questions:
  - Should comparison be case-sensitive?
  - Should spaces be ignored?
  - What about special characters?
  - What should be returned if no answer exists?

3. Discuss complexity:
  - Always mention time and space complexity
  - Explain trade-offs between approaches

4. Code quality matters:
  - Use meaningful variable names
  - Add comments for complex logic
  - Handle edge cases gracefully

5. Optimize when needed:
  - Start with brute force, then optimize
  - Explain why you chose a particular approach

---
---

### 12. Best Practices (5+ Years Expectation)
#### Practice 1: Choose the Right String Type

**Rule**:
- Use `String` for fixed or rarely modified text
- Use `StringBuilder` for frequent modifications in single-threaded code
- Use `StringBuffer` only in multi-threaded scenarios where multiple threads modify the same string

**Example**:
```java
// Reading config file - use String
String configValue = properties.getProperty("db.url");

// Building dynamic query - use StringBuilder
StringBuilder query = new StringBuilder();
query.append("SELECT * FROM users WHERE ");
// ... build conditions

// Thread-safe log buffer - use StringBuffer (rare)
StringBuffer threadSafeLog = new StringBuffer();
```

#### Practice 2: Always Use `.equals()` for Content Comparison

**Rule**: Never use `==` to compare string content in production code.

**Why**: `==` compares references, which can lead to subtle bugs.

**Exception**: Only use `==` after explicitly interning strings and when you understand the implications.

#### Practice 3: Avoid String Concatenation in Loops

**Rule**: Use `StringBuilder` when concatenating inside loops.

**Benchmark-driven rule**: For more than 5-10 concatenations, prefer `StringBuilder`.

#### Practice 4: Be Mindful of String Immutability

**Rule**: Remember that string methods return new strings.
```java
// Wrong - original string unchanged
String s = "  hello  ";
s.trim();

// Correct
s = s.trim();
```

#### Practice 5: Use String Pool Wisely

**Rule**: 
- Use string literals for common, reusable strings
- Avoid `new String()` unless you specifically need a separate heap object
- Use `intern()` judiciously for duplicate detection scenarios

#### Practice 6: Handle Null Safely

**Rule**: Always check for null before calling string methods, or use defensive coding.
```java
// Defensive pattern - literal first
if ("ADMIN".equals(userRole)) {
    // ...
}

// Null check pattern
if (userRole != null && userRole.equals("ADMIN")) {
    // ...
}

// Java 7+ - Objects utility
if (Objects.equals(userRole, "ADMIN")) {
    // ...
}
```

#### Practice 7: Prefer Built-in Methods Over Custom Logic

**Rule**: Use optimized String methods instead of writing custom character-by-character logic.

**Example**:
```java
// Less efficient - manual loop
boolean found = false;
for (int i = 0; i < s.length(); i++) {
    if (s.charAt(i) == 'x') {
        found = true;
        break;
    }
}

// Better - built-in method
boolean found = s.indexOf('x') != -1;
// Or even better:
boolean found = s.contains("x");
```

#### Practice 8: Be Aware of Character Encoding

**Rule**: When converting strings to bytes or reading from external sources, explicitly specify encoding.
```java
// Risky - uses platform default encoding
byte[] bytes = s.getBytes();

// Safe - explicit encoding
byte[] bytes = s.getBytes(StandardCharsets.UTF_8);
```

#### Practice 9: Validate and Sanitize User Input

**Rule**: Always validate and clean user-provided strings before processing.
```java
public boolean isValidUsername(String username) {
    if (username == null || username.trim().isEmpty()) {
        return false;
    }
    
    username = username.trim();
    
    // Length check
    if (username.length() < 3 || username.length() > 20) {
        return false;
    }
    
    // Pattern validation
    return username.matches("[a-zA-Z0-9_]+");
}
```

#### Practice 10: Optimize String Operations in Performance-Critical Code

**Rule**: Profile before optimizing, but be aware of common pitfalls.

**Hot path optimization**:
```java
// Instead of repeated substring operations:
String data = getLargeString();
for (int i = 0; i < 1000; i++) {
    process(data.substring(i * 10, (i + 1) * 10));  // Creates 1000 strings
}

// Better - use single substring or character-level processing:
for (int i = 0; i < 1000; i++) {
    int start = i * 10;
    int end = (i + 1) * 10;
    // Process characters directly from data without creating substrings
    for (int j = start; j < end; j++) {
        char c = data.charAt(j);
        // process char
    }
}
```

---
---

### 13. Interview-Oriented Key Points (Quick Revision)

1. **Strings are immutable** - once created, content cannot change.

2. **String Pool** - special heap area that stores string literals for memory optimization (moved from PermGen to heap in Java 7).

3. **String literal vs new keyword**:
   - Literal: `"Hello"` → goes to String Pool
   - `new String("Hello")` → creates object in heap (bypasses pool)

4. **Always use `.equals()` for comparison**, not `==` (which compares references).

5. **String concatenation in loops** - use `StringBuilder` to avoid creating excessive objects.

6. **StringBuilder vs StringBuffer**:
   - StringBuilder: faster, not thread-safe (prefer this)
   - StringBuffer: thread-safe, slower (use only in multi-threaded scenarios)

7. **`intern()` method** - adds string to pool or returns reference to existing pooled string.

8. **String methods return new strings** - original string remains unchanged (immutability).

9. **Common methods**: `length()`, `charAt()`, `substring()`, `equals()`, `compareTo()`, `contains()`, `replace()`, `split()`, `trim()`.

10. **String vs StringBuilder vs StringBuffer** - choose based on mutability needs and thread safety.

11. **Compiler optimization** - literals concatenated with `+` are optimized at compile time.

12. **Memory impact** - excessive string creation causes garbage collection pressure.

13. **Null safety** - always check for null or use defensive patterns like `"literal".equals(variable)`.

14. **From Java 9**: improved string concatenation using `invokedynamic`.

15. **From Java 11**: new methods like `isBlank()`, `lines()`, `strip()`, `repeat()`.

16. **Character encoding matters** - always specify charset when converting strings to bytes.

17. **String Pool is garbage collected** from Java 7+ (was not in earlier versions).

18. **Default StringBuilder capacity** is 16, grows by formula: `(old * 2) + 2`.

19. **String is a final class** - cannot be subclassed.

20. **All string handling rules remain unchanged till Java 25**.

---
---

### 14. One-Line Exam/Interview Answer

**Q: What is a String in Java?**

**A**: "A String is an immutable sequence of characters represented by the `java.lang.String` class, stored in the String Pool for memory optimization, and providing numerous methods for text manipulation."

**Alternative (more technical)**: "String is a final, immutable class in `java.lang` package that represents a sequence of characters, internally backed by a character array, stored in the String Pool to enable memory reuse and reference-based equality checks."

---
---

### Conclusion 
**Final thought**: Strings are deceptively simple on the surface but reveal layers of complexity when examined closely. This depth is what makes string-related questions a staple in technical interviews—they test not just syntax knowledge, but deep understanding of Java's memory model, performance optimization, and software engineering principles.

---
---