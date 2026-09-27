### 9. Best Practices (5+ YOE Expectation)
#### 1. Choose the Right Loop Type

```java
// Known iterations → for loop
for (int i = 0; i < 10; i++) { }

// Unknown iterations → while loop
while (!queue.isEmpty()) { }

// At least one execution → do-while
do { } while (condition);

// Collection iteration → enhanced for
for (String name : names) { }
```

#### 2. Cache Collection Size

```java
// AVOID
for (int i = 0; i < list.size(); i++) { }

// PREFER
int size = list.size();
for (int i = 0; i < size; i++) { }

// OR USE enhanced for
for (String item : list) { }
```

#### 3. Use Enhanced For Loop When Possible

```java
// Less code, cleaner, no index errors
for (String name : names) {
    process(name);
}
```

#### 4. Break Out of Nested Loops with Labels

```java
outer: for (int i = 0; i < 10; i++) {
    for (int j = 0; j < 10; j++) {
        if (found(i, j)) {
            break outer;
        }
    }
}
```

#### 5. Avoid Deep Nesting

```java
// BAD: Hard to read
for (...) {
    for (...) {
        for (...) {
            for (...) {
                // Code
            }
        }
    }
}

// BETTER: Extract to methods
for (...) {
    processRow(row);
}
```

#### 6. Use continue to Reduce Nesting

```java
// BEFORE
for (String item : items) {
    if (item != null) {
        if (!item.isEmpty()) {
            if (item.startsWith("A")) {
                process(item);
            }
        }
    }
}

// AFTER
for (String item : items) {
    if (item == null) continue;
    if (item.isEmpty()) continue;
    if (!item.startsWith("A")) continue;
    process(item);
}
```

#### 7. Document Intentional Infinite Loops

```java
while (true) {  // Intentional infinite loop - server accepts connections
    Connection conn = server.accept();
    if (conn == null) break;
    handleConnection(conn);
}
```

#### 8. Avoid Creating Objects in Tight Loops

```java
// BAD
for (int i = 0; i < 10000; i++) {
    StringBuilder sb = new StringBuilder();  // 10000 objects created
    sb.append("Hello");
}

// GOOD
StringBuilder sb = new StringBuilder();  // Reuse
for (int i = 0; i < 10000; i++) {
    sb.setLength(0);  // Reset
    sb.append("Hello");
}
```

#### 9. Use Descriptive Loop Variables

```java
// OK for simple loops
for (int i = 0; i < n; i++) { }

// BETTER for clarity
for (int rowIndex = 0; rowIndex < rows.length; rowIndex++) { }
for (User user : users) { }
```

#### 10. Consider Stream API for Collection Operations (Java 8+)

```java
// Traditional loop
List<String> filtered = new ArrayList<>();
for (String name : names) {
    if (name.startsWith("A")) {
        filtered.add(name.toUpperCase());
    }
}

// Functional approach
List<String> filtered = names.stream()
    .filter(name -> name.startsWith("A"))
    .map(String::toUpperCase)
    .collect(Collectors.toList());
```

---
---