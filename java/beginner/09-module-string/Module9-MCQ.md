## MODULE 9: Strings

---

##### MCQ 1 (Beginner)
##### Which of the following creates a string in the String Pool?
##### A) String s = new String("Java");  
##### B) String s = "Java";  
##### C) String s = new String("Java").intern();  
##### D) Both B and C
###### Answer: D) Both B and C
###### Explanation: Option B directly creates a string literal in the String Pool. Option C uses `new String()` which creates an object in the heap, but calling `.intern()` adds it to the pool or returns the existing pooled string. Option A creates a heap object without interning it. Both B and C result in a pooled string reference.

---

##### MCQ 2 (Beginner)
##### What will be the output of the following code?

```java
String s = "Hello";
s.concat(" World");
System.out.println(s);
```

##### A) Hello World  
##### B) Hello  
##### C) Compilation error  
##### D) NullPointerException
###### Answer: B) Hello 
###### Explanation: Since strings are immutable, `concat()` creates a new string but doesn't modify the original. The returned new string is not assigned to any variable, so `s` still references "Hello". To see "Hello World", you would need: `s = s.concat(" World");`

---

##### MCQ 3 (Beginner)
##### Which method is used to compare the content of two strings?
##### A) ==  
##### B) compareTo()  
##### C) equals()  
##### D) compare()
###### Answer: C) equals()  
###### Explanation: The `.equals()` method compares the actual character sequence of two strings. The `==` operator compares references (memory addresses). `compareTo()` returns an integer for lexicographic comparison. There is no `compare()` method in the String class.

---

##### MCQ 4 (Beginner)
##### What is the default capacity of a StringBuilder?
##### A) 0  
##### B) 8  
##### C) 16  
##### D) 32
###### Answer: C) 16 
###### Explanation: When you create a StringBuilder using `new StringBuilder()`, it initializes with a default capacity of 16 characters. This capacity automatically expands when needed using the formula: (old capacity * 2) + 2.

---

##### MCQ 5 (Intermediate)
##### What will be the output?

```java
String s1 = "Java";
String s2 = "Java";
String s3 = new String("Java");
System.out.println(s1 == s2);
System.out.println(s1 == s3);
```

##### A) true true  
##### B) true false  
##### C) false true  
##### D) false false
###### Answer: B) true false  
###### Explanation: `s1` and `s2` both reference the same string literal in the String Pool, so `s1 == s2` is true. However, `s3` is explicitly created in the heap using `new`, so it's a different object despite having the same content, making `s1 == s3` false.

---

##### MCQ 6 (Intermediate)
##### Which class should be used for string concatenation in a loop for best performance?
##### A) String  
##### B) StringBuffer  
##### C) StringBuilder  
##### D) Both B and C
###### Answer: C) StringBuilder 
###### Explanation: StringBuilder is the best choice for single-threaded string concatenation in loops because it's mutable and not synchronized, making it faster than StringBuffer. String concatenation in loops creates multiple objects, causing performance degradation. StringBuffer has synchronization overhead, making it slower than StringBuilder when thread safety isn't needed.

---

##### MCQ 7 (Intermediate)
##### Where is the String Pool located from Java 7 onwards?
##### A) Stack memory  
##### B) Heap memory  
##### C) PermGen space  
##### D) Metaspace
###### Answer: B) Heap memory  
###### Explanation: Before Java 7, the String Pool was in PermGen space. From Java 7 onwards, it was moved to the heap memory. This change made the pool eligible for garbage collection and reduced OutOfMemoryError issues. This remains unchanged till Java 25.

---

##### MCQ 8 (Intermediate)
##### What does the `intern()` method do?
##### A) Creates a new string in the heap  
##### B) Converts a string to uppercase  
##### C) Places a string in the String Pool or returns the pooled reference  
##### D) Deletes a string from memory
###### Answer: C) Places a string in the String Pool or returns the pooled reference 
###### Explanation: The `intern()` method checks if the string exists in the String Pool. If it exists, it returns a reference to the pooled string. If not, it adds the string to the pool and returns the reference. This enables memory optimization and fast reference-based comparison.

---

##### MCQ 9 (Intermediate)
##### What is the output?

