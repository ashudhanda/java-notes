# 14 — Collections: Smart Containers 📦

> Arrays ki problem yaad hai? **Size FIXED hota hai.** 50 students ka array banaya, 51st aa gaya → phas gaye! Collections = self-adjusting, feature-packed containers. Real projects me 90% yahi use hote hain.

---

## 1. Array ki problem → Collections ka solution

```java
int[] arr = new int[3];     // size 3 FIXED — badal nahi sakte
arr[3] = 40;                // 💥 ArrayIndexOutOfBoundsException (note 06!)
```

**Collections:** size apne aap badhta-ghatta hai, add/remove/search ready-made methods, sab kuch built-in!

### The big 3 (95% kaam inhi se):

| Collection | Kya hai | Analogy |
|-----------|---------|--------|
| `ArrayList` | resizable list (order maintained, duplicates OK) | 👜 stretchable shopping bag |
| `HashSet` | unique items only (no order) | 🆔 Aadhaar system — duplicate entry impossible |
| `HashMap` | key → value pairs | 📖 dictionary — word se meaning |

---

## 2. ArrayList — the stretchable array 👜

```java
import java.util.ArrayList;    // import karna padta hai!

ArrayList<String> fruits = new ArrayList<>();

fruits.add("Apple");           // [Apple]
fruits.add("Banana");          // [Apple, Banana]
fruits.add("Mango");           // [Apple, Banana, Mango]
fruits.add("Apple");           // [Apple, Banana, Mango, Apple] — duplicates OK!

System.out.println(fruits.get(0));        // Apple (index se access — array jaisa)
System.out.println(fruits.size());        // 4 (size(), not length!)
fruits.remove("Banana");                  // [Apple, Mango, Apple]
fruits.set(0, "Orange");                  // [Orange, Mango, Apple] — replace
System.out.println(fruits.contains("Mango"));   // true

// Loop — dono tarike (note 05/06 wale hi!)
for (String f : fruits) System.out.println(f);
for (int i = 0; i < fruits.size(); i++) System.out.println(fruits.get(i));
```

### `<String>` kya hai? — Generics (simple words)
`ArrayList<String>` = "is list me SIRF String aayenge". Type-safety ka guard — galti se number daala toh compile error (runtime surprise nahi!).

### ⚠️ Primitives directly nahi — wrapper classes:

| Primitive | Wrapper |
|-----------|--------|
| `int` | `Integer` |
| `double` | `Double` |
| `char` | `Character` |
| `boolean` | `Boolean` |

```java
ArrayList<Integer> marks = new ArrayList<>();   // ArrayList<int> ❌ nahi chalta
marks.add(85);        // int → Integer automatic (autoboxing — Java khud kar deta hai)
int first = marks.get(0);    // Integer → int automatic (unboxing)
```

### Array vs ArrayList:

| | Array | ArrayList |
|--|-------|-----------|
| Size | fixed | auto-grow/shrink |
| Syntax | `arr[0]` | `list.get(0)` |
| Length | `arr.length` | `list.size()` |
| Primitives | ✅ direct | wrapper classes se |
| Methods | kuch nahi | add, remove, contains... |

---

## 3. HashSet — duplicates ka dushman 🆔

```java
import java.util.HashSet;

HashSet<String> voters = new HashSet<>();
voters.add("Ashu");      // true — added
voters.add("Rahul");     // true — added
voters.add("Ashu");      // false — REJECTED! Duplicate 🚫

System.out.println(voters.size());       // 2 (not 3!)
System.out.println(voters.contains("Ashu"));   // true — SUPER FAST lookup
```

### Kab use karo?
- **Duplicates hatane** hain → list ko Set me daal do:
```java
ArrayList<Integer> nums = new ArrayList<>(List.of(1, 2, 2, 3, 3, 3));
HashSet<Integer> unique = new HashSet<>(nums);    // {1, 2, 3} — one line!
```
- **"Kya ye pehle aaya hai?"** check karna hai → `contains()` bijli ki speed se (array me loop lagana padta — slow!)

⚠️ Order maintain NAHI hota — jo daala usi order me wapas milega guarantee nahi.

---

## 4. HashMap — key se value nikalo 📖

**Har entry = pair: KEY (unique) → VALUE.** Roll number se student, word se meaning, username se password.

```java
import java.util.HashMap;

HashMap<Integer, String> students = new HashMap<>();   // key=roll, value=name

students.put(1, "Ashu");        // 1 → Ashu
students.put(2, "Rahul");       // 2 → Rahul
students.put(3, "Priya");       // 3 → Priya
students.put(2, "Rohan");       // key 2 PEHLE se tha → value REPLACE (Rahul → Rohan!)

System.out.println(students.get(1));         // Ashu (key do, value lo)
System.out.println(students.get(99));        // null (key nahi mili)
System.out.println(students.containsKey(3)); // true
students.remove(3);                          // Priya gayi
System.out.println(students.size());         // 2

// HashMap pe loop:
for (Integer roll : students.keySet()) {
    System.out.println(roll + " → " + students.get(roll));
}
// Ya behtar — entrySet:
for (var entry : students.entrySet()) {
    System.out.println(entry.getKey() + " → " + entry.getValue());
}
```

