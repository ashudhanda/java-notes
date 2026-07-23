# 🔢 Easy — Numbers & Maths (N1–N30)

> Har question: **Problem → Solution (hidden) → Idea**. Pehle KHUD try karo, fir solution kholo! Detailed dry-runs ke liye [Starter Pack](../01-easy.md) dekho.

---

## N1. Even ya Odd
**Problem:** Number even hai ya odd? `7 → Odd`
<details><summary>✅ Solution</summary>

```java
System.out.println(n % 2 == 0 ? "Even" : "Odd");
```
**Idea:** `% 2` ka remainder 0 = even.
</details>

---

## N2. Positive, Negative ya Zero
**Problem:** Number ka sign batao. `-5 → Negative`
<details><summary>✅ Solution</summary>

```java
if (n > 0) System.out.println("Positive");
else if (n < 0) System.out.println("Negative");
else System.out.println("Zero");
```
**Idea:** Teen possibilities = if / else if / else.
</details>

---

## N3. Largest of 3
**Problem:** Teen me sabse bada. `12, 45, 30 → 45`
<details><summary>✅ Solution</summary>

```java
int max = Math.max(a, Math.max(b, c));
// ya if-else chain — Starter Pack Q2 me detail
```
**Idea:** `Math.max` do ka max deta hai — nest kar do.
</details>

---

## N4. Min of 3
**Problem:** Teen me sabse chhota. `12, 45, 30 → 12`
<details><summary>✅ Solution</summary>

```java
int min = Math.min(a, Math.min(b, c));
```
</details>

---

## N5. Swap (with temp)
**Problem:** a aur b exchange karo. `a=5,b=10 → a=10,b=5`
<details><summary>✅ Solution</summary>

```java
int temp = a; a = b; b = temp;
```
**Idea:** Do glass ka paani exchange — teesra glass chahiye!
</details>

---

## N6. Swap (without temp)
**Problem:** Bina teesre variable ke swap.
<details><summary>✅ Solution</summary>

```java
a = a + b;  b = a - b;  a = a - b;
```
**Idea:** Total me se ek nikalo → doosra milta hai. (Dry run: Starter Pack Q3)
</details>

---

## N7. Multiplication Table
**Problem:** n ki table 1–10. `5 → 5 x 1 = 5 ...`
<details><summary>✅ Solution</summary>

```java
for (int i = 1; i <= 10; i++)
    System.out.println(n + " x " + i + " = " + (n * i));
```
</details>

---

## N8. Sum of Digits
**Problem:** Digits ka sum. `407 → 11`
<details><summary>✅ Solution</summary>

```java
int sum = 0;
while (n > 0) { sum += n % 10; n /= 10; }
```
**Idea:** `%10` last digit deta hai, `/10` use hataata hai.
</details>

---

## N9. Reverse a Number
**Problem:** `123 → 321`
<details><summary>✅ Solution</summary>

```java
int rev = 0;
while (n > 0) { rev = rev * 10 + n % 10; n /= 10; }
```
**Idea:** rev ko ×10 karke naya digit chipkao.
</details>

---

## N10. Palindrome Number
**Problem:** `121 → yes, 123 → no`
<details><summary>✅ Solution</summary>

```java
int original = n, rev = 0;
while (n > 0) { rev = rev * 10 + n % 10; n /= 10; }
System.out.println(original == rev);
```
**Idea:** Reverse == original? Original pehle bacha lo!
</details>

---

## N11. Factorial
**Problem:** `5 → 120`
<details><summary>✅ Solution</summary>

```java
long fact = 1;
for (int i = 1; i <= n; i++) fact *= i;
```
**Idea:** `long` lo — 13! hi int se bahar nikal jaata hai!
</details>

---

## N12. Prime Check
**Problem:** `29 → Prime`
<details><summary>✅ Solution</summary>

```java
boolean isPrime = n > 1;
for (int i = 2; i * i <= n; i++)
    if (n % i == 0) { isPrime = false; break; }
```
**Idea:** √n tak hi check karna kaafi hai — factors pairs me aate hain.
</details>

---

## N13. Primes in a Range
**Problem:** 1 se 50 tak sab primes.
<details><summary>✅ Solution</summary>

```java
for (int n = 2; n <= 50; n++) {
    boolean p = true;
    for (int i = 2; i * i <= n; i++)
        if (n % i == 0) { p = false; break; }
    if (p) System.out.print(n + " ");
}
```
**Idea:** N12 ko loop me lapet do.
</details>

---

## N14. Fibonacci Series
**Problem:** Pehle n terms. `7 → 0 1 1 2 3 5 8`
<details><summary>✅ Solution</summary>

```java
int a = 0, b = 1;
for (int i = 1; i <= n; i++) {
    System.out.print(a + " ");
    int next = a + b; a = b; b = next;
}
```
**Idea:** Do variables ka "aage khisko" dance. (Dry run: Starter Pack Q10)
</details>

---

## N15. Armstrong Number
**Problem:** `153 → 1³+5³+3³ = 153 ✅`
<details><summary>✅ Solution</summary>

```java
int original = n, sum = 0;
while (n > 0) { int d = n % 10; sum += d * d * d; n /= 10; }
System.out.println(original == sum);
```
</details>

