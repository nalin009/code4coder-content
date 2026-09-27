## 13. Java Coding Rules & Conventions

---

#### 13.1 File Naming Rules
##### Rule 1: File Name Must Match Public Class Name
- If a class is declared `public`, the filename must match exactly (case-sensitive).

**Example:**
```java
// File: HelloWorld.java
public class HelloWorld {
    // ...
}
```

- **Valid:** `HelloWorld.java`
- **Invalid:** `helloworld.java`, `HelloWorld.txt`, `Hello.java`

##### Rule 2: One Public Class Per File
- A Java source file can contain at most `ONE` public class.
- Can contain `multiple` non-public classes.

**Example:**
```java
// File: Main.java
public class Main {
    // ...
}

class Helper {
    // ...
}

class Utility {
    // ...
}
```

- Main.java can contain Main (public), Helper, and Utility (non-public).
- **Compiler generates:** `Main.class`, `Helper.class`, `Utility.class`

---

#### 13.2 Package Declarations
##### Rule 1: If present, package statement MUST be the first statement in the file (before imports and class declarations).
**Example:**

```java
package com.example.project;

import java.util.Scanner;

public class MyClass {
    // ...
}
```

**Invalid**

```java
import java.util.Scanner;
package com.example.project; // ERROR: package must come first
```

---

#### 13.3 Import Statements
##### Rule 1: import statements come after package and before class declarations.
**Example:**

```java
package com.example;

import java.util.ArrayList;
import java.util.List;

public class Demo {
    // ...
}
```

###### Wildcard Imports:
- import java.util.*; imports all classes from java.util.
- Does NOT import sub-packages (e.g., java.util.concurrent.* is separate).

**Best Practice:** Use explicit imports (`import java.util.ArrayList;`) instead of wildcards for clarity.

---

#### 13.4 Class Structure Conventions
##### Recommended Order (Industry Standard):
**1.** Class-level comments/JavaDoc
**2.** package statement
**3.** import statements
**4.** Class declaration
**5.** Static variables (public → protected → private)
**6.** Instance variables (public → protected → private)
**7.** Constructors
**8.** Methods (public → protected → private)
**9.** Inner classes

**Example:**

```java
package com.example;

import java.util.List;

/**
 * This class represents a Student.
 */
public class Student {
    // Static variables
    public static final String SCHOOL_NAME = "ABC School";
    private static int studentCount = 0;

    // Instance variables
    private String name;
    private int age;

    // Constructor
    public Student(String name, int age) {
        this.name = name;
        this.age = age;
        studentCount++;
    }

    // Methods
    public String getName() {
        return name;
    }

    public static int getStudentCount() {
        return studentCount;
    }
}
```

---

#### 13.5 Code Formatting Conventions
##### Indentation:
- Use 4 spaces (or 1 tab) per indentation level.

##### Braces:
- Opening brace { on the same line (Java convention).

**Example:**

```java
if (condition) {
    // code
}
```

**Not:**

```java
if (condition)
{
    // code
}
```

##### Line Length:
- Limit lines to 80-120 characters for readability.

##### Comments:
- Use // for single-line comments.
- Use /* ... */ for multi-line comments.
- Use /** ... */ for JavaDoc comments (documentation).

**Example:**

```java
// This is a single-line comment

/*
 * This is a multi-line comment
 * explaining complex logic
 */

/**
 * This is a JavaDoc comment
 * @param name the name of the student
 * @return the student's ID
 */
public int getStudentId(String name) {
    // ...
}
```

---

#### 13.6 Blank Lines
##### Use blank lines to separate:
- Between methods.
- Between logical sections within a method.
- After class declaration before first member.

**Example:**

```java
public class Demo {

    private int value;

    public Demo(int value) {
        this.value = value;
    }

    public void display() {
        System.out.println(value);
    }

}
```

---

#### 13.7 Additional Best Practices
##### a. Avoid Magic Numbers:
- **Instead of:** `if (status == 1)`
- **Use:** `final int ACTIVE = 1; if (status == ACTIVE)`

##### b. Meaningful Names:
- Avoid single-letter variables except for loop counters (i, j, k).
- **Use descriptive names:** `employeeSalary` instead of es.

##### c. DRY Principle (Don't Repeat Yourself):
- Avoid code duplication. Extract repeated logic into methods.

##### d. SOLID Principles (5+ Years Experience):
- Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, Dependency Inversion.

##### e. Code Reviews:
- Always format code before committing.
- Use tools like Checkstyle, PMD, SonarQube for code quality checks.