### 🏭 Analogy: Cloakroom 🎫
Bag jama karo → token milta hai (KEY). Wapsi pe token do → APNA bag milta hai (VALUE). Token unique hota hai — do logo ka same token impossible (key unique!). Naya bag same token pe rakha → purana replace!

### THE classic pattern: frequency counting (interview me 100% aayega 🎯)

```java
String s = "programming";
HashMap<Character, Integer> freq = new HashMap<>();

for (int i = 0; i < s.length(); i++) {
    char c = s.charAt(i);                       // note 07 ka charAt!
    freq.put(c, freq.getOrDefault(c, 0) + 1);   // hai toh +1, nahi toh 0+1
}
System.out.println(freq);
// {p=1, r=2, o=1, g=2, a=1, m=2, i=1, n=1}
```

`getOrDefault(c, 0)` = "c ki value do, nahi hai toh 0" — ye ek line frequency counting ka dil hai. Ise yaad kar lo, questions section me baar-baar milega!

---

## 5. Kaunsa collection kab? (decision guide)

```
Order chahiye + index se access?        → ArrayList
Sirf unique items / fast "exists?"      → HashSet
Key se value (id→naam, word→meaning)?  → HashMap
```

| Kaam | Best choice |
|------|-------------|
| Students ki list, order matters | `ArrayList` |
| Vote kar chuke logo ka record | `HashSet` |
| Roll no → marks mapping | `HashMap` |
| Shopping cart items | `ArrayList` |
| Visited pages (unique) | `HashSet` |
| Username → password | `HashMap` |

💡 **Interview point:** `List`, `Set`, `Map` INTERFACES hain (note 12!); `ArrayList`, `HashSet`, `HashMap` unke implementations. Isliye pro log likhte hain: `List<String> list = new ArrayList<>();` — interface reference, implementation object (polymorphism — note 11!).

---

## 6. Common Beginner Mistakes ❌

1. `list.get(i)` array syntax se: `list[i]` → ❌ collections me brackets nahi.
2. `list.length` ya `list.length()` → ❌ `list.size()` hai.
3. `ArrayList<int>` → ❌ wrapper chahiye: `ArrayList<Integer>`.
4. Loop ke andar list se remove karna (for-each me) → 💥 `ConcurrentModificationException`! Iterator ya `removeIf()` use karo.
5. HashMap me `put` same key pe = REPLACE hota hai, add nahi — bhool jaate hain log.
6. HashSet/HashMap me order expect karna → order ki guarantee NAHI.
7. `map.get(key)` null-check kiye bina use karna → `NullPointerException` (note 09/13!).

---

## 7. Practice: predict the output (answers hidden)

```java
// Q1
ArrayList<Integer> list = new ArrayList<>();
list.add(10); list.add(20); list.add(30);
list.remove(1);
System.out.println(list);

// Q2
HashSet<String> set = new HashSet<>();
set.add("a"); set.add("b"); set.add("a"); set.add("c"); set.add("b");
System.out.println(set.size());

// Q3
HashMap<String, Integer> map = new HashMap<>();
map.put("x", 1);
map.put("y", 2);
map.put("x", 5);
System.out.println(map.get("x") + map.get("y"));

// Q4
String s = "aab";
HashMap<Character, Integer> f = new HashMap<>();
for (char c : s.toCharArray()) f.put(c, f.getOrDefault(c, 0) + 1);
System.out.println(f.get('a'));
```

<details>
<summary>👉 Click for answers</summary>

- **Q1:** `[10, 30]` — `remove(1)` INDEX 1 hataata hai (20), value 1 nahi!
- **Q2:** `3` — duplicates reject: sirf a, b, c
- **Q3:** `7` — "x" ki value replace hui (1 → 5), 5 + 2 = 7
- **Q4:** `2` — 'a' do baar aaya, frequency counting pattern!

</details>

---

## 8. Quick Revision (30 seconds) ⚡

- Array = fixed size; Collections = auto-resize + ready-made methods.
- `ArrayList` = stretchable array: `add/get/size/remove/contains`; duplicates+order ✅.
- `HashSet` = sirf unique; super-fast `contains`; order ❌.
- `HashMap` = key→value; key unique, same key pe put = replace; `getOrDefault` = frequency counting ka hero.
- Primitives nahi — wrappers: `Integer`, `Double`, `Character`.
- `List`/`Set`/`Map` interfaces; `ArrayList`/`HashSet`/`HashMap` implementations.

---

⬅️ **Previous:** [13 — Exception Handling](13-exception-handling.md) | ➡️ **Next:** 15 — Multithreading Basics (coming soon)
