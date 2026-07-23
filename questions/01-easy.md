# 🟢 Easy Coding Questions — Batch 1 (Q1–Q15)

> Har question ka format: **Problem → Hint → Solution → Explanation → Dry Run**. Pehle KHUD try karo (hint dekh ke), solution LAST me kholo. Copy-paste mat karo — type karke chalao! 💪

> Ye questions internet ke sabse popular sources (GeeksforGeeks, w3resource, HackerRank, JavaConceptOfTheDay, PrepInsta) se hand-picked hain — wahi jo exams aur interviews me BAAR-BAAR aate hain.

---

## Q1. Even ya Odd?

**Problem:** Ek number lo, batao even hai ya odd.
`Input: 7 → Output: Odd`

<details><summary>💡 Hint</summary>

Note 04 ka `%` operator — 2 se divide karke remainder dekho.
</details>

<details><summary>✅ Solution + Explanation</summary>

```java
int n = 7;
if (n % 2 == 0) System.out.println("Even");
else System.out.println("Odd");
```

**Explanation:** `n % 2` = 2 se divide karne ke baad bacha hua remainder. Even numbers me remainder 0, odd me 1.

**Dry run:** `7 % 2` → 7 = 2×3 + **1** → remainder 1 ≠ 0 → "Odd" ✅
</details>

---

## Q2. Teen numbers me sabse bada

**Problem:** 3 numbers me largest dhundo.
`Input: 12, 45, 30 → Output: 45`

<details><summary>💡 Hint</summary>

if-else if chain (note 05), ya nested ternary. Compare a vs b vs c.
</details>

<details><summary>✅ Solution + Explanation</summary>

```java
int a = 12, b = 45, c = 30;
int max;
if (a >= b && a >= c) max = a;
else if (b >= c) max = b;
else max = c;
System.out.println(max);   // 45
```

**Explanation:** Pehla check: kya `a` dono se bada/equal hai? Nahi → ab ladai sirf b vs c me hai (a already out). `b >= c`? Haan → b winner.

**Dry run:** a=12: `12>=45`? ❌ → `b>=c`: `45>=30`? ✅ → max=45 ✅
</details>

---

## Q3. Swap without third variable

**Problem:** Do variables ki values exchange karo — teesra variable use kiye BINA.
`Input: a=5, b=10 → Output: a=10, b=5`

<details><summary>💡 Hint</summary>

Sum me dono chhupe hain: a+b. Ek ko nikalo, doosra bach jaata hai.
</details>

<details><summary>✅ Solution + Explanation</summary>

```java
int a = 5, b = 10;
a = a + b;    // a = 15 (dono ka total)
b = a - b;    // b = 15 - 10 = 5 (purana a!)
a = a - b;    // a = 15 - 5 = 10 (purana b!)
System.out.println(a + " " + b);   // 10 5
```

**Explanation:** Total me se ek value minus karo toh doosri milti hai. Pehle total banao, fir usme se ek-ek karke nikalo.

**Dry run:** a=5,b=10 → a=15 → b=15-10=**5** → a=15-5=**10** ✅ Swap done!
</details>

---

## Q4. Multiplication Table

**Problem:** Kisi number ki table print karo (1 se 10 tak).
`Input: 5 → Output: 5 x 1 = 5 ... 5 x 10 = 50`

<details><summary>💡 Hint</summary>

Ek for loop 1 se 10, har round me `n * i`.
</details>

<details><summary>✅ Solution + Explanation</summary>

```java
int n = 5;
for (int i = 1; i <= 10; i++) {
    System.out.println(n + " x " + i + " = " + (n * i));
}
```

**Explanation:** Loop counter `i` hi table ka multiplier hai. `(n * i)` brackets zaroori — warna `+` string jod deta (note 07 ka trap!).
</details>

---

## Q5. Sum of Digits

**Problem:** Number ke digits ka sum nikalo.
`Input: 407 → Output: 11 (4+0+7)`

<details><summary>💡 Hint</summary>

