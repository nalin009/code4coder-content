## MODULE 8: Arrays

---

##### MCQ 1 (Beginner)
##### What is the correct way to declare an array in Java?
##### A) int arr[];  
##### B) int[] arr;  
##### C) array int arr;  
##### D) Both A and B
###### Answer: D) Both A and B
###### Explanation: Both `int arr[]` and `int[] arr` are syntactically correct in Java. However, `int[] arr` is the preferred convention as it clearly indicates "array of integers." Option C is invalid syntax—Java does not have an `array` keyword for declaration.

---

##### MCQ 2 (Beginner)
##### What is the default value for elements in an `int[]` array?
##### A) null  
##### B) 0  
##### C) -1  
##### D) undefined
###### Answer: B) 0 
###### Explanation: When an integer array is created using `new int[size]`, all elements are automatically initialized to 0 (the default value for int). For object arrays, the default is null; for boolean arrays, it's false; for char arrays, it's '\u0000'.

---

##### MCQ 3 (Beginner)
##### What will be the output of the following code?

```java
int[] arr = {10, 20, 30, 40, 50};
System.out.println(arr.length);
```

##### A) 4  
##### B) 5  
##### C) Compile error  
##### D) Runtime error
###### Answer: B) 5 
###### Explanation: The array contains 5 elements, so `arr.length` returns 5. Note that `length` is a field (not a method), so no parentheses are needed. Using `arr.length()` would cause a compile error.

---

##### MCQ 4 (Beginner)
##### Which exception is thrown when accessing an invalid array index?
##### A) NullPointerException  
##### B) ArrayIndexOutOfBoundsException  
##### C) IndexOutOfBoundsException  
##### D) IllegalArgumentException
###### Answer: B) ArrayIndexOutOfBoundsException
###### Explanation: `ArrayIndexOutOfBoundsException` is thrown when you try to access an array with an invalid index (negative or >= array length). This is a runtime exception that extends `IndexOutOfBoundsException`.

---

##### MCQ 5 (Intermediate)
##### What is the output of this code?

```java
int[][] matrix = new int[3][4];
System.out.println(matrix.length);
System.out.println(matrix[0].length);
```

##### A) 3, 4  
##### B) 4, 3  
##### C) 12, 12  
##### D) Compile error
###### Answer: A) 3, 4  
###### Explanation: `matrix.length` returns the number of rows (3), and `matrix[0].length` returns the number of columns in the first row (4). In 2D arrays, the outer array represents rows, and each inner array represents columns.

---

##### MCQ 6 (Intermediate)
##### Which statement is TRUE about arrays in Java?
##### A) Arrays can grow in size after creation  
##### B) Arrays are stored in stack memory  
##### C) Arrays are objects stored in heap memory  
##### D) Array length can be modified
###### Answer: C) Arrays are objects stored in heap memory  
###### Explanation: Arrays are objects in Java, always stored in heap memory (the reference variable is on the stack). Array size is fixed at creation and cannot be changed. To resize, you must create a new array and copy elements.

---

##### MCQ 7 (Intermediate)
##### What happens when you execute this code?

```java
String[] names = new String[3];
System.out.println(names[0]);
```

##### A) Prints empty string  
##### B) Prints null  
##### C) Throws NullPointerException  
##### D) Compile error
###### Answer: B) Prints null 
###### Explanation: Object arrays are initialized with null as the default value for each element. The code prints "null" (the string representation of null). A NullPointerException would occur only if you try to call a method on `names[0]`, like `names[0].length()`.

---

##### MCQ 8 (Intermediate)
##### Which of the following correctly creates a jagged array?
##### A) int[][] jagged = new int[3][4];  
##### B) int[][] jagged = {{1,2}, {3,4,5}, {6}};  
##### C) int[][] jagged = new int[][3];  
##### D) int[][] jagged = {3, 4, 2};
###### Answer: B) int[][] jagged = {{1,2}, {3,4,5}, {6}};  
###### Explanation: A jagged array has rows of different lengths. Option B shows proper syntax with nested array literals of varying sizes. Option A creates a rectangular array (all rows same length). Options C and D are syntactically incorrect.

