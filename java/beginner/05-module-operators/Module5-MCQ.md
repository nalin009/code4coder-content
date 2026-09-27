## MODULE 5: OPERATORS

---

##### MCQ 1 (Beginner)
##### What is the result of the following expression: 5 + 3 * 2?
##### A) 16
##### B) 11
##### C) 13
##### D) 10
###### Answer: B) 11
###### Explanation: Multiplication (*) has higher precedence than addition (+), so the expression evaluates as 5 + (3 * 2) = 5 + 6 = 11. To get 16, you would need parentheses: (5 + 3) * 2.

---

##### MCQ 2 (Beginner)
##### Which operator is used to compare two primitive values for equality in Java?
##### A) =
##### B) ==
##### C) .equals()
##### D) ===
###### Answer: B) ==
###### Explanation: The == operator compares the values of two primitive types. The = operator is for assignment. The .equals() method is used to compare object content, not primitives. Java does not have a === operator (unlike JavaScript).

---

##### MCQ 3 (Beginner)
##### What will be the output of the following code?

```java
int x = 10;
int y = x++;
System.out.println(y);
```

##### A) 10
##### B) 11
##### C) 9
##### D) Compilation error
###### Answer: A) 10
###### Explanation: x++ is the post-increment operator. It first assigns the current value of x (which is 10) to y, and then increments x to 11. Therefore, y is 10.

---

##### MCQ 4 (Beginner)
##### Which operator is used to check if an object is an instance of a specific class?
##### A) typeof
##### B) instanceof
##### C) is
##### D) classof
###### Answer: B) instanceof
###### Explanation: The instanceof operator checks if an object is an instance of a specific class or interface. Java does not have typeof, is, or classof operators (unlike some other languages).

---

##### MCQ 5 (Beginner)
##### What is the result of 10 % 3 in Java?
##### A) 3
##### B) 1
##### C) 0
##### D) 3.33
###### Answer: B) 1
###### Explanation: The modulus operator (%) returns the remainder of the division. 10 / 3 = 3 with a remainder of 1, so 10 % 3 = 1.

---

##### MCQ 6 (Intermediate)
##### What is the result of 7 / 2 in Java?
##### A) 3.5
##### B) 3
##### C) 4
##### D) 3.0
###### Answer: B) 3
###### Explanation: Since both operands are integers, Java performs integer division, which truncates the decimal part. The result is 3, not 3.5. To get 3.5, at least one operand must be a floating-point type: 7.0 / 2 or (double) 7 / 2.

---

##### MCQ 7 (Intermediate)
##### Which of the following operators uses short-circuit evaluation?
##### A) &
##### B) |
##### C) &&
##### D) ^
###### Answer: C) &&
###### Explanation: The && (logical AND) operator uses short-circuit evaluation, meaning if the first operand is false, the second operand is not evaluated. The & operator (bitwise AND) always evaluates both operands. | is bitwise OR, and ^ is bitwise XOR, neither of which short-circuits.

---

##### MCQ 8 (Intermediate)
##### What will be the output of the following code?

```java
String s1 = new String("Hello");
String s2 = new String("Hello");
System.out.println(s1 == s2);
```

##### A) true
##### B) false
##### C) Compilation error
##### D) Runtime error
###### Answer: B) false
###### Explanation: The == operator compares references (memory addresses) for objects, not their content. s1 and s2 are two different objects in memory, so s1 == s2 returns false. To compare content, use s1.equals(s2), which would return true.

---

##### MCQ 9 (Intermediate)
##### What is the result of the expression ~5 in Java?
##### A) 5
##### B) -5
##### C) -6
##### D) 6
###### Answer: C) -6
###### Explanation: The bitwise complement operator (~) inverts all bits. 5 in binary is 00000000 00000000 00000000 00000101. After inverting, it becomes 11111111 11111111 11111111 11111010, which represents -6 in two's complement representation.

---

##### MCQ 10 (Intermediate)
##### Which statement about the ternary operator is true?
##### A) It can have four operands.
##### B) It is the only ternary operator in Java.
##### C) It always requires parentheses.
##### D) It cannot be nested.
###### Answer: B) It is the only ternary operator in Java.
###### Explanation: The conditional operator (? :) is Java's only ternary operator (operates on three operands). It does not require parentheses (though they improve readability), and it can be nested: (a > b) ? "A" : (b > c) ? "B" : "C".

---

##### MCQ 11 (Intermediate)
##### What will be the result of 5 & 3 in Java?
##### A) 1
##### B) 3
##### C) 5
##### D) 7
###### Answer: A) 1
###### Explanation: The & operator performs a bitwise AND operation. 5 in binary is 0101, and 3 is 0011. Performing AND: 0101 & 0011 = 0001, which is 1 in decimal.

---

##### MCQ 12 (Advanced)
##### What will be the output of the following code?

```java
byte b = 100;
b = b + 1;
System.out.println(b);
```

##### A) 101
##### B) Compilation error
##### C) 100
##### D) Runtime error
###### Answer: B) Compilation error
###### Explanation: The expression b + 1 promotes b to int (binary numeric promotion), and the result is an int. Assigning an int to a byte without explicit casting causes a compilation error: "incompatible types: possible lossy conversion from int to byte." Using b += 1 would work because compound operators include an implicit cast.

---

##### MCQ 13 (Advanced)
##### What is the result of -5 >> 1 in Java?
##### A) -2
##### B) -3
##### C) 2147483645
##### D) -1
###### Answer: B) -3
###### Explanation: The >> operator performs a signed (arithmetic) right shift, preserving the sign bit. -5 in binary (two's complement) is 11111111 11111111 11111111 11111011. Shifting right by 1 and filling with the sign bit (1) gives 11111111 11111111 11111111 11111101, which is -3. If unsigned shift (>>>) were used, the result would be a large positive number.

---

##### MCQ 14 (Advanced)
##### What is the behavior of the following code?

```java
int x = Integer.MAX_VALUE;
int y = x + 1;
System.out.println(y);
```

##### A) Prints 2147483648
##### B) Prints -2147483648
##### C) Throws ArithmeticException
##### D) Compilation error
###### Answer: B) Prints -2147483648
###### Explanation: Integer overflow in Java wraps around silently without throwing an exception. Integer.MAX_VALUE is 2147483647. Adding 1 causes overflow, wrapping to Integer.MIN_VALUE, which is -2147483648. This behavior is unchanged till Java 25.

---

##### MCQ 15 (Advanced)
##### Which of the following correctly explains why x += 1 compiles but x = x + 1 does not for byte x?
##### A) += is faster than +.
##### B) += includes an implicit cast to the target type.
##### C) + promotes to long, but += does not.
##### D) It is a JVM-level optimization.
###### Answer: B) += includes an implicit cast to the target type.
###### Explanation: The expression x + 1 promotes x (a byte) to int, and the result is int. Assigning an int to a byte requires an explicit cast. However, the compound assignment operator += implicitly casts the result back to the target type: x += 1 is equivalent to x = (byte)(x + 1), which compiles successfully.

---