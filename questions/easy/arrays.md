# 📦 Easy — Arrays (A1–A25)

> Note 06 revise karke aao — `length`, index 0 se, two-pointer. Yahan har array question ka base pattern milega.

---

## A1. Sum & Average
**Problem:** `{10,20,30,40} → Sum=100, Avg=25.0`
<details><summary>✅ Solution</summary>

```java
int sum = 0;
for (int x : arr) sum += x;
double avg = (double) sum / arr.length;
```
**Trap:** `(double)` cast — warna int division!
</details>

---

## A2. Maximum Element
<details><summary>✅ Solution</summary>

```java
int max = arr[0];
for (int x : arr) if (x > max) max = x;
```
</details>

---

## A3. Minimum Element
<details><summary>✅ Solution</summary>

```java
int min = arr[0];
for (int x : arr) if (x < min) min = x;
```
</details>

---

## A4. Second Largest ⭐
**Problem:** `{10, 5, 20, 8} → 10`
<details><summary>✅ Solution</summary>

```java
int first = Integer.MIN_VALUE, second = Integer.MIN_VALUE;
for (int x : arr) {
    if (x > first) { second = first; first = x; }
    else if (x > second && x != first) second = x;
}
```
**Idea:** Champion + runner-up ek saath track. (Dry run: Starter Pack Q20)
</details>

---

## A5. Linear Search
<details><summary>✅ Solution</summary>

```java
int index = -1;
for (int i = 0; i < arr.length; i++)
    if (arr[i] == target) { index = i; break; }
```
</details>

---

## A6. Reverse Array (in-place)
<details><summary>✅ Solution</summary>

```java
int l = 0, r = arr.length - 1;
while (l < r) {
    int t = arr[l]; arr[l] = arr[r]; arr[r] = t;
    l++; r--;
}
```
**Idea:** Two-pointer — kinaron se swap karte hue milo.
</details>

---

## A7. Count Even & Odd
<details><summary>✅ Solution</summary>

```java
int even = 0, odd = 0;
for (int x : arr) { if (x % 2 == 0) even++; else odd++; }
```
</details>

---

## A8. Count Positive, Negative, Zero
<details><summary>✅ Solution</summary>

```java
int pos = 0, neg = 0, zero = 0;
for (int x : arr) {
    if (x > 0) pos++;
    else if (x < 0) neg++;
    else zero++;
}
```
</details>

---

## A9. Copy Array (sahi tarika)
<details><summary>✅ Solution</summary>

```java
int[] copy = Arrays.copyOf(arr, arr.length);
// b = a ❌ — wo copy nahi, SAME array ka doosra naam hai (note 06 trap!)
```
</details>

---

## A10. Swap First & Last
<details><summary>✅ Solution</summary>

```java
int t = arr[0];
arr[0] = arr[arr.length - 1];
arr[arr.length - 1] = t;
```
</details>

---

## A11. Element ki Occurrences Count
**Problem:** `{2, 5, 2, 8, 2}, x=2 → 3 baar`
<details><summary>✅ Solution</summary>

```java
int count = 0;
for (int v : arr) if (v == x) count++;
```
</details>

---

## A12. Duplicate Check
<details><summary>✅ Solution</summary>

```java
HashSet<Integer> seen = new HashSet<>();
boolean dup = false;
for (int x : arr)
    if (!seen.add(x)) { dup = true; break; }
```
**Idea:** `add()` false = pehle se tha (note 14).
</details>

---

## A13. Frequency of Each Element
**Problem:** `{1, 2, 2, 3} → 1:1, 2:2, 3:1`
<details><summary>✅ Solution</summary>

```java
HashMap<Integer, Integer> freq = new HashMap<>();
for (int x : arr) freq.put(x, freq.getOrDefault(x, 0) + 1);
System.out.println(freq);
```
**Idea:** THE frequency pattern — rat lo ise!
</details>

---

## A14. Bubble Sort (ascending) ⭐
<details><summary>✅ Solution</summary>

```java
for (int i = 0; i < arr.length - 1; i++) {
    for (int j = 0; j < arr.length - 1 - i; j++) {
        if (arr[j] > arr[j + 1]) {
            int t = arr[j]; arr[j] = arr[j + 1]; arr[j + 1] = t;
        }
    }
}
```
**Idea:** Bade bubbles upar (right) tairte jaate hain — har pass me sabse bada apni jagah pahunch jaata hai. Shortcut: `Arrays.sort(arr)`.
</details>

