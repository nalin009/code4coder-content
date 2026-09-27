## MODULE 16: Packages

---

##### MCQ 1 (Beginner)
##### Which package is automatically imported in every Java program?
##### A) java.util
##### B) java.io
##### C) java.lang
##### D) java.net
###### Answer: C) java.lang
###### Explanation: java.lang is implicitly imported in every Java source file. It contains fundamental classes like Object, String, System, and Math. All other packages require explicit import statements.

---

##### MCQ 2 (Beginner)
##### What is the correct package declaration for a class file located at src/com/library/model/Book.java?
##### A) package com.library.model.Book;
##### B) package Book;
##### C) package com.library.model;
##### D) package src.com.library.model;
###### Answer: C) package com.library.model;
###### Explanation: The package declaration must match the directory path relative to the source root, excluding the filename. Package names do not include the class name or the source root directory (src).

---

##### MCQ 3 (Beginner)
##### What is the primary purpose of packages in Java?
##### A) To increase execution speed of programs
##### B) To organize classes and interfaces and prevent naming conflicts
##### C) To reduce the size of compiled bytecode
##### D) To automatically import all Java classes
###### Answer: B) To organize classes and interfaces and prevent naming conflicts
###### Explanation: Packages are primarily an organizational and namespace mechanism. They group related classes/interfaces and prevent naming conflicts by ensuring each class has a unique fully qualified name. They do not affect execution speed or bytecode size, nor do they import classes automatically (except java.lang).

---

##### MCQ 4 (Beginner)
##### Which of the following is a valid package naming convention?
##### A) Package.MyApp.Service
##### B) com.Company.MyApp
##### C) com.company.myapp
##### D) com company myapp
###### Answer: C) com.company.myapp
###### Explanation: Package names should be all lowercase with words separated by dots (not spaces). While Java technically allows uppercase letters, the convention (and best practice) is to use lowercase only.

---

##### MCQ 5 (Beginner)
##### What is the fully qualified name of the ArrayList class?
##### A) ArrayList
##### B) util.ArrayList
##### C) java.util.ArrayList
##### D) java.lang.util.ArrayList
###### Answer: C) java.util.ArrayList
###### Explanation: The fully qualified name includes the complete package path followed by the class name. ArrayList resides in the java.util package, so its fully qualified name is java.util.ArrayList.

---

##### MCQ 6 (Beginner)
##### Can you import a class from the unnamed (default) package into a class that has a package declaration?
##### A) Yes, using import DefaultPackageClass;
##### B) Yes, using import .DefaultPackageClass;
##### C) No, classes in the unnamed package cannot be imported
##### D) Yes, but only if both files are in the same directory
###### Answer: C) No, classes in the unnamed package cannot be imported
###### Explanation: Classes in the unnamed package are not importable by classes in named packages. This is a deliberate design restriction to discourage use of the unnamed package. If you need to use a class across packages, it must have a package declaration.

---

##### MCQ (Beginner)
##### Which Java version introduced the static import feature?
##### A) Java 1.4  
##### B) Java 5  
##### C) Java 7  
##### D) Java 8
###### Answer: B) Java 5  
###### Explanation: Static import was introduced in Java 5 (2004) alongside other major features like generics, enhanced for-loop, autoboxing, enums, and varargs. The feature has remained unchanged through Java 25.

---

##### MCQ 7 (Intermediate)
##### What happens if you declare a class in package com.app.service and try to access a package-private class from package com.app.model?
##### A) Compilation succeeds—classes in subpackages have access
##### B) Compilation fails—different packages have no access to package-private members
##### C) Runtime exception is thrown
##### D) The JVM auto-imports the required class
###### Answer: B) Compilation fails—different packages have no access to package-private members
###### Explanation: Package-private (default) access restricts visibility to the same package only. com.app.service and com.app.model are completely different packages despite the naming similarity—there is no subpackage relationship in Java.

---

##### MCQ 8 (Intermediate)
##### Which statement about import statements is TRUE?
##### A) Imports are processed at runtime by the JVM
##### B) Wildcard imports (import java.util.*;) load all classes from the package into memory
##### C) Imports are compile-time syntactic sugar with no runtime effect
##### D) Importing the same class twice causes a compilation error
###### Answer: C) Imports are compile-time syntactic sugar with no runtime effect
###### Explanation: Import statements are purely a compile-time feature. The compiler uses them to resolve class names to fully qualified names. At runtime, the bytecode contains only fully qualified names—import statements don't exist. Wildcard imports don't load classes into memory; they just help the compiler resolve names.

---

##### MCQ 9 (Intermediate)
##### What is the unnamed (default) package in Java?
##### A) The package used when no package declaration is specified
##### B) A special package that can be imported by all other packages
##### C) A package automatically created for built-in classes
##### D) Another name for java.lang
###### Answer: A) The package used when no package declaration is specified
###### Explanation: The unnamed package is where classes without a package declaration reside. It's primarily for simple learning exercises. Classes in the unnamed package cannot be imported by classes in named packages, making it unsuitable for production code.