```java
String s1 = "Hello" + "World";
String s2 = "HelloWorld";
System.out.println(s1 == s2);
```

##### A) true  
##### B) false  
##### C) Compilation error  
##### D) Runtime exception
###### Answer: A) true 
###### Explanation: The Java compiler optimizes string literal concatenation at compile time. `"Hello" + "World"` is converted to `"HelloWorld"` during compilation. Both `s1` and `s2` reference the same pooled string, so `s1 == s2` returns true.

---

##### MCQ 10 (Advanced)
##### Which statement is TRUE about String, StringBuilder, and StringBuffer?
##### A) String is mutable, StringBuilder and StringBuffer are immutable  
##### B) StringBuilder is thread-safe, StringBuffer is not  
##### C) String and StringBuffer are thread-safe, StringBuilder is not  
##### D) All three are mutable and thread-safe
###### Answer: C) String and StringBuffer are thread-safe, StringBuilder is not  
###### Explanation: String is immutable (inherently thread-safe because its state can't change). StringBuffer is thread-safe due to synchronized methods. StringBuilder is not thread-safe but offers better performance in single-threaded scenarios. This distinction is crucial for production code decisions.

---

##### MCQ 11 (Advanced)
##### What is the time complexity of string concatenation using the `+` operator in a loop with n iterations?
##### A) O(n)  
##### B) O(n log n)  
##### C) O(n²)  
##### D) O(1)
###### Answer: C) O(n²) 
###### Explanation: Each concatenation creates a new string and copies all previous content. In iteration 1, it copies 1 character; in iteration 2, it copies 2 characters, and so on. Total operations: 1 + 2 + 3 + ... + n = n(n+1)/2, which is O(n²). Using StringBuilder reduces this to O(n).

---

##### MCQ 12 (Advanced)
##### What happens when StringBuilder's capacity is exceeded?
##### A) It throws an OutOfMemoryError  
##### B) It creates a new array with capacity: (old capacity * 2) + 2  
##### C) It creates a new array with capacity: old capacity + 1  
##### D) It stops accepting new characters
###### Answer: B) It creates a new array with capacity: (old capacity * 2) + 2  
###### Explanation: When the current capacity is exceeded, StringBuilder creates a new character array with capacity calculated as: (oldCapacity * 2) + 2. It then copies the existing content to the new array. This expansion strategy balances memory usage and the number of resizing operations.

---

##### MCQ 13 (Advanced)
##### Which scenario is BEST suited for using `intern()`?
##### A) Storing unique user IDs  
##### B) Processing a CSV file with many repeated city names  
##### C) Generating random strings  
##### D) Building dynamic SQL queries
###### Answer: B) Processing a CSV file with many repeated city names 
###### Explanation: `intern()` is most beneficial when dealing with many duplicate strings, as it reuses memory by pooling identical strings. In a CSV with repeated city names, interning those names saves significant memory. Using it for unique values (A, C) wastes pool space, and for dynamic queries (D), StringBuilder is more appropriate.

---

##### MCQ 14 (Advanced)
##### What is the JVM-level reason for String immutability?
##### A) To enable String Pool optimization and thread safety  
##### B) To reduce memory usage  
##### C) To make strings faster than primitives  
##### D) To prevent compiler errors
###### Answer: A) To enable String Pool optimization and thread safety  
###### Explanation: Immutability enables the String Pool to safely share string objects across multiple references without risk of one reference modifying the content for others. It also makes strings inherently thread-safe without synchronization. These JVM-level optimizations significantly improve both memory efficiency and concurrent programming safety.


---

##### MCQ 15 (Advanced - Java Version Specific)
##### From which Java version onwards did the JVM optimize string concatenation using `invokedynamic`?
##### A) Java 7  
##### B) Java 8  
##### C) Java 9  
##### D) Java 11
###### Answer: C) Java 9  
###### Explanation: Java 9 introduced optimized string concatenation using `invokedynamic` bytecode instruction and the `StringConcatFactory` class. This replaces the earlier approach of converting `+` operations into explicit `StringBuilder` calls, providing more flexibility for JVM optimizations. This optimization remains in effect through Java 25.

---