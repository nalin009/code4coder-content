### 6. Real-World Use Cases
#### Beginner Level:
##### 1. Multiplication Table:

```java
for (int i = 1; i <= 10; i++) {
    System.out.println("5 x " + i + " = " + (5 * i));
}
```

##### 2. Sum of Array:

```java
int[] numbers = {10, 20, 30, 40, 50};
int sum = 0;
for (int num : numbers) {
    sum += num;
}
System.out.println("Sum: " + sum);
```

##### 3. Count Even Numbers:

```java
int[] numbers = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
int count = 0;
for (int num : numbers) {
    if (num % 2 == 0) count++;
}
System.out.println("Even numbers: " + count);
```

#### Interview Level:
##### 1. Palindrome Check:

```java
String str = "radar";
boolean isPalindrome = true;
for (int i = 0; i < str.length() / 2; i++) {
    if (str.charAt(i) != str.charAt(str.length() - 1 - i)) {
        isPalindrome = false;
        break;
    }
}
```

##### 2. Find Largest Element:

```java
int[] arr = {45, 23, 78, 12, 90, 34};
int max = arr[0];
for (int i = 1; i < arr.length; i++) {
    if (arr[i] > max) {
        max = arr[i];
    }
}
```

##### 3. Armstrong Number:
```java
int num = 153;
int original = num, sum = 0;
while (num > 0) {
    int digit = num % 10;
    sum += digit * digit * digit;
    num /= 10;
}
boolean isArmstrong = (sum == original);
```

#### Production Level:
##### Batch Processing:

```java
List<Order> orders = getOrders();
for (Order order : orders) {
    try {
        processOrder(order);
    } catch (Exception e) {
        logger.error("Failed to process order: " + order.getId(), e);
        continue;  // Skip failed order, process rest
    }
}
```

##### Pagination:

```java
int pageSize = 100;
int offset = 0;
while (true) {
    List<Record> records = database.fetchRecords(offset, pageSize);
    if (records.isEmpty()) break;
    
    for (Record record : records) {
        process(record);
    }
    offset += pageSize;
}
```

##### Retry Logic:

```java
int maxRetries = 3;
int attempt = 0;
boolean success = false;

while (attempt < maxRetries && !success) {
    try {
        makeApiCall();
        success = true;
    } catch (NetworkException e) {
        attempt++;
        if (attempt >= maxRetries) {
            throw new RuntimeException("Max retries exceeded", e);
        }
        Thread.sleep(1000 * attempt);  // Exponential backoff
    }
}
```


---
---