---

## N16. Leap Year
**Problem:** `2024 ✅, 1900 ❌, 2000 ✅`
<details><summary>✅ Solution</summary>

```java
boolean leap = (y % 4 == 0) && (y % 100 != 0 || y % 400 == 0);
```
**Idea:** Century years sirf tab leap jab 400 se divide ho.
</details>

---

## N17. Count Digits
**Problem:** `45078 → 5`
<details><summary>✅ Solution</summary>

```java
int count = (n == 0) ? 1 : 0;
while (n > 0) { count++; n /= 10; }
```
</details>

---

## N18. GCD (HCF)
**Problem:** `12, 18 → 6`
<details><summary>✅ Solution</summary>

```java
while (b != 0) { int t = b; b = a % b; a = t; }
System.out.println(a);
```
**Idea:** Euclid: GCD(a,b) = GCD(b, a%b). (Dry run: Starter Pack Q19)
</details>

---

## N19. LCM
**Problem:** `4, 6 → 12`
<details><summary>✅ Solution</summary>

```java
int gcd = /* N18 se */;
int lcm = (a * b) / gcd;
```
**Idea:** a × b = GCD × LCM — golden formula!
</details>

---

## N20. Sum of N Naturals
**Problem:** `100 → 5050`
<details><summary>✅ Solution</summary>

```java
int sum = n * (n + 1) / 2;   // Gauss ka formula, no loop!
```
</details>

---

## N21. Power of 2 Check
**Problem:** `16 → yes, 20 → no`
<details><summary>✅ Solution</summary>

```java
boolean isPow2 = n > 0 && (n & (n - 1)) == 0;
// Loop version: jab tak even hai /2 karo, end me 1 bacha toh yes
```
**Idea:** Power of 2 me binary me sirf EK 1-bit hota hai; `n & (n-1)` use uda deta hai.
</details>

---

## N22. Perfect Number
**Problem:** Divisors (khud ko chhod ke) ka sum = number? `6 → 1+2+3 = 6 ✅`
<details><summary>✅ Solution</summary>

```java
int sum = 0;
for (int i = 1; i <= n / 2; i++)
    if (n % i == 0) sum += i;
System.out.println(sum == n);
```
</details>

---

## N23. Strong Number
**Problem:** Digits ke FACTORIALS ka sum = number? `145 → 1!+4!+5! = 145 ✅`
<details><summary>✅ Solution</summary>

```java
int original = n, sum = 0;
while (n > 0) {
    int d = n % 10, f = 1;
    for (int i = 1; i <= d; i++) f *= i;
    sum += f; n /= 10;
}
System.out.println(original == sum);
```
**Idea:** Sum of digits + factorial ka combo.
</details>

---

## N24. Automorphic Number
**Problem:** Square ke END me number khud aata hai? `25 → 625 ends with 25 ✅`
<details><summary>✅ Solution</summary>

```java
int sq = n * n, digits = String.valueOf(n).length();
int lastPart = sq % (int) Math.pow(10, digits);
System.out.println(lastPart == n);
```
**Idea:** `% 10^digits` square ke aakhri digits deta hai.
</details>

---

## N25. Neon Number
**Problem:** Square ke digits ka sum = number? `9 → 81 → 8+1 = 9 ✅`
<details><summary>✅ Solution</summary>

```java
int sq = n * n, sum = 0;
while (sq > 0) { sum += sq % 10; sq /= 10; }
System.out.println(sum == n);
```
</details>

---

## N26. Sum of Even Digits
**Problem:** `2468 → sirf even digits ka sum = 20`
<details><summary>✅ Solution</summary>

```java
int sum = 0;
while (n > 0) {
    int d = n % 10;
    if (d % 2 == 0) sum += d;
    n /= 10;
}
```
</details>

---

## N27. Product of Digits
**Problem:** `234 → 24`
<details><summary>✅ Solution</summary>

```java
int prod = 1;
while (n > 0) { prod *= n % 10; n /= 10; }
```
**Idea:** Sum wale pattern me `+` ko `*` karo aur 0 ki jagah 1 se shuru.
</details>

---

## N28. First + Last Digit
**Problem:** `4567 → 4 + 7 = 11`
<details><summary>✅ Solution</summary>

```java
int last = n % 10;
while (n >= 10) n /= 10;    // first digit tak ghatao
System.out.println(n + last);
```
</details>

---

## N29. Simple Interest
**Problem:** P=1000, R=5%, T=2 saal → SI=100
<details><summary>✅ Solution</summary>

```java
double si = (p * r * t) / 100.0;
```
**Idea:** `100.0` (double) likho — int division ka trap avoid!
</details>

---

## N30. Number ka ASCII/Char khel
**Problem:** 'A' ka ASCII? 66 ka character? `A → 65, 66 → B`
<details><summary>✅ Solution</summary>

```java
char c = 'A';
int ascii = c;              // char → int: 65
char ch = (char) 66;        // int → char: B
```
**Idea:** char andar se number hi hai (note 03!) — cast se dono taraf jao.
</details>

---

➡️ **Next category:** [Patterns & Loops](patterns.md) | 🏠 [Roadmap](../../README.md)
