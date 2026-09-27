## 8. Important Diagrams (Described in Words)

---

#### Diagram 1: Java Program Structure Hierarchy

```java
Program
└── Package (optional)
    └── Import Statements (optional)
        └── Class (one or more)
            └── Fields (class variables)
            └── Constructors
            └── Methods
                └── main method (entry point)
                    └── Statements
                        └── Blocks
                            └── Nested Blocks
```

---

#### Diagram 2: Scope Visualization

```java
Method Scope
├── Variable A (accessible everywhere in method)
│
├── Block 1
│   ├── Variable B (accessible only in Block 1 and nested blocks)
│   │
│   └── Nested Block 1.1
│       └── Variable C (accessible only in Block 1.1)
│
└── Block 2
    └── Variable D (accessible only in Block 2)
    
When blocks end, variables are destroyed from inner to outer.
```

---

#### Diagram 3: Statement Execution Flow

```java
Program Start
    ↓
main method called
    ↓
Statement 1 executed
    ↓
Statement 2 executed
    ↓
Block entered
    ↓
Statements inside block executed
    ↓
Block exited (variables destroyed)
    ↓
Continue with remaining statements
    ↓
main method ends
    ↓
Program terminates
```