Note 04 ke golden tricks: `% 10` = last digit, `/ 10` = last digit hatao. While loop jab tak n > 0.
</details>

<details><summary>✅ Solution + Explanation</summary>

```java
int n = 407, sum = 0;
while (n > 0) {
    sum += n % 10;    // last digit jodo
    n /= 10;          // last digit hatao
}
System.out.println(sum);   // 11
```

**Dry run:**
| Round | n | n%10 | sum | n/10 |
|-------|-----|------|-----|------|
| 1 | 407 | 7 | 7 | 40 |
| 2 | 40 | 0 | 7 | 4 |
| 3 | 4 | 4 | 11 | 0 |

n=0 → loop khatam → sum=11 ✅
</details>

---

## Q6. Reverse a Number

**Problem:** Number ulta karo.
`Input: 123 → Output: 321`

<details><summary>💡 Hint</summary>

Wahi `%10` / `/10` combo — par ab digits ko JODNA hai: `rev = rev*10 + digit`.
</details>

<details><summary>✅ Solution + Explanation</summary>

```java
int n = 123, rev = 0;
while (n > 0) {
    rev = rev * 10 + n % 10;   // purane rev ko left shift + naya digit
    n /= 10;
}
System.out.println(rev);   // 321
```

**Explanation:** `rev * 10` purane digits ko ek jagah left khiskata hai, `+ n % 10` naya digit right me lagata hai.

**Dry run:**
| Round | n | n%10 | rev = rev*10 + digit |
|-------|-----|------|-----------------------|
| 1 | 123 | 3 | 0*10+3 = 3 |
| 2 | 12 | 2 | 3*10+2 = 32 |
| 3 | 1 | 1 | 32*10+1 = 321 |

✅ Ye pattern AGLE 2 questions me bhi kaam aayega!
</details>

---

## Q7. Palindrome Number

**Problem:** Number aage-peechhe same hai? (121 ✅, 123 ❌)

<details><summary>💡 Hint</summary>

Q6 ka reverse nikalo, original se compare karo. (Original ko pehle SAVE kar lena — loop use kha jaata hai!)
</details>

<details><summary>✅ Solution + Explanation</summary>

```java
int n = 121, original = n, rev = 0;
while (n > 0) {
    rev = rev * 10 + n % 10;
    n /= 10;
}
System.out.println(original == rev ? "Palindrome" : "Not palindrome");
```

**Explanation:** Reverse == original → palindrome. `original` variable isliye — while loop `n` ko 0 bana deta hai!

**Dry run:** 121 → rev: 1 → 12 → 121. `121 == 121` ✅ Palindrome!
</details>

---

## Q8. Factorial

**Problem:** n! nikalo (n! = 1×2×3×...×n).
`Input: 5 → Output: 120`

<details><summary>💡 Hint</summary>

Loop 1 se n, ek variable me multiply karte jao. `fact` ko 1 se start karna (0 se kiya toh sab 0! 😄)
</details>

<details><summary>✅ Solution + Explanation</summary>

```java
int n = 5;
long fact = 1;                 // long — factorial JALDI bada ho jaata hai!
for (int i = 1; i <= n; i++) {
    fact *= i;
}
System.out.println(fact);      // 120
```

**Dry run:** fact: 1 → 1×1=1 → 1×2=2 → 2×3=6 → 6×4=24 → 24×5=**120** ✅

**Bonus:** Recursion wala version note 08 me dekha tha: `n * factorial(n-1)`.
</details>

---

## Q9. Prime Number Check

**Problem:** Number prime hai ya nahi? (Prime = sirf 1 aur khud se divide ho)
`Input: 29 → Output: Prime`

<details><summary>💡 Hint</summary>

2 se n/2 (ya √n) tak check karo — koi bhi divide kar de toh prime NAHI. Flag boolean rakho.
</details>

<details><summary>✅ Solution + Explanation</summary>

