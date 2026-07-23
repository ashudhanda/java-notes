# 🟡 Medium Questions — Batch 1 (MD1–MD25)

> Easy level pakka hai? Ab asli maza. Yahan questions me **technique** seekhni hai — two-pointer, binary search, Kadane, frequency maps. Har technique aage 10 questions me kaam aayegi. Format: **Problem → Hint → Solution → Idea/Dry run**.

---

## MD1. Two Sum ⭐⭐
**Problem:** Array me do numbers dhundo jinka sum = target. Indices batao.
`{2, 7, 11, 15}, target=9 → [0, 1]`

<details><summary>💡 Hint</summary>

Har element ke liye poochho: mera PARTNER (target - x) pehle mil chuka hai? HashMap me store karte jao.
</details>

<details><summary>✅ Solution</summary>

```java
HashMap<Integer, Integer> seen = new HashMap<>();   // value -> index
for (int i = 0; i < arr.length; i++) {
    int need = target - arr[i];
    if (seen.containsKey(need)) {
        System.out.println(seen.get(need) + ", " + i);
        break;
    }
    seen.put(arr[i], i);
}
```
**Idea:** Nested loops O(n²) ki jagah ek pass O(n) — "partner pehle dekha hai?" wala sawal HashMap se instant.

**Dry run:** i=0: need=7, map empty → store {2:0}. i=1: need=2 → map me HAI! → [0,1] ✅
</details>

---

## MD2. Move Zeros to End
**Problem:** `{0, 1, 0, 3, 12} → {1, 3, 12, 0, 0}` (order intact, in-place)

<details><summary>💡 Hint</summary>

Ek pointer "agla non-zero kahan rakhna hai" track kare.
</details>

<details><summary>✅ Solution</summary>

```java
int pos = 0;
for (int i = 0; i < arr.length; i++)
    if (arr[i] != 0) arr[pos++] = arr[i];
while (pos < arr.length) arr[pos++] = 0;
```
**Idea:** Non-zeros ko aage sarkate jao, bachi jagah 0 se bhar do.
</details>

---

## MD3. Rotate Array by K ⭐
**Problem:** `{1,2,3,4,5}, k=2 → {4,5,1,2,3}`

<details><summary>💡 Hint</summary>

Reversal trick: pura reverse → pehle k reverse → baaki reverse.
</details>

<details><summary>✅ Solution</summary>

```java
static void reverse(int[] a, int l, int r) {
    while (l < r) { int t = a[l]; a[l++] = a[r]; a[r--] = t; }
}
k = k % arr.length;              // k > length ho sakta hai!
reverse(arr, 0, arr.length - 1); // {5,4,3,2,1}
reverse(arr, 0, k - 1);          // {4,5,3,2,1}
reverse(arr, k, arr.length - 1); // {4,5,1,2,3}
```
**Idea:** 3 reversals = rotation, bina extra array ke. A6 wala reverse ab METHOD ban ke 3 baar kaam aaya!
</details>

---

## MD4. Pair Sum in Sorted Array (two-pointer)
**Problem:** SORTED array me pair with sum = target. `{1,3,5,7,9}, 12 → (3,9)`

<details><summary>✅ Solution</summary>

```java
int l = 0, r = arr.length - 1;
while (l < r) {
    int sum = arr[l] + arr[r];
    if (sum == target) { System.out.println(arr[l] + "," + arr[r]); break; }
    else if (sum < target) l++;    // sum chhota → bada element chahiye
    else r--;                       // sum bada → chhota element chahiye
}
```
**Idea:** Sorted hai isliye pointer HILANE ka logic possible: sum kam → left aage, zyada → right peechhe.
</details>

---

## MD5. Binary Search ⭐⭐
**Problem:** Sorted array me target ka index — O(log n) me.
`{2, 5, 8, 12, 16, 23}, target=12 → 3`

<details><summary>💡 Hint</summary>

Beech ka dekho: target chhota → left half, bada → right half. Range aadhi karte jao.
</details>

<details><summary>✅ Solution</summary>

```java
int lo = 0, hi = arr.length - 1, ans = -1;
while (lo <= hi) {
    int mid = lo + (hi - lo) / 2;    // (lo+hi)/2 overflow kar sakta hai!
    if (arr[mid] == target) { ans = mid; break; }
    else if (arr[mid] < target) lo = mid + 1;
    else hi = mid - 1;
}
```
**Analogy:** Dictionary me word dhundna — beech kholo, aage/peechhe decide karo. 1000 elements = sirf ~10 steps!

