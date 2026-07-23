# 🌟 Easy — Patterns & Loops (P1–P20)

> Patterns ka GOLDEN RULE (note 05): **outer loop = rows, inner loop = columns**. Pyramid types me pehle spaces, fir stars. Har pattern ke liye row `i` me kitne spaces/stars — bas yahi formula nikalna hai!

---

## P1. Solid Square
```
* * * *
* * * *
* * * *
* * * *
```
<details><summary>✅ Solution</summary>

```java
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n; j++) System.out.print("* ");
    System.out.println();
}
```
</details>

---

## P2. Right Triangle
```
*
* *
* * *
* * * *
```
<details><summary>✅ Solution</summary>

```java
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= i; j++) System.out.print("* ");
    System.out.println();
}
```
**Formula:** row i me i stars.
</details>

---

## P3. Inverted Right Triangle
```
* * * *
* * *
* *
*
```
<details><summary>✅ Solution</summary>

```java
for (int i = n; i >= 1; i--) {
    for (int j = 1; j <= i; j++) System.out.print("* ");
    System.out.println();
}
```
</details>

---

## P4. Right-Aligned Triangle
```
      *
    * *
  * * *
* * * *
```
<details><summary>✅ Solution</summary>

```java
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n - i; j++) System.out.print("  ");
    for (int j = 1; j <= i; j++) System.out.print("* ");
    System.out.println();
}
```
**Formula:** row i = (n-i) spaces + i stars.
</details>

---

## P5. Pyramid
```
   *
  * *
 * * *
* * * *
```
<details><summary>✅ Solution</summary>

```java
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n - i; j++) System.out.print(" ");
    for (int j = 1; j <= i; j++) System.out.print("* ");
    System.out.println();
}
```
</details>

---

## P6. Inverted Pyramid
```
* * * *
 * * *
  * *
   *
```
<details><summary>✅ Solution</summary>

```java
for (int i = n; i >= 1; i--) {
    for (int j = 1; j <= n - i; j++) System.out.print(" ");
    for (int j = 1; j <= i; j++) System.out.print("* ");
    System.out.println();
}
```
</details>

---

## P7. Diamond ⭐
```
   *
  * *
 * * *
  * *
   *
```
<details><summary>✅ Solution</summary>

```java
// Upar wala pyramid (P5) + neeche inverted (P6, n-1 rows se)
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n - i; j++) System.out.print(" ");
    for (int j = 1; j <= i; j++) System.out.print("* ");
    System.out.println();
}
for (int i = n - 1; i >= 1; i--) {
    for (int j = 1; j <= n - i; j++) System.out.print(" ");
    for (int j = 1; j <= i; j++) System.out.print("* ");
    System.out.println();
}
```
**Idea:** Diamond = pyramid + inverted pyramid. Do patterns jodna aa gaya = boss level!
</details>

---

## P8. Hollow Square
```
* * * *
*     *
*     *
* * * *
```
<details><summary>✅ Solution</summary>

```java
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n; j++) {
        if (i == 1 || i == n || j == 1 || j == n) System.out.print("* ");
        else System.out.print("  ");
    }
    System.out.println();
}
```
**Idea:** Border pe star (pehli/aakhri row ya column), andar space.
</details>

---

## P9. Number Triangle (repeat)
```
1
2 2
3 3 3
```
<details><summary>✅ Solution</summary>

```java
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= i; j++) System.out.print(i + " ");
    System.out.println();
}
```
</details>

---

## P10. Number Triangle (counting)
```
1
1 2
1 2 3
```
<details><summary>✅ Solution</summary>

```java
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= i; j++) System.out.print(j + " ");
    System.out.println();
}
```
**Fark P9 se:** `i` print karo vs `j` print karo — bas!
</details>

---

## P11. Floyd's Triangle ⭐
```
1
2 3
4 5 6
7 8 9 10
```
<details><summary>✅ Solution</summary>

```java
int num = 1;
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= i; j++) System.out.print(num++ + " ");
    System.out.println();
}
```
**Idea:** Counter loops ke BAHAR rakho — kabhi reset nahi hota.
</details>

---

## P12. 0-1 Triangle
```
1
0 1
1 0 1
0 1 0 1
```
<details><summary>✅ Solution</summary>

```java
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= i; j++)
        System.out.print((i + j) % 2 == 0 ? "1 " : "0 ");
    System.out.println();
}
```
**Idea:** `(i+j)` even → 1, odd → 0. Chessboard logic!
</details>

---

## P13. Character Triangle
```
A
A B
A B C
```
<details><summary>✅ Solution</summary>

```java
for (int i = 1; i <= n; i++) {
    for (int j = 0; j < i; j++)
        System.out.print((char) ('A' + j) + " ");
    System.out.println();
}
```
**Idea:** `'A' + j` int ban jaata hai — `(char)` cast se wapas letter (N30 wala funda).
</details>

---

## P14. Hollow Triangle
```
*
* *
*   *
* * * *
```
<details><summary>✅ Solution</summary>

```java
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= i; j++) {
        if (j == 1 || j == i || i == n) System.out.print("* ");
        else System.out.print("  ");
    }
    System.out.println();
}
```
</details>

---

## P15. Series: 1 + 1/2 + 1/3 + ... + 1/n
<details><summary>✅ Solution</summary>

```java
double sum = 0;
for (int i = 1; i <= n; i++) sum += 1.0 / i;
```
**Trap:** `1/i` likha toh int division — sab 0! `1.0/i` likho.
</details>

---

## P16. Series: 1 + 11 + 111 + 1111...
<details><summary>✅ Solution</summary>

```java
long term = 1, sum = 0;
for (int i = 1; i <= n; i++) {
    sum += term;
    term = term * 10 + 1;   // 1 → 11 → 111
}
```
**Idea:** Agla term = purana ×10 + 1 (N9 reverse jaisa trick!).
</details>

---

## P17. Series: 1² + 2² + 3² + ... + n²
<details><summary>✅ Solution</summary>

```java
int sum = 0;
for (int i = 1; i <= n; i++) sum += i * i;
// Formula version: n*(n+1)*(2*n+1)/6
```
</details>

---

## P18. Reverse Counting with Step
**Problem:** 50 se 0 tak, 5-5 ke gap me: `50 45 40 ... 0`
<details><summary>✅ Solution</summary>

```java
for (int i = 50; i >= 0; i -= 5) System.out.print(i + " ");
```
**Idea:** Update section me kuch bhi likh sakte ho — `i -= 5` bhi!
</details>

---

## P19. Sum of Odd & Even (1 to n) alag-alag
<details><summary>✅ Solution</summary>

```java
int evenSum = 0, oddSum = 0;
for (int i = 1; i <= n; i++) {
    if (i % 2 == 0) evenSum += i;
    else oddSum += i;
}
```
</details>

---

## P20. Pascal's Triangle (starter) ⭐
```
1
1 1
1 2 1
1 3 3 1
```
<details><summary>✅ Solution</summary>

```java
for (int i = 0; i < n; i++) {
    int val = 1;
    for (int j = 0; j <= i; j++) {
        System.out.print(val + " ");
        val = val * (i - j) / (j + 1);   // agla binomial coefficient
    }
    System.out.println();
}
```
**Idea:** Har value = pichli × (i-j) / (j+1). Formula yaad na rahe toh 2D array se bhi bana sakte ho: har cell = upar + upar-left.
</details>

---

➡️ **Next category:** [Arrays](arrays.md) | ⬅️ [Numbers](numbers.md) | 🏠 [Roadmap](../../README.md)