```java
int n = 29;
boolean isPrime = n > 1;            // 0 aur 1 prime nahi hote!
for (int i = 2; i <= n / 2; i++) {
    if (n % i == 0) {               // koi divide kar gaya?
        isPrime = false;
        break;                      // aage check karne ka faayda nahi (note 05 ka break!)
    }
}
System.out.println(isPrime ? "Prime" : "Not prime");
```

**Explanation:** Prime ka matlab — 2 se leke n/2 tak KOI number use divide nahi karta. Ek bhi mil gaya → flag false + break (time bachao).

**Dry run (n=29):** i=2..14 tak koi `29 % i == 0` nahi → isPrime true rahа → "Prime" ✅

**Speed tip:** `i * i <= n` (√n tak) aur bhi fast hai — Medium me use karenge!
</details>

---

## Q10. Fibonacci Series

**Problem:** Pehle n Fibonacci numbers print karo (har number = pichhle do ka sum).
`Input: 7 → Output: 0 1 1 2 3 5 8`

<details><summary>💡 Hint</summary>

Do variables `a=0, b=1`. Har round: print a, fir naya number = a+b, aur a-b ko aage khiskao.
</details>

<details><summary>✅ Solution + Explanation</summary>

```java
int n = 7, a = 0, b = 1;
for (int i = 1; i <= n; i++) {
    System.out.print(a + " ");
    int next = a + b;    // agla number
    a = b;               // a aage badha
    b = next;            // b aage badha
}
// Output: 0 1 1 2 3 5 8
```

**Dry run:**
| Round | print | next=a+b | naya a | naya b |
|-------|-------|----------|--------|--------|
| 1 | 0 | 1 | 1 | 1 |
| 2 | 1 | 2 | 1 | 2 |
| 3 | 1 | 3 | 2 | 3 |
| 4 | 2 | 5 | 3 | 5 |
| 5 | 3 | 8 | 5 | 8 |
| 6 | 5 | 13 | 8 | 13 |
| 7 | 8 | — | — | — |

✅ Do variables ka "aage khisko" dance — classic pattern!
</details>

---

## Q11. Array ka Sum aur Average

**Problem:** Array ke sab elements ka sum aur average nikalo.
`Input: {10, 20, 30, 40} → Output: Sum=100, Avg=25.0`

<details><summary>💡 Hint</summary>

For-each loop (note 06), sum jama karte jao. Average ke liye `(double)` cast mat bhoolna!
</details>

<details><summary>✅ Solution + Explanation</summary>

```java
int[] arr = {10, 20, 30, 40};
int sum = 0;
for (int x : arr) sum += x;
double avg = (double) sum / arr.length;
System.out.println("Sum=" + sum + ", Avg=" + avg);
```

**Explanation:** `(double) sum` cast zaroori — warna `100/4` int division hota (note 04 ka integer division trap!). Yahan toh 25 hi aata, par `{10,20,30}` pe `60/3=20` sahi lagta magar `{10,20,25}` pe `55/3=18` (18.33 nahi!) — silent bug.
</details>

---

## Q12. Array me Largest aur Smallest

**Problem:** Array ka max aur min ek saath dhundo.
`Input: {23, 67, 12, 89, 45} → Output: Max=89, Min=12`

<details><summary>💡 Hint</summary>

Note 06 ka max pattern — bas min ke liye ulta comparison bhi saath me.
</details>

<details><summary>✅ Solution + Explanation</summary>

```java
int[] arr = {23, 67, 12, 89, 45};
int max = arr[0], min = arr[0];
for (int i = 1; i < arr.length; i++) {
    if (arr[i] > max) max = arr[i];
    if (arr[i] < min) min = arr[i];
}
System.out.println("Max=" + max + ", Min=" + min);
```

**Dry run:**
| i | arr[i] | max | min |
|---|--------|-----|-----|
| 1 | 67 | 67 | 23 |
| 2 | 12 | 67 | 12 |
| 3 | 89 | 89 | 12 |
| 4 | 45 | 89 | 12 |

✅ Ek hi loop me dono — do alag loop lagane ki zaroorat nahi!
</details>

---

## Q13. Reverse a String

