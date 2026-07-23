# 🎁 Easy — Collections, Methods & OOP Basics (M1–M10)

> Notes 08–14 ke concepts ka practice — methods, ArrayList, HashMap, HashSet, recursion.

---

## M1. ArrayList Operations Combo
**Problem:** List banao, 5 add karo, ek remove, ek update, print.
<details><summary>✅ Solution</summary>

```java
ArrayList<String> list = new ArrayList<>();
list.add("A"); list.add("B"); list.add("C"); list.add("D"); list.add("E");
list.remove("B");
list.set(0, "Z");
System.out.println(list + " size=" + list.size());   // [Z, C, D, E] size=4
```
</details>

---

## M2. ArrayList me Max
<details><summary>✅ Solution</summary>

```java
int max = list.get(0);
for (int x : list) if (x > max) max = x;
// Shortcut: Collections.max(list)
```
</details>

---

## M3. Student Marks (HashMap)
**Problem:** Naam → marks store karo, sabse zyada marks wala dhundo.
<details><summary>✅ Solution</summary>

```java
HashMap<String, Integer> marks = new HashMap<>();
marks.put("Ashu", 85); marks.put("Rahul", 92); marks.put("Priya", 78);
String topper = null; int best = -1;
for (var e : marks.entrySet())
    if (e.getValue() > best) { best = e.getValue(); topper = e.getKey(); }
System.out.println(topper + " → " + best);   // Rahul → 92
```
</details>

---

## M4. Union & Intersection (HashSet)
**Problem:** `{1,2,3}` aur `{2,3,4}` → union `{1,2,3,4}`, intersection `{2,3}`
<details><summary>✅ Solution</summary>

```java
HashSet<Integer> union = new HashSet<>(setA);
union.addAll(setB);
HashSet<Integer> inter = new HashSet<>(setA);
inter.retainAll(setB);
```
**Idea:** `addAll` = union, `retainAll` = sirf common bachao.
</details>

---

## M5. Method — isPrime() Reusable
**Problem:** Prime check ko method banao, 1–20 ke primes print karo.
<details><summary>✅ Solution</summary>

```java
static boolean isPrime(int n) {
    if (n <= 1) return false;
    for (int i = 2; i * i <= n; i++)
        if (n % i == 0) return false;
    return true;
}
// main me:
for (int i = 1; i <= 20; i++)
    if (isPrime(i)) System.out.print(i + " ");
```
**Idea:** Ek baar likho, har jagah use karo — methods ka asli fayda (note 08)!
</details>

---

## M6. Method Overloading — area()
<details><summary>✅ Solution</summary>

```java
static double area(double radius) { return 3.14159 * radius * radius; }
static int area(int l, int b) { return l * b; }
static double area(double base, double height, boolean tri) { return 0.5 * base * height; }
```
**Idea:** Same naam, alag parameters — compiler khud sahi wala chunta hai.
</details>

---

## M7. Recursion — Sum of Digits
**Problem:** N8 ko recursion se karo.
<details><summary>✅ Solution</summary>

```java
static int sumDigits(int n) {
    if (n == 0) return 0;              // base case — zaroori!
    return n % 10 + sumDigits(n / 10);
}
```
**Dry run:** sumDigits(407) = 7 + sumDigits(40) = 7 + 0 + sumDigits(4) = 7+0+4 = 11 ✅
</details>

---

## M8. Recursion — Fibonacci nth Term
<details><summary>✅ Solution</summary>

```java
static int fib(int n) {
    if (n <= 1) return n;
    return fib(n - 1) + fib(n - 2);
}
```
**Note:** Simple par SLOW (same kaam baar-baar) — loop version (N14) fast hai. Kyun slow hai, ye Medium me dekhenge!
</details>

---

## M9. Simple BankAccount Class
**Problem:** deposit/withdraw wala class — balance kabhi negative na ho.
<details><summary>✅ Solution</summary>

```java
class BankAccount {
    private double balance;               // encapsulation (note 12)!
    void deposit(double amt) {
        if (amt > 0) balance += amt;
    }
    void withdraw(double amt) {
        if (amt > 0 && amt <= balance) balance -= amt;
        else System.out.println("Invalid ya insufficient balance!");
    }
    double getBalance() { return balance; }
}
```
**Idea:** `private` + validation = data safe. Direct `balance = -500` koi nahi kar sakta.
</details>

---

## M10. Remove Duplicates from ArrayList (order intact)
**Problem:** `[1, 2, 2, 3, 1] → [1, 2, 3]`
<details><summary>✅ Solution</summary>

```java
ArrayList<Integer> unique = new ArrayList<>(new LinkedHashSet<>(list));
```
**Idea:** LinkedHashSet duplicates khaata hai, order yaad rakhta hai — wapas ArrayList me daal do. One-liner magic!
</details>

---

## 🎯 Easy level COMPLETE — 140 questions!

30 (Starter Pack) + 110 (categories) = **140 solved questions**. Ab 🟡 Medium ka time!

⬅️ [Strings](strings.md) | 🏠 [Roadmap](../../README.md)
