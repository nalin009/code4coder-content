## Module 6: DECISION-MAKING STATEMENTS 

---

##### MCQ 1 (Beginner)
##### What will be the output of the following code?

```java
int x = 15;
if (x > 10) {
    System.out.println("Greater");
} else {
    System.out.println("Smaller");
}
```

##### A) Greater
##### B) Smaller
##### C) Greater Smaller
##### D) Compilation error
###### Answer: A) Greater
###### Explanation: Since x > 10 evaluates to true (15 > 10), the if block executes and prints "Greater". The else block is skipped.  

---

##### MCQ 2 (Beginner)
##### Which of the following data types is NOT supported by the switch statement?
##### A) int
##### B) String
##### C) double
##### D) enum
###### Answer: C) double
###### Explanation: Switch does not support long, float, double, or boolean types. It supports byte, short, int, char, String (Java 7+), and enum (Java 5+). Floating-point types are excluded due to precision issues.

---

##### MCQ 3 (Beginner)
##### What will be the result of the following ternary operation?

```java
int a = 10, b = 20;
int max = (a > b) ? a : b;
System.out.println(max);
```

##### A) 10
##### B) 20
##### C) 30
##### D) Compilation error
###### Answer: B) 20
###### Explanation: The ternary operator evaluates a > b (false), so it returns b, which is 20.

---

##### MCQ 4 (Beginner)
##### What is the purpose of the default case in a switch statement?
##### A) It is mandatory in every switch statement
##### B) It handles values not matched by any case
##### C) It must be placed at the beginning of the switch
##### D) It prevents compilation errors
###### Answer: B) It handles values not matched by any case
###### Explanation: The default case acts as a catch-all for values that don't match any explicit case. It is optional but recommended for defensive programming.

---

##### MCQ 5 (Beginner)
##### Which statement is correct about comparing strings in Java?
##### A) Use == to compare string content
##### B) Use equals() to compare string content
##### C) Both == and equals() are identical
##### D) Strings cannot be compared in if statements
###### Answer: B) Use equals() to compare string content
###### Explanation: == compares object references (memory addresses), while equals() compares actual string content. Always use equals() for string comparison.

---

##### MCQ 6 (Beginner)
##### What happens if both operands of && are method calls that have side effects?
##### A) Both methods always execute
##### B) Second method executes only if first returns true
##### C) Second method executes only if first returns false
##### D) Compilation error
###### Answer: B) Second method executes only if first returns true
###### Explanation: && uses short-circuit evaluation. If the first operand is false, the second operand (including any side effects) is not evaluated.

---


##### MCQ 7 (Intermediate)
##### What will be the output?

```java
int num = 5;
String result = switch (num) {
    case 1, 2, 3 -> "Low";
    case 4, 5, 6 -> "Medium";
    default -> "High";
};
System.out.println(result);
```

##### A) Low
##### B) Medium
##### C) High
##### D) Compilation error (Java 13 or earlier)
###### Answer: B) Medium (D) if Java 13 or earlier
###### Explanation: This is a switch expression (Java 14+). Since num is 5, it matches the second case and returns "Medium". On Java 13 or earlier, this syntax causes a compilation error.

---

##### MCQ 8 (Intermediate)
##### What is the output of the following code?

```java
int day = 2;
switch (day) {
    case 1:
        System.out.print("Mon ");
    case 2:
        System.out.print("Tue ");
    case 3:
        System.out.print("Wed ");
    default:
        System.out.print("Other");
}
```

##### A) Tue
##### B) Tue Wed Other
##### C) Mon Tue Wed Other
##### D) Other
###### Answer: B) Tue Wed Other
###### Explanation: Missing break statements cause fallthrough. Execution starts at case 2 and continues through case 3 and default, printing all three.

---

##### MCQ 9 (Intermediate)
##### Which operator is used for short-circuit AND evaluation in Java?
##### A) &
##### B) &&
##### C) |
##### D) ||
###### Answer: B) &&
###### Explanation: && is the short-circuit AND operator. If the first operand is false, the second operand is not evaluated. & is a bitwise AND operator that always evaluates both operands.

---

##### MCQ 10 (Intermediate)
##### What will be the output?

```java
String result = (5 > 3) ? "Yes" : "No";
System.out.println(result);
```

##### A) Yes
##### B) No
##### C) YesNo
##### D) Compilation error
###### Answer: A) Yes
###### Explanation:  The condition 5 > 3 is true, so the ternary operator returns "Yes".

---

##### MCQ 11 (Intermediate)
##### What will be the output of the following code?

```java
int x = 10;
if (x > 5 && x < 15) {
    System.out.println("In range");
}
```

##### A) In range
##### B) No output
##### C) Compilation error
##### D) Runtime error
###### Answer: A) In range
###### Explanation: Both conditions x > 5 and x < 15 are true, so the if block executes and prints "In range".

---


##### MCQ 12 (Advanced)
##### What is the time complexity of a switch statement with 100 cases when using tableswitch optimization?
##### A) O(1)
##### B) O(log n)
##### C) O(n)
##### D) O(n²)
###### Answer: A) O(1)
###### Explanation: When cases are densely packed, the compiler uses tableswitch bytecode, which creates an array-based lookup table enabling constant-time O(1) jumps to the matching case.

---

##### MCQ 13 (Advanced)
##### Which Java version introduced switch expressions with arrow syntax?
##### A) Java 8
##### B) Java 11
##### C) Java 14
##### D) Java 17
###### Answer: C) Java 14
###### Explanation: Switch expressions with arrow syntax (->) were introduced as a standard feature in Java 14, eliminating the need for break statements and allowing switches to return values.

---

##### MCQ 14 (Advanced)
##### What is the time complexity of a switch statement with 100 cases when using tableswitch optimization?
##### A) O(1)
##### B) O(log n)
##### C) O(n)
##### D) O(n²)
###### Answer: A) O(1)
###### Explanation: When cases are densely packed, the compiler uses tableswitch bytecode, which creates an array-based lookup table enabling constant-time O(1) jumps to the matching case.

---

##### MCQ 15 (Advanced)
##### In Java 21+ pattern matching for switch, which of the following is valid?
##### A) case String s -> s.length();
##### B) case int i -> i * 2;
##### C) case 1, 2, 3 -> "Low";
##### D) All of the above
###### Answer: A) case String s -> s.length();
###### Explanation: Java 21+ supports pattern matching in switch, allowing type patterns like String s. Options B uses primitive type (not a pattern), and option C is regular switch expression syntax, not pattern matching.

---