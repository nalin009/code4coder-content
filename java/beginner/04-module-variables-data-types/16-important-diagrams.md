## 16. Important Diagrams (Described in Words)

---

#### Diagram 1: Variable Types and Memory Locations

**Description**:
- Draw three sections: **Stack**, **Heap**, **Metaspace**.
- **Stack**: Show local variables (`int x`, `String ref`).
- **Heap**: Show objects (`String object`, `Integer object`, instance variables inside objects).
- **Metaspace**: Show static variables (`static int count`).
- Use arrows from stack references to heap objects.

---

#### Diagram 2: Primitive Data Type Sizes

**Description**:
- Draw a horizontal bar chart showing the size of each primitive type:
  - `byte`: 1 byte
  - `short`: 2 bytes
  - `int`: 4 bytes
  - `long`: 8 bytes
  - `float`: 4 bytes
  - `double`: 8 bytes
  - `char`: 2 bytes
  - `boolean`: 1 bit (or 1 byte in practice)

---

#### Diagram 3: Type Casting (Implicit vs Explicit)

**Description**:
- Draw two flowcharts:
  1. **Implicit Casting**: `byte → short → int → long → float → double` (automatic, no data loss).
  2. **Explicit Casting**: Reverse direction, manual, potential data loss.

---

#### Diagram 4: Autoboxing and Unboxing

**Description**:
- Draw two boxes: **Primitive** and **Wrapper**.
- Show arrows:
  - **Autoboxing**: `int` → `Integer` (compiler adds `Integer.valueOf()`)
  - **Unboxing**: `Integer` → `int` (compiler adds `.intValue()`)

---

#### Diagram 5: Wrapper Class Caching

**Description**:
- Draw a cache box labeled "Integer Cache (-128 to 127)".
- Show two scenarios:
  1. `Integer a = 100; Integer b = 100;` → Both point to the same cached object.
  2. `Integer c = 200; Integer d = 200;` → Two different objects on the heap.