---

## A15. Is Array Sorted?
<details><summary>✅ Solution</summary>

```java
boolean sorted = true;
for (int i = 0; i < arr.length - 1; i++)
    if (arr[i] > arr[i + 1]) { sorted = false; break; }
```
**Idea:** Har padosİ pair check — koi ulta mila toh sorted nahi.
</details>

---

## A16. Merge Two Arrays
<details><summary>✅ Solution</summary>

```java
int[] merged = new int[a.length + b.length];
for (int i = 0; i < a.length; i++) merged[i] = a[i];
for (int i = 0; i < b.length; i++) merged[a.length + i] = b[i];
```
</details>

---

## A17. Common Elements (intersection)
<details><summary>✅ Solution</summary>

```java
HashSet<Integer> setA = new HashSet<>();
for (int x : a) setA.add(x);
for (int x : b)
    if (setA.contains(x)) System.out.print(x + " ");
```
</details>

---

## A18. Missing Number (1 to n) ⭐
**Problem:** `{1, 2, 4, 5}, n=5 → 3 missing`
<details><summary>✅ Solution</summary>

```java
int expected = n * (n + 1) / 2;    // Gauss formula (N20!)
int actual = 0;
for (int x : arr) actual += x;
System.out.println(expected - actual);
```
**Idea:** Hona chahiye tha − jo hai = jo gayab hai. Maths beats loops!
</details>

---

## A19. Left Rotate by 1
**Problem:** `{1,2,3,4} → {2,3,4,1}`
<details><summary>✅ Solution</summary>

```java
int first = arr[0];
for (int i = 0; i < arr.length - 1; i++) arr[i] = arr[i + 1];
arr[arr.length - 1] = first;
```
**Idea:** Pehla bacha lo, sabko ek ghar left khisko, pehla aakhir me.
</details>

---

## A20. Insert at Position
**Problem:** `{1,2,4,5}` me index 2 pe 3 daalo
<details><summary>✅ Solution</summary>

```java
int[] res = new int[arr.length + 1];
for (int i = 0; i < pos; i++) res[i] = arr[i];
res[pos] = value;
for (int i = pos; i < arr.length; i++) res[i + 1] = arr[i];
```
**Idea:** Array ka size fixed hai — naya bada array banana padta hai. (Isliye ArrayList better — note 14!)
</details>

---

## A21. Delete Element at Index
<details><summary>✅ Solution</summary>

```java
int[] res = new int[arr.length - 1];
for (int i = 0, j = 0; i < arr.length; i++)
    if (i != pos) res[j++] = arr[i];
```
</details>

---

## A22. Even/Odd Alag Arrays Me
<details><summary>✅ Solution</summary>

```java
ArrayList<Integer> evens = new ArrayList<>(), odds = new ArrayList<>();
for (int x : arr) {
    if (x % 2 == 0) evens.add(x);
    else odds.add(x);
}
```
**Idea:** Size pata nahi kitna hoga — ArrayList perfect (auto-grow!).
</details>

---

## A23. Index of Minimum
<details><summary>✅ Solution</summary>

```java
int minIdx = 0;
for (int i = 1; i < arr.length; i++)
    if (arr[i] < arr[minIdx]) minIdx = i;
```
**Idea:** Value nahi, INDEX track karo.
</details>

---

## A24. Sum of Two Arrays (element-wise)
**Problem:** `{1,2,3} + {4,5,6} → {5,7,9}`
<details><summary>✅ Solution</summary>

```java
int[] sum = new int[a.length];
for (int i = 0; i < a.length; i++) sum[i] = a[i] + b[i];
```
</details>

---

## A25. 2D Array — Row & Column Sums
<details><summary>✅ Solution</summary>

```java
int[][] m = {{1,2,3},{4,5,6}};
for (int i = 0; i < m.length; i++) {
    int rowSum = 0;
    for (int j = 0; j < m[i].length; j++) rowSum += m[i][j];
    System.out.println("Row " + i + " sum = " + rowSum);
}
```
**Idea:** 2D = array of arrays (note 06 cinema seats). `m.length` = rows, `m[i].length` = us row ke columns.
</details>

---

➡️ **Next category:** [Strings](strings.md) | ⬅️ [Patterns](patterns.md) | 🏠 [Roadmap](../../README.md)