---

##### MCQ 9 (Intermediate)
##### What is the result of comparing two arrays like this?

```java
int[] arr1 = {1, 2, 3};
int[] arr2 = {1, 2, 3};
System.out.println(arr1 == arr2);
```

##### A) true  
##### B) false  
##### C) Compile error  
##### D) Runtime error
###### Answer: B) false 
###### Explanation: The `==` operator compares references (memory addresses), not array content. Since `arr1` and `arr2` are different objects in heap memory, the comparison returns false. Use `Arrays.equals(arr1, arr2)` to compare content, which would return true.

---

##### MCQ 10 (Intermediate)
##### Which is the fastest way to copy an array?
##### A) Manual loop with assignment  
##### B) Arrays.copyOf()  
##### C) clone() method  
##### D) B and C are equally fast
###### Answer: D) B and C are equally fast
###### Explanation: Both `Arrays.copyOf()` and `clone()` internally use `System.arraycopy()`, which is a native method optimized at the JVM level. This is significantly faster than manual loops. `System.arraycopy()` directly is the fastest, but `Arrays.copyOf()` and `clone()` provide convenient wrappers with similar performance.

---

##### MCQ 11 (Advanced)
##### What is the time complexity of accessing an element in an array by index?
##### A) O(1)  
##### B) O(n)  
##### C) O(log n)  
##### D) O(n²)
###### Answer: A) O(1)
###### Explanation: Array access is O(1) constant time because the JVM calculates the memory address directly using the formula: `base_address + (index × element_size)`. No iteration or searching is required, making arrays extremely efficient for random access.

---

##### MCQ 12 (Advanced)
##### Which method from Arrays class requires the array to be sorted?
##### A) Arrays.fill()  
##### B) Arrays.sort()  
##### C) Arrays.binarySearch()  
##### D) Arrays.toString()
###### Answer: C) Arrays.binarySearch()  
###### Explanation: `Arrays.binarySearch()` uses binary search algorithm which only works correctly on sorted arrays. If the array is not sorted, the result is undefined (may return incorrect index or negative value). All other methods work on unsorted arrays.

---

##### MCQ 13 (Advanced)
##### What is the memory overhead for a 2D array compared to a 1D array with the same total elements?
##### A) Same memory usage  
##### B) Higher due to multiple object headers  
##### C) Lower due to optimization  
##### D) JVM-dependent only
###### Answer: B) Higher due to multiple object headers  
###### Explanation: A 2D array in Java is an array of arrays, meaning it creates multiple array objects (one main array plus one for each row). Each array object has its own header (~16 bytes), resulting in significant overhead compared to a single 1D array storing the same total elements.

---

##### MCQ 14 (Advanced)
##### What happens in this code?

```java
Object[] objects = new String[5];
objects[0] = 10;
```

##### A) Compiles and runs successfully  
##### B) Compile error  
##### C) ArrayStoreException at runtime  
##### D) ClassCastException at runtime
###### Answer: C) ArrayStoreException at runtime
###### Explanation: This demonstrates array covariance. The code compiles because `String[]` is a subtype of `Object[]`. However, at runtime, the JVM knows the array was created as `String[]` and throws `ArrayStoreException` when attempting to store an Integer (autoboxed from 10) into a String array.

---

##### MCQ 15 (Advanced)
##### What is true about the enhanced for loop with arrays?
##### A) Provides access to array index  
##### B) Can modify array elements  
##### C) Faster than traditional for loop  
##### D) Creates a copy of each element
###### Answer: D) Creates a copy of each element
###### Explanation: The enhanced for loop (`for (int num : array)`) creates a copy of each element value. For primitives, modifying the loop variable doesn't affect the array. For objects, you can modify object properties but cannot change which object the array element references. The enhanced for loop is syntactic sugar converted to a traditional for loop by the compiler, so performance is equivalent.

---