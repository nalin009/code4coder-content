## 6 switch Statement

---

#### 6.1 Syntax:

```java
switch (expression) {
    case value1:
        // code
        break;
    case value2:
        // code
        break;
    default:
        // default code
}
```

##### How It Works:
1. `Expression` is evaluated once
2. `Result` is compared against each case value
3. When a match is `found`, execution starts from that case
4. Execution continues until `break`, return, or end of switch
5. If no case matches, the `default` block executes (if present)

**Example:**

```java
int day = 3;
switch (day) {
    switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    case 3:
        System.out.println("Wednesday");
        break;
    case 4:
        System.out.println("Thursday");
        break;
    case 5:
        System.out.println("Friday");
        break;
    case 6:
        System.out.println("Saturday");
        break;
    case 7:
        System.out.println("Sunday");
        break;
    default:
        System.out.println("Invalid day");
}
```

**Output:**
```java
Wednesday
```

##### How switch Works Internally (Bytecode Level):
1. **Compiler Role:** The compiler analyzes the case values and chooses an optimization strategy:
  a) **tableswitch (Dense Cases):**
    - Used when case values are closely packed (few gaps)
    - Creates an `array-based` lookup table
    - Direct O(1) jump to the matching case
    - **Example:** cases 1, 2, 3, 4, 5

  b) **lookupswitch (Sparse Cases):**
    - Used when case values are scattered (many gaps)
    - Performs binary search on sorted case values
    - O(log n) lookup time
    - **Example:** cases 1, 100, 1000, 10000

2. **JVM Role:**
  - Evaluates the expression once and stores the `result`
  - Uses the `bytecode` instruction (tableswitch/lookupswitch) to jump directly
  - Much faster than multiple if-else comparisons for 5+ cases

##### Performance Comparison:

|**Number of Cases**|**if-else Time Complexity**|**switch Time Complexity**|
|-------------------|---------------------------|--------------------------|
| **1-3 cases** | O(n) - similar performance | O(1) or O(log n) - similar |
| **5+ cases** | O(n) - slower | O(1) or O(log n) - faster |
| **10+ cases** | O(n) - significantly slower | O(1) or O(log n) - significantly faster |

##### Supported Types in Switch
- **Primitive Types:** `byte`, `short`, `int`, `char`
- **Wrapper Classes:** `Byte`, `Short`, `Integer`, `Character`
- **Reference Types:**
  - `String` (Java 7+)
  - `enum` (Java 5+)
- **NOT Supported:** `long`, `float`, `double`, `boolean`

##### Why These Limitations?
1. **long not supported:** Historical design decision from C/C++, kept for consistency
2. **float/double not supported:** Floating-point comparisons are imprecise due to rounding errors
3. **boolean not supported:** Only two values (true/false) make if-else more natural and readable

**Example of Floating-Point Precision Issue:**

```java
double x = 0.1 + 0.2;  // Result: 0.30000000000000004
// Cannot reliably use in switch due to precision
```

---

#### 6.2 Fallthrough Behavior in Switch:
##### What is Fallthrough?
When a case block `doesn't end` with break, execution "`falls through`" to the next case without checking its condition.

**Example Without Break:**

```java
int x = 2;
switch (x) {
    case 1:
        System.out.println("One");
    case 2:
        System.out.println("Two");  // Executes
    case 3:
        System.out.println("Three");  // Also executes (fallthrough)
    default:
        System.out.println("Default");  // Also executes (fallthrough)
}
```

**Output:**
```java
Two
Three
Default
```

**Intentional Fallthrough (Multiple Cases, Same Logic):**

```java
int month = 2;
switch (month) {
    case 12:
    case 1:
    case 2:
        System.out.println("Winter");
        break;
    case 3:
    case 4:
    case 5:
        System.out.println("Spring");
        break;
    case 6:
    case 7:
    case 8:
        System.out.println("Summer");
        break;
    case 9:
    case 10:
    case 11:
        System.out.println("Fall");
        break;
    default:
        System.out.println("Invalid month");
}
```

