# 02 — Memory in Java: Stack, Heap, DMA & Garbage Collector

> Most students skip this topic and struggle later. Understand this once, and OOP + arrays + references will feel easy forever.

---

## 1. Why should you care about memory?

When your program runs, JVM needs space in RAM to store:
- your variables,
- your method calls,
- your objects and arrays.

JVM divides this space into **two main areas**: **Stack** and **Heap**.

---

## 2. Stack Memory (the plates 🍽️)

### Analogy: A stack of plates
You can only put a plate on **top**, and remove from the **top**. This is called **LIFO** (Last In, First Out).

### What goes in Stack?
- **Local variables** (variables inside methods) — like `int a = 5;`
- **Method calls** — every time a method is called, a new "frame" (box) is placed on the stack. When the method finishes, its box is removed automatically.
- **References** to objects (the "address slip" of objects, not the objects themselves).

### Properties:
- Very **fast**.
- **Small** in size.
- Memory is freed **automatically** when a method ends.
- Each thread has its **own** stack.

---

## 3. Heap Memory (the warehouse 🏭)

### Analogy: A big warehouse
Big storage area where things can be kept for a long time, in any order. Finding things is a bit slower, and a cleaner (Garbage Collector) removes unused stuff.

### What goes in Heap?
- **All objects** — anything created with the `new` keyword.
- **Arrays** (arrays are objects in Java!).
- **Instance variables** (variables inside objects).

### Properties:
- **Bigger** but **slower** than stack.
- Shared by the **whole program** (all threads).
- Cleaned automatically by the **Garbage Collector**.

---

## 4. Example: See exactly what goes where

```java
public class Main {
    public static void main(String[] args) {
        int age = 20;                  // Stack (local primitive variable)
        int[] marks = new int[3];      // 'marks' reference → Stack, actual array → Heap
        String name = "Ashu";          // 'name' reference → Stack, String object → Heap
    }
}
```

### Memory picture:

```
        STACK                         HEAP
┌─────────────────────┐      ┌──────────────────────┐
│ main() frame:       │      │                      │
│  age   = 20         │      │  [0, 0, 0]  ← array  │
│  marks = @101 ──────┼─────→│  (at address @101)   │
│  name  = @205 ──────┼─────→│  "Ashu"              │
│                     │      │  (at address @205)   │
└─────────────────────┘      └──────────────────────┘
```

💡 **Key idea:** `marks` does NOT contain the array. It contains the **address** of the array (like a home address slip). The real array lives in the Heap.

---

## 5. DMA — Dynamic Memory Allocation (the `new` keyword)

**DMA = asking for memory while the program is RUNNING (at runtime), not before.**

```java
int[] arr = new int[n];   // size decided at runtime — this is DMA
```

- In C/C++, you use `malloc()` / `new` and you must **free the memory yourself** (dangerous, easy to make mistakes).
- In Java, `new` allocates memory in the **Heap**, and freeing is done **automatically** by the Garbage Collector. 🎉

**Every time you write `new` → memory is allocated in the Heap. Simple rule.**

---

## 6. Garbage Collector (GC) — Java's automatic cleaner 🧹

When an object in the Heap has **no reference pointing to it**, it becomes garbage.

```java
String name = new String("Ashu");
name = null;   // now nobody points to "Ashu" object → it becomes garbage
```

The **Garbage Collector** runs automatically in the background and frees such memory. You don't (and can't) free memory manually in Java.

---

## 7. Two famous memory errors

| Error | When it happens | Example cause |
|-------|-----------------|---------------|
| `StackOverflowError` | Stack gets full | A method calling itself forever (infinite recursion) |
| `OutOfMemoryError` | Heap gets full | Creating too many objects that are never freed |

```java
// StackOverflowError example (never do this!)
static void hello() {
    hello();   // calls itself forever → stack full → crash
}
```

---

## 8. Stack vs Heap — Final comparison table ⚡

| Feature | Stack | Heap |
|---------|-------|------|
| Stores | Local variables, method calls, references | Objects, arrays, instance variables |
| Speed | Very fast | Slower |
| Size | Small | Large |
| Cleanup | Automatic (method ends → gone) | Garbage Collector |
| Sharing | One per thread | Shared by whole program |
| Error when full | `StackOverflowError` | `OutOfMemoryError` |

---

## 9. Quick Revision (30 seconds) ⚡

- **Stack** = plates (LIFO) → local variables + method calls. Fast, small, auto-cleaned.
- **Heap** = warehouse → all `new` objects + arrays. Big, GC-cleaned.
- References live in Stack; real objects live in Heap.
- `new` = DMA = runtime memory allocation in Heap.
- Infinite recursion → `StackOverflowError`; too many objects → `OutOfMemoryError`.

---

⬅️ **Previous:** [01 — Java Basics](01-java-basics.md) | ➡️ **Next:** 03 — Variables & Data Types (coming soon)
