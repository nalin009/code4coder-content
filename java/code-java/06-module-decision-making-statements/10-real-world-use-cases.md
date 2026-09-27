## 10. Real-World Use Cases

---

#### Beginner Level:
##### Age Verification:

```java
int age = 16;
if (age >= 18) {
    System.out.println("Can vote");
} else {
    System.out.println("Cannot vote");
}
```

##### Grade Calculator:

```java
int marks = 75;
String grade;
if (marks >= 90) {
    grade = "A";
} else if (marks >= 75) {
    grade = "B";
} else if (marks >= 60) {
    grade = "C";
} else {
    grade = "F";
}
```

##### Day of Week:

```java
int day = 3;
switch (day) {
    case 1 -> System.out.println("Monday");
    case 2 -> System.out.println("Tuesday");
    case 3 -> System.out.println("Wednesday");
    default -> System.out.println("Other day");
}
```

---

#### Interview Level:
##### Leap Year Check:

```java
int year = 2024;
if ((year % 4 == 0 && year % 100 != 0) || (year % 400 == 0)) {
    System.out.println("Leap year");
} else {
    System.out.println("Not a leap year");
}
```

##### Largest of Three Numbers:

```java
int a = 10, b = 20, c = 15;
int largest = (a > b) ? ((a > c) ? a : c) : ((b > c) ? b : c);
System.out.println("Largest: " + largest);
```

##### Character Type Check:

```java
char ch = 'A';
if (ch >= 'a' && ch <= 'z') {
    System.out.println("Lowercase");
} else if (ch >= 'A' && ch <= 'Z') {
    System.out.println("Uppercase");
} else if (ch >= '0' && ch <= '9') {
    System.out.println("Digit");
} else {
    System.out.println("Special character");
}
```

---

#### Production Level:
##### HTTP Status Code Handling:

```java
String handleResponse(int statusCode) {
    return switch (statusCode) {
        case 200, 201, 204 -> "Success";
        case 400, 401, 403, 404 -> "Client error";
        case 500, 502, 503 -> "Server error";
        default -> "Unknown status: " + statusCode;
    };
}
```

##### User Role Authorization:

```java
boolean hasAccess(String role, String resource) {
    return switch (role) {
        case "ADMIN" -> true;
        case "USER" -> resource.equals("read") || resource.equals("write");
        case "GUEST" -> resource.equals("read");
        default -> false;
    };
}
```

##### Payment Method Selection:

```java
void processPayment(String method, double amount) {
    switch (method.toUpperCase()) {
        case "CREDIT_CARD":
            processCreditCard(amount);
            break;
        case "DEBIT_CARD":
            processDebitCard(amount);
            break;
        case "UPI":
            processUPI(amount);
            break;
        case "NET_BANKING":
            processNetBanking(amount);
            break;
        default:
            throw new IllegalArgumentException("Invalid payment method: " + method);
    }
}
```