##### Best Practice:
- Always use `break` unless fallthrough is intentional
- Document intentional `fallthrough` with a comment

```java
case 1:
    // Fallthrough intentional - shared logic for cases 1 and 2
case 2:
    System.out.println("Case 1 or 2");
    break;
```

---

#### 6.3 break Statement in switch
**Purpose:** Exits the switch block `immediately` and `transfers` control to the next statement after the switch.

##### Syntax:

```java
break;
```

**Example:**

```java
int option = 2;
switch (option) {
    case 1:
        System.out.println("Option 1");
        break;  // Exits switch
    case 2:
        System.out.println("Option 2");
        break;  // Exits switch
    case 3:
        System.out.println("Option 3");
        break;  // Exits switch
    default:
        System.out.println("Invalid option");
}
System.out.println("After switch");
```

**Output:**
Option 2
After switch

**What Happens Without Break:**

```java
int option = 2;
switch (option) {
    case 1:
        System.out.println("Option 1");
    case 2:
        System.out.println("Option 2");
    case 3:
        System.out.println("Option 3");
    default:
        System.out.println("Invalid option");
}
}
```

**Output:**

```java
Option 2
Option 3
Invalid option
```

**Best Practice:** Always use `break` unless `intentional` fallthrough is needed.

---

#### 6.4 default Case in switch
**Purpose:** Handles values `not explicitly` covered by any case; acts as a catch-all.

##### Syntax:

```java
default:
    // code for unmatched values
```

**Example:**

```java
int option = 10;
switch (option) {
    case 1:
        System.out.println("Option 1");
        break;
    case 2:
        System.out.println("Option 2");
        break;
    default:
        System.out.println("Invalid option");
}
```

**Output:**
```java
Invalid choice: 10
```

##### Important Points:
- default is `optional` but strongly `recommended`
- Can be placed `anywhere` in the switch (conventionally at the end)
- `Executes` if no case matches
- Should include `break` if not at the end (to prevent fallthrough)

**Default Not at the End:**

```java
switch (x) {
    case 1:
        System.out.println("One");
        break;
    default:
        System.out.println("Default");
        break;  // Important: prevents fallthrough to case 2
    case 2:
        System.out.println("Two");
        break;
}
```

##### Best Practice:  
- Always include a `default` case for defensive programming
- Use it to handle unexpected values or log errors
- Even if you think all values are covered, requirements change

---

#### 6.5 Switch Expressions (Java 14+) [MODERN JAVA]
##### What Are Switch Expressions?
Switch expressions are an `enhanced version` of the traditional switch statement introduced in Java 14. They can return values directly and use arrow syntax (->) to eliminate the need for break statements.

##### Key Differences from Traditional Switch:
- Returns a `value` (can be assigned to a variable)
- Arrow syntax (->) `prevents` fallthrough
- No need for `break` statements
- Must be exhaustive (all possible values must be handled)
- `Cleaner`, more concise syntax

##### Traditional Switch vs Switch Expression
###### Traditional Switch:

```java
int day = 2;
String dayType;
switch (day) {
    case 1:
    case 2:
    case 3:
    case 4:
    case 5:
        dayType = "Weekday";
        break;
    case 6:
    case 7:
        dayType = "Weekend";
        break;
    default:
        dayType = "Invalid";
}
System.out.println(dayType);
```

###### Modern Switch Expression:

```java
int day = 2;
String dayType = switch (day) {
    case 1, 2, 3, 4, 5 -> "Weekday";
    case 6, 7 -> "Weekend";
    default -> "Invalid";
};
System.out.println(dayType);
```

##### Benefits:
- 8 lines `reduced` to 5 lines
- `No break` needed
- Cannot forget `break` (no fallthrough bugs)
- `Value` is returned directly
- More `functional` programming style

---

#### 6.6 Syntax Variants of Switch Expressions
##### 1. Single Expression (Arrow Syntax):

```java
int month = 3;
String season = switch (month) {
    case 12, 1, 2 -> "Winter";
    case 3, 4, 5 -> "Spring";
    case 6, 7, 8 -> "Summer";
    case 9, 10, 11 -> "Fall";
    default -> "Invalid month";
};
```

