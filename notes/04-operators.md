# 04 — Operators: The Symbols That Do Work

> Operators = symbols that perform actions on values. `+` adds, `>` compares, `&&` combines conditions. Simple.

---

## 1. Arithmetic Operators (maths wale)

| Operator | Meaning | Example | Result |
|----------|---------|---------|--------|
| `+` | add | `10 + 3` | `13` |
| `-` | subtract | `10 - 3` | `7` |
| `*` | multiply | `10 * 3` | `30` |
| `/` | divide | `10 / 3` | `3` ⚠️ |
| `%` | remainder (modulus) | `10 % 3` | `1` |

### ⚠️ The #1 trap in Java: Integer division
```java
System.out.println(10 / 3);     // 3     (int / int = int, decimal CUT)
System.out.println(10.0 / 3);   // 3.3333... (one double makes result double)
```
**Rule:** `int / int` always gives `int`. Want decimals? Make one number a double.

### 💡 Why `%` (modulus) is super important
- Even/odd check: `n % 2 == 0` → even
- Last digit of a number: `n % 10`
- Remove last digit: `n / 10`

These two tricks (`% 10` and `/ 10`) are used in MANY coding questions (reverse number, palindrome, sum of digits...).

---

## 2. Increment & Decrement: `++` and `--`

```java
int a = 5;
a++;    // a is now 6 (a = a + 1)
a--;    // a is now 5 again
```

### Pre vs Post (favourite exam question!)

| Form | Meaning |
|------|---------|
| `++a` (pre) | FIRST increase, THEN use |
| `a++` (post) | FIRST use, THEN increase |

```java
int a = 5;
System.out.println(a++);   // prints 5 (use first, then a becomes 6)
System.out.println(a);     // prints 6

int b = 5;
System.out.println(++b);   // prints 6 (increase first, then use)
```

💡 **Memory trick:** Jo pehle likha hai wo pehle hota hai. `++a` → `++` pehle → increase pehle. `a++` → `a` pehle → use pehle.

---

## 3. Assignment Operators (shortcuts)

| Shortcut | Same as |
|----------|---------|
| `a += 5` | `a = a + 5` |
| `a -= 5` | `a = a - 5` |
| `a *= 5` | `a = a * 5` |
| `a /= 5` | `a = a / 5` |
| `a %= 5` | `a = a % 5` |

---

## 4. Comparison (Relational) Operators — answer is always true/false

| Operator | Meaning | Example | Result |
|----------|---------|---------|--------|
| `==` | equal to | `5 == 5` | `true` |
| `!=` | not equal | `5 != 3` | `true` |
| `>` | greater | `5 > 3` | `true` |
| `<` | smaller | `5 < 3` | `false` |
| `>=` | greater or equal | `5 >= 5` | `true` |
| `<=` | smaller or equal | `3 <= 5` | `true` |

### ⚠️ Trap: `=` vs `==`
- `=` → assignment (put value in box)
- `==` → comparison (are they equal?)

```java
int a = 5;        // put 5 in a
if (a == 5) ...   // check: is a equal to 5?
```

---

## 5. Logical Operators — combining conditions

| Operator | Name | Rule (simple) |
|----------|------|----------------|
| `&&` | AND | true only if **BOTH** are true |
| `\|\|` | OR | true if **ANY ONE** is true |
| `!` | NOT | flips: true → false, false → true |

### 🏭 Analogy:
- `&&` = strict parents: marks bhi acche AND behaviour bhi accha, tabhi phone milega 📱
- `||` = chill parents: koi ek bhi accha ho toh phone mil jayega

```java
int age = 20;
boolean hasId = true;

System.out.println(age >= 18 && hasId);   // true  (both true)
System.out.println(age < 18 || hasId);    // true  (one is true)
System.out.println(!hasId);               // false (flip of true)
```

💡 **Short-circuit:** In `a && b`, if `a` is false, Java doesn't even check `b` (answer is already false). Same for `||` when first is true. This makes code fast and is also an interview question!

---

## 6. Ternary Operator — mini if-else in one line

```java
condition ? valueIfTrue : valueIfFalse
```

```java
int marks = 75;
String result = (marks >= 40) ? "Pass" : "Fail";
System.out.println(result);   // Pass
```

Read it as: "marks >= 40? Yes → Pass, No → Fail".

---

## 7. Practice: predict the output (answers at bottom)

```java
int a = 7, b = 2;
System.out.println(a / b);        // Q1
System.out.println(a % b);        // Q2
System.out.println(a++ + ++a);    // Q3 (tricky!)
System.out.println(a > 5 && b > 5); // Q4
System.out.println((a > b) ? "big" : "small"); // Q5
```

<details>
<summary>👉 Click for answers</summary>

- **Q1:** `3` (int division, decimal cut)
- **Q2:** `1` (7 = 2×3 + 1)
- **Q3:** `16` → `a++` uses 7 (a becomes 8), `++a` makes a 9 and uses 9 → 7 + 9 = 16
- **Q4:** `false` (b > 5 is false, AND needs both true)
- **Q5:** `big` (a is 9 now, 9 > 2)

</details>

---

## 8. Quick Revision (30 seconds) ⚡

- `int / int = int` (decimal cut). `%` gives remainder.
- `n % 10` = last digit, `n / 10` = remove last digit — golden tricks.
- `a++` use-then-increase; `++a` increase-then-use.
- `=` assign, `==` compare.
- `&&` both true; `||` any one true; `!` flip. Short-circuit exists.
- Ternary: `condition ? yes : no`.

---

⬅️ **Previous:** [03 — Variables & Data Types](03-variables-datatypes.md) | ➡️ **Next:** 05 — Control Flow (coming soon)
