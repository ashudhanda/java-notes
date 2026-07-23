# 🟢 Easy Coding Questions — Batch 2 (Q16–Q30)

> Format wahi: **Problem → Hint → Solution → Explanation → Dry Run**. Pehle khud try karo! 💪

---

## Q16. Armstrong Number

**Problem:** 3-digit number Armstrong hai? (Digits ke CUBES ka sum = number khud)
`153 → 1³ + 5³ + 3³ = 1 + 125 + 27 = 153 ✅`

<details><summary>💡 Hint</summary>

Sum of digits (Q5) jaisa hi — bas digit jodne ki jagah digit³ jodo.
</details>

<details><summary>✅ Solution + Explanation</summary>

```java
int n = 153, original = n, sum = 0;
while (n > 0) {
    int d = n % 10;
    sum += d * d * d;
    n /= 10;
}
System.out.println(original == sum ? "Armstrong" : "Not Armstrong");
```

**Dry run:**
| n | d | d³ | sum |
|-----|---|-----|-----|
| 153 | 3 | 27 | 27 |
| 15 | 5 | 125 | 152 |
| 1 | 1 | 1 | 153 |

`153 == 153` ✅ Armstrong!

**Note:** General version me power = digit count (`Math.pow(d, digits)`), e.g. 1634 (4 digits, power 4).
</details>

---

## Q17. Leap Year Check

**Problem:** Saal leap year hai ya nahi?
`2024 ✅, 1900 ❌ (surprise!), 2000 ✅`

<details><summary>💡 Hint</summary>

Rule: 4 se divide ho AUR (100 se na ho YA 400 se ho). Note 04 ke `&&`/`||` yahan asli test dete hain!
</details>

<details><summary>✅ Solution + Explanation</summary>

```java
int year = 1900;
boolean leap = (year % 4 == 0) && (year % 100 != 0 || year % 400 == 0);
System.out.println(leap ? "Leap year" : "Not leap year");
```

**Explanation:** Century years (100 se divide) special case hain — wo tabhi leap jab 400 se bhi divide ho.

**Dry run (1900):** `1900%4==0` ✅, par `1900%100!=0` ❌ aur `1900%400==0` ❌ → false → NOT leap. (2000: `2000%400==0` ✅ → leap!)
</details>

---

## Q18. Count Digits

**Problem:** Number me kitne digits hain?
`Input: 45078 → Output: 5`

<details><summary>💡 Hint</summary>

`/10` karte jao jab tak 0 na ho, counter++.
</details>

<details><summary>✅ Solution + Explanation</summary>

```java
int n = 45078, count = 0;
if (n == 0) count = 1;         // edge case: 0 me 1 digit hai!
while (n > 0) {
    count++;
    n /= 10;
}
System.out.println(count);     // 5
```

**Dry run:** 45078 → 4507 → 450 → 45 → 4 → 0. Count: 1,2,3,4,**5** ✅

**One-liner (cheat):** `String.valueOf(n).length()` 😄
</details>

---

## Q19. GCD (HCF) of Two Numbers

**Problem:** Do numbers ka GCD nikalo.
`Input: 12, 18 → Output: 6`

<details><summary>💡 Hint</summary>

Euclidean algorithm: jab tak b != 0, (a, b) = (b, a % b). Interview favourite ⭐
</details>

<details><summary>✅ Solution + Explanation</summary>

```java
int a = 12, b = 18;
while (b != 0) {
    int temp = b;
    b = a % b;
    a = temp;
}
System.out.println("GCD = " + a);   // 6
```

**Explanation:** Euclid ka 2300 saal purana magic: GCD(a,b) = GCD(b, a%b). Remainder 0 hua → jo bacha wahi GCD.

**Dry run:**
| a | b | a%b |
|----|----|-----|
| 12 | 18 | 12 |
| 18 | 12 | 6 |
| 12 | 6 | 0 |
| 6 | 0 | — loop khatam |

GCD = 6 ✅

**Bonus:** LCM = `(a * b) / gcd` — ye formula yaad rakho!
</details>

---

## Q20. Second Largest in Array ⭐

**Problem:** Array ka doosra sabse bada element (interview me BAHUT common!).
`Input: {10, 5, 20, 8} → Output: 10`

<details><summary>💡 Hint</summary>