##### 2. Block with yield Keyword: Use yield when you need multiple statements in a case block.

```java
int score = 85;
String grade = switch (score / 10) {
    case 10, 9 -> "A";
    case 8 -> "B";
    case 7 -> "C";
    case 6 -> "D";
    default -> {
        System.out.println("Score is below 60");
        yield "F";  // yield returns the value
    }
};
System.out.println("Grade: " + grade);
```

**Output:**

```java
Grade: B
```

##### 3. Using yield for Complex Logic:

```java
int number = 15;
String result = switch (number) {
    case 1, 2, 3 -> "Small";
    case 4, 5, 6 -> "Medium";
    default -> {
        if (number < 0) {
            yield "Negative";
        } else if (number > 100) {
            yield "Very Large";
        } else {
            yield "Large";
        }
    }
};
System.out.println(result);
```

**Output:**

```java
Large
```

---

#### 6.7 Exhaustiveness in Switch Expressions
##### What Does Exhaustive Mean?
A switch expression must handle `all possible` values of the expression type. If any value is not covered, the code won't compile.

**Example with Enum (Exhaustive Check):**

```java
enum Day { MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY }

Day day = Day.MONDAY;

// This will NOT compile without default or all cases covered
String dayType = switch (day) {
    case MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY -> "Weekday";
    case SATURDAY, SUNDAY -> "Weekend";
    // No default needed - all enum values covered
};
```

##### If You Miss a Case:

```java
// Compilation error: the switch expression does not cover all possible input values
String dayType = switch (day) {
    case MONDAY -> "Weekday";
    // Error: TUESDAY, WEDNESDAY, etc. not covered
};
```

##### For int, String, etc., default is Required:

```java
int x = 5;
String result = switch (x) {
    case 1 -> "One";
    case 2 -> "Two";
    // Must have default for exhaustiveness
    default -> "Other";
};
```

---

#### 6.8 Real-World Example: HTTP Status Code Handling
##### Traditional Switch:

```java
int statusCode = 404;
String message;
switch (statusCode) {
    case 200:
        message = "OK";
        break;
    case 201:
        message = "Created";
        break;
    case 400:
        message = "Bad Request";
        break;
    case 401:
        message = "Unauthorized";
        break;
    case 404:
        message = "Not Found";
        break;
    case 500:
        message = "Internal Server Error";
        break;
    default:
        message = "Unknown Status";
}
System.out.println(message);
```

##### Modern Switch Expression:

```java
int statusCode = 404;
String message = switch (statusCode) {
    case 200 -> "OK";
    case 201 -> "Created";
    case 400 -> "Bad Request";
    case 401 -> "Unauthorized";
    case 404 -> "Not Found";
    case 500 -> "Internal Server Error";
    default -> "Unknown Status";
};
System.out.println(message);
```

---

#### 6.9 When to Use Switch Expressions
##### Use Switch Expressions When:
- You need to assign a `value` based on multiple cases
- You want `cleaner`, more functional code
- You're using Java 14+
- You want to avoid `fallthrough` bugs
- `Exhaustiveness` checking adds safety (enums)

##### Use Traditional Switch When:
- You're on Java 13 or earlier
- You don't need to return a `value`
- You need intentional `fallthrough` behavior
- You have complex side effects in each case

##### Pattern Matching for Switch (Java 21+) [PREVIEW/FUTURE]
Java 21 introduced `pattern matching` in switch expressions, allowing type checking and casting in one step.

**Example:**

```java
Object obj = "Hello";

String result = switch (obj) {
    case String s -> "String of length " + s.length();
    case Integer i -> "Integer: " + i;
    case Long l -> "Long: " + l;
    case null -> "Null value";
    default -> "Unknown type";
};

System.out.println(result);
```

```java
String of length 5
```

###### Benefits:
- No need for `instanceof` checks and casting
- More `readable` and `concise`
- `Type-safe` at compile time

This feature is in preview/finalized in Java 21+ and represents the future direction of Java.