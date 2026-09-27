## MODULE 3:  Basic Java Syntax

---

##### MCQ 1  (Beginner)
##### What is the correct entry point method signature in Java?
##### A) public void main(String[] args)
##### B) public static void main(String[] args)
##### C) static void main(String args)
##### D) public static int main(String[] args)
###### Answer: B) public static void main(String[] args)
###### Explanation: The JVM requires the main method to be public (accessible from anywhere), static (callable without creating an object), void (no return value), and named main with a String[] parameter. This signature has been unchanged since Java 1.0.

---

##### MCQ 2 (Beginner)
##### Which of the following is a valid single-line comment in Java?
##### A) /* This is a comment */
##### B) // This is a comment
##### C) <!-- This is a comment -->
##### D) # This is a comment
###### Answer: B) // This is a comment
###### Explanation: ava uses // for single-line comments. /* */ is for multi-line comments. <!-- --> is HTML syntax. # is used in Python and shell scripts, not Java.

---

##### MCQ 3 (Beginner)
##### What will be the output of the following code?

```java
System.out.print("Hello");
System.out.print(" World");
```
##### A) Hello World (on two lines)
##### B) HelloWorld (no space, same line)
##### C) Hello World (with space, same line)
##### D) Compilation error
###### Answer: C) Hello World (with space, same line)
###### Explanation: System.out.print does not add a newline, so both strings are printed on the same line. Since there's a space before "World" in the second print statement, the output is Hello World on the same line.

---

##### MCQ 4 (Beginner)
##### Which escape sequence represents a newline in Java?
##### A) \r
##### B) \n
##### C) \t
##### D) \\
###### Answer: B) \n
###### Explanation: \n represents a newline (line break). \r is carriage return, \t is tab, and \\ is a literal backslash.

---

##### MCQ 5 (Beginner)
##### What is a block in Java?
##### A) A single statement ending with a semicolon
##### B) A group of statements enclosed in curly braces {}
##### C) A method declaration
##### D) A class definition
###### Answer: B) A group of statements enclosed in curly braces {}
###### Explanation: A block is zero or more statements grouped together within curly braces {}. Blocks define scope boundaries and allow multiple statements to be treated as a single unit.

---

##### MCQ 6 (Intermediate)
##### What happens to comments during Java compilation?
##### A) Comments are included in the bytecode for documentation
##### B) Comments are converted to metadata in the .class file
##### C) Comments are completely stripped out and ignored
##### D) Comments are executed as no-op instructions
###### Answer: C) Comments are completely stripped out and ignored
###### Explanation: The compiler completely removes comments during tokenization. They have no representation in bytecode and no runtime impact whatsoever.

---

##### MCQ 7 (Intermediate)
##### What will be the output of the following code?

```java
public class Test {
    public static void main(String[] args) {
        int x = 10;
        {
            int y = 20;
            System.out.println(x + y);
        }
        System.out.println(x);
    }
}
```

##### A) 30 followed by 10
##### B) 30 followed by compilation error
##### C) Compilation error
##### D) 30 followed by runtime error
###### Answer: A) 30 followed by 10
###### Explanation: Variable x is in method scope and accessible in nested blocks. Variable y is in block scope and accessible within that block. After the block ends, y is destroyed, but x remains. Output: 30 (newline) 10.

---

##### MCQ 8 (Intermediate)
##### Which of the following will cause a compilation error?

```java
if (true) {
    int x = 5;
}
System.out.println(x);
```
##### A) No error
##### B) Runtime error
##### C) Compilation error: variable x cannot be resolved
##### D) Compilation error: missing semicolon
###### Answer: C) Compilation error: variable x cannot be resolved
###### Explanation: Variable x is declared inside the if block and goes out of scope when the block ends. Attempting to access it outside the block causes a compilation error.

---

##### MCQ 9 (Intermediate)
##### What is the purpose of Javadoc comments?
##### A) To improve code execution speed
##### B) To temporarily disable code during debugging
##### C) To generate HTML documentation for APIs
##### D) To explain internal implementation details
###### Answer: C) To generate HTML documentation for APIs
###### Explanation: Javadoc comments (/** */) are processed by the javadoc tool to generate HTML documentation for public APIs, methods, and classes. They are the standard for documenting Java libraries.

---

##### MCQ 10 (Intermediate)
##### Where are local variables stored in memory?
##### A) Heap
##### B) Stack
##### C) Metaspace
##### D) String Pool
###### Answer: B) Stack
###### Explanation: Local variables (declared in methods or blocks) are stored on the stack. They are automatically destroyed when the method or block exits, without requiring garbage collection.

---

##### MCQ 11 (Intermediate)
##### What is the difference between System.out.print and System.out.println?
##### A) print is faster than println
##### B) println adds a newline after printing, print does not
##### C) print is for integers, println is for strings
##### D) There is no difference
###### Answer: B) println adds a newline after printing, print does not
###### Explanation: println prints the text and adds a platform-specific newline character at the end. print outputs text without adding a newline, allowing subsequent output to appear on the same line.

---

##### MCQ 12 (Advanced)
##### What will be printed by the following code?

```java
System.out.println("Path: C:\\Users\\file.txt");
```

##### A) Path: C:\Users\file.txt
##### B) Path: C:\\Users\\file.txt
##### C) Compilation error
##### D) Path: C:/Users/file.txt
###### Answer: A) Path: C:\Users\file.txt
###### Explanation: The escape sequence \\ is converted to a single backslash \ during compilation. The output will display literal backslashes: C:\Users\file.txt.

---

##### MCQ 13 (Advanced)
##### Which statement is TRUE about Java's case sensitivity?
##### A) Class names are case-insensitive, but variable names are case-sensitive
##### B) Java is case-sensitive for all identifiers (classes, methods, variables)
##### C) Keywords are case-insensitive, but user-defined names are case-sensitive
##### D) Java is case-insensitive like SQL
###### Answer: B) Java is case-sensitive for all identifiers (classes, methods, variables)
###### Explanation: Java is strictly case-sensitive for all identifiers. System and system are completely different. Even keywords must be lowercase (e.g., public, not Public).

---

##### MCQ 14 (Advanced)
##### Which of the following practices is considered BEST for production Java code?
##### A) Using System.out.println for logging application events
##### B) Using a logging framework like SLF4J for logging
##### C) Removing all comments to reduce file size
##### D) Declaring all variables at the beginning of a method
###### Answer: B) Using a logging framework like SLF4J for logging
###### Explanation: Production code should use logging frameworks (SLF4J, Log4j) instead of System.out.println. Frameworks provide log levels, formatting, file output, and performance optimizations.

---

##### MCQ 15 (Advanced)
##### What is the scope of a variable declared in a for loop header?

```java
for (int i = 0; i < 10; i++) {
    // Code here
}
System.out.println(i); // What happens here?
```

##### A) i is accessible and prints the last value
##### B) i is out of scope, causing a compilation error
##### C) i is accessible but uninitialized
##### D) Runtime error occurs
###### Answer: B) i is out of scope, causing a compilation error
###### Explanation: Variables declared in a for loop header (e.g., int i = 0) have loop scope and are destroyed when the loop exits. Attempting to access i outside the loop causes a compilation error.

---