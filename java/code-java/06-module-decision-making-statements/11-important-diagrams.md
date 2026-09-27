## 11. Important Diagrams (Described in Words)

---

#### Diagram 11.1: If Statement Flow

```java
Start → Evaluate Condition → True? → Execute Block → Continue
                           → False? → Skip Block → Continue
```

---

#### Diagram 11.2: If-Else Flow

```java
Start → Evaluate Condition → True? → Execute If Block → End
                           → False? → Execute Else Block → End
```

---

#### Diagram 11.3: Else-If Ladder Flow

```java
Start → Condition1? → True → Block1 → End
                    → False → Condition2? → True → Block2 → End
                                         → False → Condition3? → True → Block3 → End
                                                              → False → Default Block → End
```

---

#### Diagram 11.4: Switch Statement Flow (Traditional)

```java
Start → Evaluate Expression → 
        Case 1 Match? → Execute → Break → End
        Case 2 Match? → Execute → Break → End
        Case 3 Match? → Execute → Break → End
        No Match? → Default → End
```

---

#### Diagram 11.5: Switch Expression Flow (Java 14+)

```java
Start → Evaluate Expression → 
        Case 1 Match? → Return Value1 → End
        Case 2 Match? → Return Value2 → End
        Case 3 Match? → Return Value3 → End
        No Match? → Return Default → End
```

---

#### Diagram 11.6: Ternary Operator Flow

```java
Start → Evaluate Condition → True? → Return Expression1 → End
                            → False? → Return Expression2 → End
```