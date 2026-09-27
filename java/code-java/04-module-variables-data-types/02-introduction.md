## 2. Introduction

---

#### 2.1. Why This Topic Exists
Every program processes data—whether it's calculating a salary, storing a user's name, or tracking inventory. Variables are named memory locations that hold data, and data types define what kind of data can be stored and how much memory is needed.
Java is a statically-typed language, meaning every variable must have a declared type at compile-time. This design choice prevents many runtime errors and makes code more predictable and maintainable.

---

#### 2.2. What Problem Java Is Solving
###### **Without variables, you cannot:**
- Store user input
- Perform calculations
- Track program state
- Pass information between methods

###### **Without data types, the compiler wouldn't know:**
- How much memory to allocate
- What operations are valid (you can't add a number to a boolean)
- How to interpret the bits stored in memory

---

#### 2.3. Why Beginners Struggle With This Topic
###### **Beginners often:**
- Confuse declaration with initialization
- Don't understand why int and Integer are different
- Misuse type casting, causing data loss
- Forget that variables have scope and lifetime
- Don't grasp the difference between primitive and reference types

---

#### 2.4. Why Interviewers Ask This (Especially 3–5+ YOE)
###### **For experienced developers, interviewers probe:**
- **Memory management:** Where are primitives vs objects stored?
- **Performance implications:** Why use int over Integer?
- **Autoboxing overhead:** When does it happen? What's the cost?
- **Thread safety:** Are static variables thread-safe?
- **Immutability:** Why are wrapper classes immutable?