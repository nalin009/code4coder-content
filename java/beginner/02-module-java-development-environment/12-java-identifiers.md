## 12. Java Identifiers

---

#### 12.1. What Are Identifiers?
**Definition:** Names given to `variables`, `methods`, `classes`, `packages`, `interfaces`, etc.

```java
int age;              // 'age' is an identifier
void calculate() {}   // 'calculate' is an identifier
class Student {}      // 'Student' is an identifier
```

---

#### 12.2. Rules for Identifiers (Compiler-Enforced)
##### **Rule 1: Valid Characters**
- **Can contain:** letters (A-Z, a-z), digits (0-9), underscore (_), dollar sign ($).
- Cannot start with a digit.
- **Examples:**
  - **Valid:** `age`, `_name`, `$value`, `total123`, `_123`
  - **Invalid:** 123total, @name, total-amount

##### **Rule 2: No Keywords**
- Cannot use Java keywords as identifiers.
- **Invalid:** int, class, public, void

##### **Rule 3: Case Sensitive**
- age, Age, AGE are three different identifiers.

##### **Rule 4: No Length Limit**
- Identifiers can be of any length (theoretically unlimited, practically limited by memory).

##### **Rule 5: Unicode Support**
- Java supports Unicode, so identifiers can include non-English characters.
- **Example:** `int सं ख्या = 10;` (Hindi characters) is valid but NOT recommended.

---

#### 12.3. Conventions (Not Compiler-Enforced, but Industry Standard)
##### Classes/Interfaces:
- PascalCase (first letter of each word capitalized).
- **Examples:** Student, HelloWorld, EmployeeDetails

##### Methods/Variables:
- camelCase (first word lowercase, subsequent words capitalized).
- **Examples:** calculateSalary, employeeName, totalAmount

##### Constants:
- ALL_UPPERCASE with underscores.
- **Examples:** MAX_VALUE, PI, DEFAULT_SIZE

##### Packages:
- All lowercase, often reverse domain name.
- **Examples:** com.company.project, java.util, org.apache.commons

##### Why Conventions Matter:
- Improves code readability.
- Industry-standard; violating conventions in professional code is considered unprofessional.
- Interviewers often check adherence to naming conventions.