**Problem:** String ulti karo.
`Input: "hello" → Output: "olleh"`

<details><summary>💡 Hint</summary>

Last index (`length()-1`) se 0 tak loop, `charAt(i)` jodte jao. (Note 07!)
</details>

<details><summary>✅ Solution + Explanation</summary>

```java
String s = "hello";
StringBuilder rev = new StringBuilder();
for (int i = s.length() - 1; i >= 0; i--) {
    rev.append(s.charAt(i));
}
System.out.println(rev);   // olleh
```

**Explanation:** Peechhe se aage loop + har character jodo. `StringBuilder` use kiya kyunki loop me `+` slow hai (note 07 ka performance trap).

**One-liner (jab allowed ho):** `new StringBuilder(s).reverse().toString()`

**Dry run:** i=4 'o' → i=3 'l' → i=2 'l' → i=1 'e' → i=0 'h' → "olleh" ✅
</details>

---

## Q14. Count Vowels & Consonants

**Problem:** String me kitne vowels, kitne consonants?
`Input: "programming" → Output: Vowels=3, Consonants=8`

<details><summary>💡 Hint</summary>

Har character check: vowel list me hai? Letter hai bhi ya nahi (space/digit skip)?
</details>

<details><summary>✅ Solution + Explanation</summary>

```java
String s = "programming";
int vowels = 0, consonants = 0;
for (int i = 0; i < s.length(); i++) {
    char c = Character.toLowerCase(s.charAt(i));
    if (c >= 'a' && c <= 'z') {                    // sirf letters count karo
        if (c=='a' || c=='e' || c=='i' || c=='o' || c=='u') vowels++;
        else consonants++;
    }
}
System.out.println("Vowels=" + vowels + ", Consonants=" + consonants);
```

**Explanation:** `toLowerCase` se 'A' aur 'a' dono handle. `c >= 'a' && c <= 'z'` — chars ke andar numbers hote hain, isliye range check chalta hai! Letter hai → vowel ya consonant.

**Dry run (short):** p,r,g,r,m,m,n,g → consonants (8); o,a,i → vowels (3) ✅
</details>

---

## Q15. Star Pattern — Right Triangle + Pyramid

**Problem (a):** 
```
*
* *
* * *
* * * *
```

**Problem (b) — Pyramid:**
```
   *
  * *
 * * *
* * * *
```

<details><summary>💡 Hint</summary>

Note 05 ka rule: outer loop = rows, inner = columns. Pyramid ke liye pehle SPACES print karo, fir stars.
</details>

<details><summary>✅ Solution + Explanation</summary>

**(a) Right triangle:**
```java
int n = 4;
for (int i = 1; i <= n; i++) {          // row number
    for (int j = 1; j <= i; j++) {      // row i me i stars
        System.out.print("* ");
    }
    System.out.println();
}
```

**(b) Pyramid:**
```java
int n = 4;
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n - i; j++) System.out.print(" ");   // pehle spaces
    for (int j = 1; j <= i; j++) System.out.print("* ");      // fir stars
    System.out.println();
}
```

**Explanation:** Pyramid ka formula har row ke liye: **spaces = n - i, stars = i**. Row 1: 3 spaces + 1 star. Row 4: 0 spaces + 4 stars.

**Dry run (b), n=4:**
| Row i | Spaces (n-i) | Stars (i) |
|-------|--------------|-----------|
| 1 | 3 | 1 |
| 2 | 2 | 2 |
| 3 | 1 | 3 |
| 4 | 0 | 4 |

✅ Pattern questions ka 90% yahi formula hai — spaces aur stars ka hisaab!
</details>

---

## 🎯 Batch 1 complete! Aage kya?

- Ye 15 questions notes 01–08 ke concepts pakke karte hain.
- **Batch 2 (coming):** aur easy questions — Armstrong number, leap year, GCD/LCM, count digits, second largest, linear search...
- Fir 🟡 **Medium** — two-pointer, frequency counting (HashMap!), sorting logic, 2D matrix...

⬅️ [Back to Roadmap](../README.md)