**Dry run (target=12):** lo=0,hi=5,mid=2(8)<12 → lo=3. lo=3,hi=5,mid=4(16)>12 → hi=3. mid=3(12) ✅
</details>

---

## MD6. Kadane's Algorithm — Max Subarray Sum ⭐⭐
**Problem:** Continuous subarray ka max sum. `{-2,1,-3,4,-1,2,1,-5,4} → 6` (subarray {4,-1,2,1})

<details><summary>💡 Hint</summary>

Har element pe decide: purane sum me jodo, ya FRESH START yahan se?
</details>

<details><summary>✅ Solution</summary>

```java
int curr = arr[0], best = arr[0];
for (int i = 1; i < arr.length; i++) {
    curr = Math.max(arr[i], curr + arr[i]);   // jodo ya fresh start
    best = Math.max(best, curr);
}
```
**Analogy:** Business me ghaata itna ho gaya ki purana sab chhod ke NAYI dukaan kholna behtar hai? Wahi decision har din.

**Dry run:**
| x | curr = max(x, curr+x) | best |
|----|------------------------|------|
| 1 | max(1, -1) = 1 | 1 |
| -3 | max(-3, -2) = -2 | 1 |
| 4 | max(4, 2) = **4** (fresh!) | 4 |
| -1 | 3 | 4 |
| 2 | 5 | 5 |
| 1 | 6 | **6** |
| -5 | 1 | 6 |
| 4 | 5 | 6 |

✅ Interview LEGEND question hai ye.
</details>

---

## MD7. Majority Element (> n/2 baar)
**Problem:** `{2, 2, 1, 2, 3, 2, 2} → 2`

<details><summary>✅ Solution</summary>

```java
// Simple: HashMap frequency + check > n/2
// Smart (Moore's Voting):
int candidate = arr[0], votes = 1;
for (int i = 1; i < arr.length; i++) {
    if (votes == 0) { candidate = arr[i]; votes = 1; }
    else if (arr[i] == candidate) votes++;
    else votes--;
}
```
**Analogy:** Election — alag vote aapas me cancel ho jaate hain; majority wala hi khada bachta hai.
</details>

---

## MD8. Leaders in Array
**Problem:** Element leader hai agar uske RIGHT me koi bada nahi. `{16,17,4,3,5,2} → 17, 5, 2`

<details><summary>✅ Solution</summary>

```java
int maxRight = arr[arr.length - 1];
System.out.print(maxRight + " ");            // last hamesha leader
for (int i = arr.length - 2; i >= 0; i--) {
    if (arr[i] > maxRight) {
        maxRight = arr[i];
        System.out.print(arr[i] + " ");
    }
}
```
**Idea:** RIGHT se LEFT chalo, running max rakho — ek pass me done. (Left se chalte toh har element ke liye pura right scan karna padta!)
</details>

---

## MD9. Equilibrium Index
**Problem:** Index jahan left sum == right sum. `{1, 3, 5, 2, 2} → index 2` (1+3 = 2+2)

<details><summary>✅ Solution</summary>

```java
int total = 0, leftSum = 0;
for (int x : arr) total += x;
for (int i = 0; i < arr.length; i++) {
    total -= arr[i];              // total ab RIGHT sum hai
    if (leftSum == total) { System.out.println(i); break; }
    leftSum += arr[i];
}
```
**Idea:** Total me se current nikala = right sum. Left sum banate jao — match hua toh equilibrium!
</details>

---

## MD10. Merge Two Sorted Arrays ⭐
**Problem:** `{1,3,5} + {2,4,6} → {1,2,3,4,5,6}` (sorted hi rahe)

<details><summary>✅ Solution</summary>

```java
int[] res = new int[a.length + b.length];
int i = 0, j = 0, k = 0;
while (i < a.length && j < b.length)
    res[k++] = (a[i] <= b[j]) ? a[i++] : b[j++];
while (i < a.length) res[k++] = a[i++];
while (j < b.length) res[k++] = b[j++];
```
**Analogy:** Do sorted lines me se har baar chhota wala aage bulao. Merge Sort ka dil yahi hai!
</details>

---

## MD11. Matrix Transpose
**Problem:** Rows ↔ columns. `{{1,2},{3,4}} → {{1,3},{2,4}}`

<details><summary>✅ Solution</summary>

```java
int[][] t = new int[cols][rows];
for (int i = 0; i < rows; i++)
    for (int j = 0; j < cols; j++)
        t[j][i] = m[i][j];
```
**Idea:** `[i][j] → [j][i]` — bas indices ulta do.
</details>

---

## MD12. Rotate Matrix 90° Clockwise ⭐
**Problem:**
```
1 2 3      7 4 1
4 5 6  →   8 5 2
7 8 9      9 6 3
```

