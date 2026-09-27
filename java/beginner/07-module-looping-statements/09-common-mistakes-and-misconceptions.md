### 8. Common Mistakes & Misconceptions
#### 1. Off-by-One Error

```java
// Wrong: Runs 11 times (i = 0 to 10)
for (int i = 0; i <= 10; i++) { }

// Correct: Runs 10 times (i = 0 to 9)
for (int i = 0; i < 10; i++) { }
```

#### 2. Modifying Collection During Enhanced For Loop

```java
List<Integer> list = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5));
for (int num : list) {
    if (num % 2 == 0) {
        list.remove(Integer.valueOf(num));  // ConcurrentModificationException
    }
}
```

#### 3. Infinite Loop Due to Floating-Point

```java
// May never terminate due to precision
for (double d = 0.0; d != 1.0; d += 0.1) {
    System.out.println(d);
}
```

#### 4. Forgetting Break in Switch Inside Loop

```java
for (int i = 0; i < 5; i++) {
    switch (i) {
        case 1:
            System.out.println("One");
            // Missing break - falls through
        case 2:
            System.out.println("Two");
            break;
    }
}
```

#### 5. Scope Confusion

```java
for (int i = 0; i < 10; i++) {
    // i is accessible here
}
// i is NOT accessible here - compilation error
System.out.println(i);
```

#### 6. Using Wrong Loop Type

```java
// BAD: Unknown iterations, but using for loop
for (int i = 0; ; i++) {
    String line = reader.readLine();
    if (line == null) break;
    process(line);
}

// BETTER: Use while for unknown iterations
String line;
while ((line = reader.readLine()) != null) {
    process(line);
}
```

#### 7. Not Checking Empty Collection

```java
int[] arr = {};
int max = arr[0];  // ArrayIndexOutOfBoundsException
for (int i = 1; i < arr.length; i++) {
    if (arr[i] > max) max = arr[i];
}
```

#### 8. Incrementing Wrong Variable in Nested Loop

```java
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        System.out.println(i + ", " + j);
        i++;  // BUG: Incrementing outer loop variable
    }
}
```

---
---