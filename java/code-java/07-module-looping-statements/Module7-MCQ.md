## Module 7: LOOPING STATEMENTS 

---

##### MCQ 1 (Beginner)
##### How many times will the following loop execute?

```java
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}
```

##### A) 4
##### B) 5
##### C) 6
##### D) Infinite
###### Answer: B) 5
###### Explanation: The loop starts at i = 0 and runs while i < 5, executing for i = 0, 1, 2, 3, 4 (5 iterations total).

---

##### MCQ 2 (Beginner)
##### Which loop guarantees at least one execution of the loop body?
##### A) for loop
##### B) while loop
##### C) do-while loop
##### D) enhanced for loop
###### Answer: C) do-while loop
###### Explanation: The do-while loop checks its condition after executing the loop body, ensuring the body runs at least once even if the condition is initially false.

---

##### MCQ 3 (Beginner)
##### What is the correct syntax for an enhanced for loop?
##### A) for (int i : array)
##### B) for (int i in array)
##### C) for (int i of array)
##### D) foreach (int i : array)
###### Answer: A) for (int i : array)
###### Explanation: The enhanced for loop uses the colon (:) syntax: for (Type variable : collection).

---

##### MCQ 4 (Beginner)
##### Which statement immediately exits the loop?
##### A) continue
##### B) break
##### C) return
##### D) Both B and C
###### Answer: D) Both B and C
###### Explanation: break exits the loop immediately, while return exits the entire method (including the loop).

---

##### MCQ 5  (Beginner)
##### Which loop should you use when the number of iterations is unknown?
##### A) for loop
##### B) while loop
##### C) do-while loop
##### D) Both B and C
###### Answer: D) Both B and C
###### Explanation: Both while and do-while loops are suitable for unknown iterations, with the choice depending on whether at least one execution is required.

---

##### MCQ 6 (Intermediate)
##### What is the output of the following code?

```java
int i = 0;
do {
    System.out.print(i + " ");
    i++;
} while (i < 0);
```

##### A) No output
##### B) 0
##### C) 0 -1 -2 ...
##### D) Compilation error
###### Answer: B) 0
###### Explanation: The do-while loop executes the body once before checking the condition. It prints 0, then checks i < 0 (false) and exits.

---

##### MCQ 7 (Intermediate)
##### What will be the output of the following code?

```java
for (int i = 0; i < 5; i++) {
    if (i == 3) {
        continue;
    }
    System.out.print(i + " ");
}
```

##### A) 0 1 2 3 4
##### B) 0 1 2 4
##### C) 0 1 2
##### D) 3
###### Answer: B) 0 1 2 4
###### Explanation: When i == 3, the continue statement skips the print statement for that iteration, so 3 is not printed.

---

##### MCQ 8 (Intermediate)
##### What happens when you try to modify a collection using an enhanced for loop?
##### A) The collection is modified successfully
##### B) ConcurrentModificationException is thrown
##### C) Compilation error
##### D) Nothing happens, changes are ignored
###### Answer: B) ConcurrentModificationException is thrown
###### Explanation: Modifying a collection (adding/removing elements) during iteration with an enhanced for loop triggers the fail-fast mechanism, throwing ConcurrentModificationException.

---

##### MCQ 9 (Intermediate)
##### What will be the output?

```java
for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= 2; j++) {
        if (i == 2 && j == 1) {
            break;
        }
        System.out.print(i + "" + j + " ");
    }
}
```

##### A) 11 12 21 31 32
##### B) 11 12 21 22 31 32
##### C) 11 12 22 31 32
##### D) 11 12 31 32
###### Answer: D) 11 12 31 32
###### Explanation: When i == 2 and j == 1, break exits the inner loop. The loop then continues with i == 3.

---

##### MCQ 10 (Intermediate)
##### What is the output of the following code?

```java
int[] arr = {1, 2, 3};
for (int num : arr) {
    num = num * 2;
}
System.out.println(arr[0]);
```

##### A) 1
##### B) 2
##### C) 3
##### D) Compilation error
###### Answer: A) 1
###### Explanation: The enhanced for loop creates a copy of each element. Modifying num does not affect the original array.

---

##### MCQ 11 (Intermediate)
##### What will happen if the update statement is missing in a for loop?

```java
for (int i = 0; i < 10;) {
    System.out.println(i);
}
```

##### A) Compilation error
##### B) Infinite loop
##### C) Executes once
##### D) No output
###### Answer: B) Infinite loop
###### Explanation: Without the update statement (i++), i never changes, and the condition i < 10 remains true indefinitely.

---

##### MCQ 12 (Advanced)
##### What is the time complexity of the following nested loop?

```java
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        System.out.println(i + ", " + j);
    }
}
```

##### A) O(n)
##### B) O(n log n)
##### C) O(n²)
##### D) O(2n)
###### Answer: C) O(n²)
###### Explanation: The outer loop runs n times, and for each iteration, the inner loop runs n times, resulting in n × n = n² total iterations.

---

##### MCQ 13 (Advanced)
##### Which JVM optimization technique involves executing multiple loop iterations in a single pass?
##### A) Loop hoisting
##### B) Loop unrolling
##### C) Loop fusion
##### D) Dead code elimination
###### Answer: B) Loop unrolling
###### Explanation: Loop unrolling is an optimization where the JIT compiler expands the loop body to execute multiple iterations per cycle, reducing branching overhead.

---

##### MCQ 14 (Advanced)
##### What is the purpose of labeled break in nested loops?
##### A) To break out of the innermost loop only
##### B) To break out of a specific labeled loop
##### C) To continue the outer loop
##### D) To skip the current iteration
###### Answer: B) To break out of a specific labeled loop
###### Explanation: Labeled break allows you to exit a specific outer loop by name, not just the innermost loop.

---

##### MCQ 15 (Advanced)
##### Which of the following is an optimization technique where invariant code is moved outside the loop?
##### A) Loop unrolling
##### B) Loop hoisting
##### C) Loop fusion
##### D) Constant folding
###### Answer: B) Loop hoisting
###### Explanation: Loop hoisting moves calculations that produce the same result in every iteration outside the loop to improve performance.

---