<details><summary>💡 Hint</summary>

Transpose + har row reverse = 90° rotation!
</details>

<details><summary>✅ Solution</summary>

```java
// Step 1: Transpose (MD11)
for (int i = 0; i < n; i++)
    for (int j = i + 1; j < n; j++) {
        int t = m[i][j]; m[i][j] = m[j][i]; m[j][i] = t;
    }
// Step 2: har row reverse (A6 ka two-pointer!)
for (int i = 0; i < n; i++) {
    int l = 0, r = n - 1;
    while (l < r) { int t = m[i][l]; m[i][l++] = m[i][r]; m[i][r--] = t; }
}
```
**Idea:** Do easy techniques (transpose + reverse) = ek medium answer. Building blocks!
</details>

---

## MD13. Matrix Multiplication
<details><summary>✅ Solution</summary>

```java
int[][] c = new int[r1][c2];
for (int i = 0; i < r1; i++)
    for (int j = 0; j < c2; j++)
        for (int k = 0; k < c1; k++)
            c[i][j] += a[i][k] * b[k][j];
```
**Yaad:** `c[i][j]` = a ki row i × b ka column j ka dot product. Condition: a ke columns == b ki rows.
</details>

---

## MD14. Selection Sort
<details><summary>✅ Solution</summary>

```java
for (int i = 0; i < arr.length - 1; i++) {
    int minIdx = i;
    for (int j = i + 1; j < arr.length; j++)
        if (arr[j] < arr[minIdx]) minIdx = j;
    int t = arr[i]; arr[i] = arr[minIdx]; arr[minIdx] = t;
}
```
**Analogy:** Line me sabse chhote ko dhundo, aage khada karo. Repeat. (A23 ka minIndex yahan LOOP me chala!)
</details>

---

## MD15. Insertion Sort
<details><summary>✅ Solution</summary>

```java
for (int i = 1; i < arr.length; i++) {
    int key = arr[i], j = i - 1;
    while (j >= 0 && arr[j] > key) {
        arr[j + 1] = arr[j];    // bade elements right khisko
        j--;
    }
    arr[j + 1] = key;
}
```
**Analogy:** Taash ke patte haath me sort karna — naya patta sahi jagah GHUSA do.
</details>

---

## MD16. Count Frequency — Sorted Output
**Problem:** `"banana" → a:3, b:1, n:2` (alphabetical order me!)

<details><summary>✅ Solution</summary>

```java
TreeMap<Character, Integer> freq = new TreeMap<>();   // TreeMap = sorted keys!
for (char c : s.toCharArray())
    freq.put(c, freq.getOrDefault(c, 0) + 1);
System.out.println(freq);   // {a=3, b=1, n=2}
```
**Idea:** HashMap ka sorted bhai = TreeMap. Keys hamesha sorted order me.
</details>

---

## MD17. Longest Common Prefix
**Problem:** `{"flower", "flow", "flight"} → "fl"`

<details><summary>✅ Solution</summary>

```java
String prefix = arr[0];
for (int i = 1; i < arr.length; i++) {
    while (!arr[i].startsWith(prefix))
        prefix = prefix.substring(0, prefix.length() - 1);   // chhota karte jao
}
```
**Idea:** Pehle word ko prefix maano, har word ke saath match hone tak kaat-te jao.
</details>

---

## MD18. String Compression
**Problem:** `"aabbbcc" → "a2b3c2"`

<details><summary>✅ Solution</summary>

```java
StringBuilder sb = new StringBuilder();
int count = 1;
for (int i = 1; i <= s.length(); i++) {
    if (i < s.length() && s.charAt(i) == s.charAt(i - 1)) count++;
    else {
        sb.append(s.charAt(i - 1)).append(count);
        count = 1;
    }
}
```
**Idea:** Same chalta raha → count++. Toota → likh do aur reset. `i <= length()` ka trick last group handle karta hai.
</details>

---

## MD19. Check String Rotation
**Problem:** "abcd" aur "cdab" — kya ek doosre ka rotation hai?

<details><summary>✅ Solution</summary>

```java
boolean isRotation = s1.length() == s2.length() && (s1 + s1).contains(s2);
```
**Mind-blow:** `"abcd"+"abcd" = "abcdabcd"` — ismein HAR rotation chhupa hai ("bcda", "cdab", "dabc")! One-liner magic.
</details>

---

## MD20. Balanced Brackets ⭐
**Problem:** `"({[]})" → balanced, "([)]" → nahi`

<details><summary>✅ Solution</summary>