Do variables: `first`, `second`. Naya element first se bada → first neeche khisak ke second ban jaata hai.
</details>

<details><summary>✅ Solution + Explanation</summary>

```java
int[] arr = {10, 5, 20, 8};
int first = Integer.MIN_VALUE, second = Integer.MIN_VALUE;
for (int x : arr) {
    if (x > first) {
        second = first;    // purana champion runner-up ban gaya
        first = x;         // naya champion
    } else if (x > second && x != first) {
        second = x;        // champion se chhota par runner-up se bada
    }
}
System.out.println(second);   // 10
```

**Dry run:**
| x | first | second |
|----|-------|--------|
| 10 | 10 | MIN |
| 5 | 10 | 5 |
| 20 | 20 | 10 |
| 8 | 20 | 10 |

✅ Ek hi pass me answer — sorting ki zaroorat nahi!
</details>

---

## Q21. Linear Search

**Problem:** Array me element dhundo, index batao (nahi mila toh -1).
`Input: {4, 9, 2, 7}, target=2 → Output: index 2`

<details><summary>✅ Solution + Explanation</summary>

```java
int[] arr = {4, 9, 2, 7};
int target = 2, index = -1;
for (int i = 0; i < arr.length; i++) {
    if (arr[i] == target) {
        index = i;
        break;
    }
}
System.out.println(index);   // 2
```

**Explanation:** Ek-ek karke check — mila toh index save + break. `-1` ka matlab "nahi mila" (universal convention).
</details>

---

## Q22. Reverse an Array (in-place)

**Problem:** Array ko ULTA karo bina naya array banaye.
`Input: {1, 2, 3, 4, 5} → Output: {5, 4, 3, 2, 1}`

<details><summary>💡 Hint</summary>

Note 06 ka two-pointer: left-right swap karte hue milne tak.
</details>

<details><summary>✅ Solution + Explanation</summary>

```java
int[] arr = {1, 2, 3, 4, 5};
int left = 0, right = arr.length - 1;
while (left < right) {
    int temp = arr[left];
    arr[left] = arr[right];
    arr[right] = temp;
    left++;
    right--;
}
// arr = {5, 4, 3, 2, 1}
```

**Dry run:** swap(0,4): {5,2,3,4,1} → swap(1,3): {5,4,3,2,1} → left=2, right=2 → ruk gaye ✅
</details>

---

## Q23. Count Words in a String

**Problem:** Sentence me kitne words?
`Input: "Java is really fun" → Output: 4`

<details><summary>✅ Solution + Explanation</summary>

```java
String s = "Java is really fun";
String[] words = s.trim().split("\\s+");
System.out.println(words.length);   // 4
```

**Explanation:** `trim()` aage-peechhe ke spaces hatata hai, `split("\\s+")` ek ya zyada spaces pe todta hai. `\\s+` regex hai = "one or more whitespace".
</details>

---

## Q24. Sum of N Natural Numbers (loop vs formula)

**Problem:** 1 se n tak ka sum.
`Input: 100 → Output: 5050`

<details><summary>✅ Solution + Explanation</summary>

```java
// Tarika 1: loop
int n = 100, sum = 0;
for (int i = 1; i <= n; i++) sum += i;

// Tarika 2: Gauss ka formula — O(1), no loop!
int fast = n * (n + 1) / 2;

System.out.println(sum + " " + fast);   // 5050 5050
```

**Story:** Chhote Gauss ne school me 1-100 ka sum seconds me nikala tha: pairs banao (1+100, 2+99...) = 50 pairs × 101 = 5050. Formula > loop — efficiency ka pehla lesson!
</details>

---

## Q25. Check Duplicate Elements in Array

**Problem:** Array me koi element repeat hua hai?
`Input: {3, 7, 1, 7} → Output: true`

<details><summary>💡 Hint</summary>

Note 14 ka HashSet — `add()` false return kare toh duplicate!
</details>

<details><summary>✅ Solution + Explanation</summary>

```java
int[] arr = {3, 7, 1, 7};
HashSet<Integer> seen = new HashSet<>();
boolean hasDuplicate = false;
for (int x : arr) {
    if (!seen.add(x)) {      // add false = pehle se tha!
        hasDuplicate = true;
        break;
    }
}
System.out.println(hasDuplicate);   // true
```

