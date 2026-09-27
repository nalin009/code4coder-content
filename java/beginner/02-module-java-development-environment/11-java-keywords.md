## 11. Java Keywords

---

#### 11.1 What Are Keywords?
**Definition:** Reserved words with predefined meanings in Java. They cannot be used as identifiers (variable names, method names, class names).

---

#### 11.2 Complete List of Java Keywords (as of Java 25)
###### **Total: 53 keywords**

|**Category**|**Keywords**|
|------------|------------|
| **Access Modifiers** | `public`, `private`, `protected` |
| **Class/Object/Interface** | `class`, `interface`, `extends`, `implements`, `new`, `this`, `super` |
| **Data Types** | `byte`, `short`, `int`, `long`, `float`, `double`, `char`, `boolean`, `void` |
| **Control Flow** | `if`, `else`, `switch`, `case`, `default`, `for`, `while`, `do`, `break`, `continue`, `return` |
| **Exception Handling** | `try`, `catch`, `finally`, `throw`, `throws` |
| **Modifiers** | `static`, `final`, `abstract`, `synchronized`, `volatile`, `transient`, `native`, `strictfp` |
| **Package** | `package`, `import` |
| **Unused/Reserved** | `goto`, `const` |
| **Type Testing** | `instanceof` |
| **Assertions** | `assert` |
| **Enums** | `enum` |
| **Module System (Java 9+)** | `module`, `requires`, `exports`, `opens`, `provides`, `uses`, `with`, `to`, `transitive`, `open` |
| **Records (Java 16+)** | `record` |
| **Sealed Classes (Java 17+)** | `sealed`, `permits`, `non-sealed` |
| **Boolean Literals** | `true`, `false` |
| **Null Literal** | `null` |

###### **Note on Context-Sensitive Keywords (NOT Reserved Keywords):**
- `var` (Java 10+): Used for local variable type inference. NOT a reserved keyword; can be used as identifier except for class/interface names.
- `yield` (Java 14+): Used in switch expressions. Contextual keyword.
- `_` (Java 21+): Used for unnamed patterns and variables. Reserved as a single-character identifier since Java 10.

---

#### 11.3 Key Observations
#### Reserved but Unused:
- goto and const are reserved but not used in Java (kept for potential future use).

#### Context-Sensitive Keywords:
- **`var` (local variable type inference, Java 10+):** Not a reserved keyword; can be used as a method/variable name in some contexts.
- `yield` (switch expressions, Java 13+): Contextual keyword.

#### Case Sensitivity:
- Keywords are always lowercase.
- Public or PUBLIC are NOT keywords—they're valid identifiers.

**Unchanged Till Java 25:** Core keywords remain the same. New keywords (record, sealed, etc.) were added in recent versions but the original 50 keywords remain unchanged.