```java
ArrayDeque<Character> stack = new ArrayDeque<>();
boolean ok = true;
for (char c : s.toCharArray()) {
    if (c == '(' || c == '{' || c == '[') stack.push(c);
    else {
        if (stack.isEmpty()) { ok = false; break; }
        char open = stack.pop();
        if ((c == ')' && open != '(') || (c == '}' && open != '{')
            || (c == ']' && open != '[')) { ok = false; break; }
    }
}
ok = ok && stack.isEmpty();
```
**Idea:** Stack (note 02 ki plates!) — khula bracket push, band aaya toh top se match hona chahiye. LIFO ka perfect use.
</details>

---

## MD21. Fast Power (recursion)
**Problem:** x^n calculate karo O(log n) me. `2^10 → 1024`

<details><summary>✅ Solution</summary>

```java
static long power(long x, int n) {
    if (n == 0) return 1;
    long half = power(x, n / 2);
    return (n % 2 == 0) ? half * half : half * half * x;
}
```
**Idea:** 2^10 = (2^5)² — aadha calculate karo, square kar do. 10 multiplications ki jagah sirf 4!
</details>

---

## MD22. Find Missing AND Repeating
**Problem:** 1..n me ek number gayab, ek do baar. `{1, 2, 2, 4} → missing=3, repeat=2`

<details><summary>✅ Solution</summary>

```java
HashSet<Integer> seen = new HashSet<>();
int repeat = -1, actualSum = 0;
for (int x : arr) {
    if (!seen.add(x)) repeat = x;
    actualSum += x;
}
int missing = n * (n + 1) / 2 - (actualSum - repeat);
```
**Idea:** A12 (duplicate) + A18 (missing via Gauss) ka fusion — do easy = ek medium!
</details>

---

## MD23. Subarray with Given Sum (positives)
**Problem:** `{1, 4, 20, 3, 10, 5}, sum=33 → subarray {20, 3, 10}`

<details><summary>✅ Solution</summary>

```java
int start = 0, curr = 0;
for (int end = 0; end < arr.length; end++) {
    curr += arr[end];                          // window badhao
    while (curr > sum) curr -= arr[start++];   // zyada ho gaya? left se ghatao
    if (curr == sum) {
        System.out.println(start + " to " + end);
        break;
    }
}
```
**Idea:** **Sliding window** — rabbar ki khidki: right se phailao, zyada ho jaye toh left se sikodo. Nayi technique unlock! 🔓
</details>

---

## MD24. Intersection Point Value of Two Sorted Arrays
**Problem:** Do sorted arrays ke common elements. `{1,3,4,5,7} & {2,3,5,6} → 3 5`

<details><summary>✅ Solution</summary>

```java
int i = 0, j = 0;
while (i < a.length && j < b.length) {
    if (a[i] == b[j]) { System.out.print(a[i] + " "); i++; j++; }
    else if (a[i] < b[j]) i++;
    else j++;
}
```
**Idea:** MD10 (merge) wala two-pointer — par ab sirf MATCH pe print. Same technique, naya use.
</details>

---

## MD25. Second Most Frequent Character
**Problem:** `"aabbbcccc" → 'b'` (c=4 sabse zyada, b=3 doosra)

<details><summary>✅ Solution</summary>

```java
HashMap<Character, Integer> freq = new HashMap<>();
for (char c : s.toCharArray()) freq.put(c, freq.getOrDefault(c, 0) + 1);

char first = 0, second = 0;
int f1 = 0, f2 = 0;
for (var e : freq.entrySet()) {
    if (e.getValue() > f1) {
        f2 = f1; second = first;
        f1 = e.getValue(); first = e.getKey();
    } else if (e.getValue() > f2) {
        f2 = e.getValue(); second = e.getKey();
    }
}
System.out.println(second);
```
**Idea:** Frequency map (S5) + second largest logic (A4) — do purane dost mil ke naya question tod diya!
</details>

---

## 🎯 Batch 1 done! Techniques unlocked:

| Technique | Questions |
|-----------|-----------|
| HashMap partner-lookup | MD1, MD22 |
| Two-pointer | MD2, MD4, MD10, MD24 |
| Reversal trick | MD3, MD12 |
| Binary search | MD5 |
| Kadane / running decision | MD6, MD7, MD8, MD9 |
| Stack | MD20 |
| Sliding window | MD23 |
| Divide & conquer recursion | MD21 |

Ye 8 techniques aage Hard level ke 80% questions kholti hain! 🔑

⬅️ [Easy questions](../easy/numbers.md) | 🏠 [Roadmap](../../README.md)