---

##### MCQ 10 (Intermediate)
##### If you have two classes java.util.Date and java.sql.Date, and you import both with wildcards (import java.util.*; import java.sql.*;), what happens when you use Date in your code?
##### A) The compiler uses java.util.Date because it was imported first
##### B) The compiler uses java.sql.Date because it was imported last
##### C) Compilation error due to ambiguous reference
##### D) Runtime exception is thrown
###### Answer: C) Compilation error due to ambiguous reference
###### Explanation: When wildcard imports from two packages both contain a class with the same name, using the simple name creates an ambiguity that the compiler cannot resolve. You must use the fully qualified name for at least one of them, or import one specifically.

---

##### MCQ 11 (Intermediate)
##### Which tool can detect circular package dependencies in a Java project?
##### A) javac
##### B) jdeps
##### C) jar
##### D) javap
###### Answer: B) jdeps
###### Explanation: jdeps (Java Dependency Analysis Tool) analyzes class dependencies and can detect cycles. javac compiles code but doesn't analyze package-level architecture. jar creates archives. javap disassembles class files. jdeps has been available since Java 8 and is part of the standard JDK.

---

##### MCQ 12 (Intermediate)
##### Which statement about classpath order is TRUE?
##### A) The JVM loads classes from all matching locations and merges them
##### B) The JVM loads the first matching class file found and stops searching
##### C) The JVM loads the last matching class file found (last-wins strategy)
##### D) The JVM throws an exception if multiple matching classes exist
###### Answer: B) The JVM loads the first matching class file found and stops searching
###### Explanation: When searching for a class, the JVM (via the classloader) searches classpath entries in order and loads the first match. This is called "classpath shadowing"—later versions of a class in the classpath are ignored if an earlier match exists. This behavior is unchanged till Java 25.

---

##### MCQ (Intermediate)
##### What is the primary purpose of static import in Java?
##### A) To import entire packages without typing `import` for each class  
##### B) To access static members of a class without qualifying them with the class name  
##### C) To make classes load faster at runtime  
##### D) To allow importing private static methods
###### Answer: B) To access static members of a class without qualifying them with the class name  
###### Explanation: Static import (introduced in Java 5) allows you to access static members (fields and methods) directly without the class name prefix. For example, `import static java.lang.Math.PI;` lets you use `PI` instead of `Math.PI`. It does not affect runtime performance (purely compile-time) and only works with static members that are accessible based on normal access rules.

---

##### MCQ 13 (Advanced)
##### What is package sealing in Java?
##### A) A mechanism to prevent modification of package contents at runtime
##### B) A JAR manifest feature that restricts a package to being loaded from a single JAR file
##### C) A way to encrypt all classes in a package
##### D) A technique to compress package bytecode
###### Answer: B) A JAR manifest feature that restricts a package to being loaded from a single JAR file
###### Explanation: Package sealing is a security feature defined in JAR manifest files. When a package is sealed, the classloader ensures all classes from that package come from the same JAR. Attempting to load from a second JAR results in a SecurityException. This prevents package splitting attacks.

---

##### MCQ 14 (Advanced)
##### In the module system (Java 9+), what advantage do modules provide over packages?
##### A) Modules eliminate the need for packages entirely
##### B) Modules provide stronger encapsulation by hiding internal packages from external access
##### C) Modules run faster than packages
##### D) Modules use less memory than packages
###### Answer: B) Modules provide stronger encapsulation by hiding internal packages from external access
###### Explanation: The module system (JPMS) allows you to explicitly declare which packages are exported (visible to other modules) and which are internal. This provides stronger encapsulation than packages alone, where any public class is accessible if you can reach it via the classpath. Modules don't eliminate packages, nor do they inherently improve performance or memory usage.

---

##### MCQ 15 (Advanced)
##### Where is package metadata stored in the JVM (Java 8+)?
##### A) Heap
##### B) Stack
##### C) Metaspace
##### D) Code Cache
###### Answer: C) Metaspace
###### Explanation: In Java 8 and later, class metadata (including package information) is stored in Metaspace, which is part of native memory, not the heap. In Java 7 and earlier, this was stored in the Permanent Generation (PermGen), which was part of the heap. This change improved memory management for class metadata.

---

##### MCQ (Advanced)
##### What happens when you have two static imports with the same member name from different classes?
##### A) The JVM chooses the first one found in the classpath  
##### B) Compilation error due to ambiguous reference  
##### C) The member from the alphabetically first class is used  
##### D) Runtime exception is thrown when the member is accessed 
###### Answer:B) Compilation error due to ambiguous reference  
###### Explanation: If you static import members with identical names from two different classes (e.g., `import static ClassA.MAX_VALUE;` and `import static ClassB.MAX_VALUE;`), the compiler cannot resolve which one to use and reports an ambiguous reference error. You must either use a fully qualified name or import only one of them. This is a compile-time check, not a runtime issue.

---