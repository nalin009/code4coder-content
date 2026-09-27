## 7. Size and Range of Data Types
The sizes and ranges of primitive types have been consistent since Java 1.0 and remain unchanged in Java 25.

---

#### 7.1. Memory Size Calculation:
- **byte**= 1 byte = 8 bits → 2⁸ = 256 values (-128 to 127)
- **short** = 2 bytes = 16 bits → 2¹⁶ = 65,536 values (-32,768 to 32,767)
- **int** = 4 bytes = 32 bits → 2³² = ~4.3 billion values
- **long**= 8 bytes = 64 bits → 2⁶⁴ = ~18 quintillion values

---

#### 7.2. Why This Matters:
- Choosing the wrong type can waste memory (using long when int suffices)
- Or cause overflow errors (using int for large numbers)