**Explanation:** HashSet duplicate reject karta hai aur `add()` false deta hai — wahi hamara signal. Nested loops (O(n²)) se kahin fast!
</details>

---

## Q26. Character Frequency in String ⭐

**Problem:** Har character kitni baar aaya?
`Input: "apple" → a=1, p=2, l=1, e=1`

<details><summary>💡 Hint</summary>

Note 14 ka frequency pattern: `getOrDefault(c, 0) + 1`.
</details>

<details><summary>✅ Solution + Explanation</summary>

```java
String s = "apple";
HashMap<Character, Integer> freq = new HashMap<>();
for (char c : s.toCharArray()) {
    freq.put(c, freq.getOrDefault(c, 0) + 1);
}
System.out.println(freq);   // {p=2, a=1, e=1, l=1}
```

**Explanation:** THE pattern — note 14 me promise kiya tha, ab live! Har char: purani count lo (nahi hai toh 0), +1 karke wapas rakho. Medium/Hard questions ka base hai ye.
</details>

---

## Q27. Palindrome String

**Problem:** String palindrome hai? ("madam" ✅, "hello" ❌)

<details><summary>💡 Hint</summary>

Two-pointer (Q22 jaisa) — par swap nahi, COMPARE karo.
</details>

<details><summary>✅ Solution + Explanation</summary>

```java
String s = "madam";
boolean isPalin = true;
int left = 0, right = s.length() - 1;
while (left < right) {
    if (s.charAt(left) != s.charAt(right)) {
        isPalin = false;
        break;
    }
    left++;
    right--;
}
System.out.println(isPalin ? "Palindrome" : "Not palindrome");
```

**Dry run (madam):** m==m ✅ → a==a ✅ → left=2,right=2 ruk gaye → Palindrome ✅
</details>

---

## Q28. Even & Odd Count in Array

**Problem:** Array me kitne even, kitne odd?
`Input: {2, 5, 8, 1, 9} → Even=2, Odd=3`

<details><summary>✅ Solution + Explanation</summary>

```java
int[] arr = {2, 5, 8, 1, 9};
int even = 0, odd = 0;
for (int x : arr) {
    if (x % 2 == 0) even++;
    else odd++;
}
System.out.println("Even=" + even + ", Odd=" + odd);
```

Q1 + array loop ka combo — building blocks jodne ka perfect example!
</details>

---

## Q29. Celsius ↔ Fahrenheit

**Problem:** Temperature convert karo.
`Input: 37°C → Output: 98.6°F`

<details><summary>✅ Solution + Explanation</summary>

```java
double c = 37;
double f = (c * 9 / 5) + 32;
System.out.println(f);   // 98.6
```

**Trap:** `c` ko `int` rakha aur `(c * 9 / 5)` kiya toh bhi theek (37×9=333, /5=66.6... par int me 66!) — isliye `double` lo YA pehle multiply karo. `9/5` pehle likha toh `1` ban jaata (integer division) — formula hi galat! ⚠️
</details>

---

## Q30. Simple Calculator (switch)

**Problem:** Do numbers + operator (+, -, *, /) → result.
`Input: 12, 4, '/' → Output: 3.0`

<details><summary>✅ Solution + Explanation</summary>

```java
double a = 12, b = 4;
char op = '/';
double result;
switch (op) {
    case '+': result = a + b; break;
    case '-': result = a - b; break;
    case '*': result = a * b; break;
    case '/':
        if (b == 0) { System.out.println("Zero se divide nahi!"); return; }
        result = a / b; break;
    default:  System.out.println("Galat operator!"); return;
}
System.out.println(result);   // 3.0
```

**Explanation:** Note 05 ka switch + note 13 wali soch (divide by zero guard). `break` mat bhoolna — warna fall-through sab cases chala dega!
</details>

---

## 🎯 30 Easy questions DONE!

Ab tumhare paas notes 01–15 + 30 solved questions hain. Aage:
- 🟡 **Medium** — two-pointer problems, sorting logic, matrix, HashMap ke asli khel
- 🔴 **Hard** — recursion challenges, string algorithms
- ⭐ **Important** — interview ke sabse repeated questions
- 🧠 **Logic Building** — dimaag ghumane wale

⬅️ [Batch 1 (Q1–Q15)](01-easy.md) | 🏠 [Back to Roadmap](../README.md)
