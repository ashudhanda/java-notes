# 🔴 Hard Questions (HD1–HD18)

> Welcome to boss level! 👾 Yahan har question ek FAMOUS problem hai — interviews me baar-baar aati hain. Dar mat: har ek Medium ki techniques se hi bani hai, bas layers zyada hain. **Pehle hint se 15-20 min KHUD try karo** — Hard level ka asli fayda struggle karne me hai!

---

## HD1. Tower of Hanoi ⭐⭐
**Problem:** n disks ko rod A se rod C le jao (rod B helper). Rule: bada disk chhote ke upar nahi. Moves print karo.

<details><summary>💡 Hint</summary>

n disks A→C = (n-1 disks A→B) + (bada disk A→C) + (n-1 disks B→C). Recursion khud sochne do!
</details>

<details><summary>✅ Solution</summary>

```java
static void hanoi(int n, char from, char helper, char to) {
    if (n == 0) return;
    hanoi(n - 1, from, to, helper);   // n-1 ko helper pe rakho
    System.out.println("Disk " + n + ": " + from + " -> " + to);
    hanoi(n - 1, helper, from, to);   // n-1 ko helper se target pe lao
}
// hanoi(3, 'A', 'B', 'C') → 7 moves
```
**Idea:** Recursion ka sabse sundar example — "bade problem ko chhota banao, baaki recursion sambhal lega" (note 08). Total moves = 2ⁿ − 1. 64 disks = 585 billion saal 😅
</details>

---

## HD2. Print All Subsets (Power Set) ⭐
**Problem:** `{1, 2, 3}` ke saare subsets: `[], [1], [2], [3], [1,2], [1,3], [2,3], [1,2,3]`

<details><summary>💡 Hint</summary>

Har element ke paas 2 choices: subset me AAO ya MAT aao. n elements = 2ⁿ subsets.
</details>

<details><summary>✅ Solution</summary>

```java
static void subsets(int[] arr, int i, ArrayList<Integer> curr) {
    if (i == arr.length) {
        System.out.println(curr);
        return;
    }
    subsets(arr, i + 1, curr);          // Choice 1: element chhodo
    curr.add(arr[i]);
    subsets(arr, i + 1, curr);          // Choice 2: element lo
    curr.remove(curr.size() - 1);       // backtrack — wapas hatao!
}
```
**Idea:** **Backtracking ka pehla step:** choice karo → aage jao → wapas aake choice UNDO karo. Ye undo hi backtracking hai!
</details>

---

## HD3. All Permutations of a String ⭐
**Problem:** `"abc" → abc, acb, bac, bca, cab, cba` (n! permutations)

<details><summary>✅ Solution</summary>

```java
static void permute(char[] ch, int i) {
    if (i == ch.length) {
        System.out.println(new String(ch));
        return;
    }
    for (int j = i; j < ch.length; j++) {
        char t = ch[i]; ch[i] = ch[j]; ch[j] = t;   // swap
        permute(ch, i + 1);
        t = ch[i]; ch[i] = ch[j]; ch[j] = t;        // swap wapas (backtrack)
    }
}
```
**Idea:** Position i pe har character ko try karo (swap se lao), aage recursion, fir UNDO. Same backtracking pattern!
</details>

---

## HD4. N-Queens (4×4) ⭐⭐
**Problem:** 4 queens ko 4×4 board pe rakho — koi kisi ko attack na kare.

<details><summary>💡 Hint</summary>

Row by row rakho. Har row me har column try karo — safe hai toh aage badho, fas gaye toh WAPAS aake agla column try karo.
</details>

<details><summary>✅ Solution</summary>

```java
static boolean solve(int[][] board, int row, int n) {
    if (row == n) return true;                    // sab queens lag gayi!
    for (int col = 0; col < n; col++) {
        if (isSafe(board, row, col, n)) {
            board[row][col] = 1;
            if (solve(board, row + 1, n)) return true;
            board[row][col] = 0;                  // backtrack!
        }
    }
    return false;   // is row me koi jagah nahi → peechhe jao
}

static boolean isSafe(int[][] b, int row, int col, int n) {
    for (int i = 0; i < row; i++)
        if (b[i][col] == 1) return false;                        // upar wala column
    for (int i = row - 1, j = col - 1; i >= 0 && j >= 0; i--, j--)
        if (b[i][j] == 1) return false;                          // left diagonal
    for (int i = row - 1, j = col + 1; i >= 0 && j < n; i--, j++)
        if (b[i][j] == 1) return false;                          // right diagonal
    return true;
}
```
**Idea:** Backtracking ka KING. Try → fail → undo → try next. Bhool-bhulaiya me raasta dhundna — dead end aaye toh wapas mud ke doosra raasta.
</details>

---

## HD5. Merge Sort ⭐⭐
**Problem:** Array ko O(n log n) me sort karo — divide & conquer se.

<details><summary>💡 Hint</summary>

Aadha karo, dono side sort karo (recursion), fir MERGE (MD10 wala!) kar do.
</details>

<details><summary>✅ Solution</summary>

```java
static void mergeSort(int[] a, int l, int r) {
    if (l >= r) return;               // 1 element = already sorted
    int mid = (l + r) / 2;
    mergeSort(a, l, mid);
    mergeSort(a, mid + 1, r);
    merge(a, l, mid, r);
}

static void merge(int[] a, int l, int mid, int r) {
    int[] temp = new int[r - l + 1];
    int i = l, j = mid + 1, k = 0;
    while (i <= mid && j <= r)
        temp[k++] = (a[i] <= a[j]) ? a[i++] : a[j++];
    while (i <= mid) temp[k++] = a[i++];
    while (j <= r) temp[k++] = a[j++];
    for (int x = 0; x < temp.length; x++) a[l + x] = temp[x];
}
```
**Analogy:** Copies ka bundle sort karna — do students me aadha-aadha baanto, dono apna sort karein, fir MD10 wale merge se jodo. Bubble sort (A14) O(n²) vs ye O(n log n) — 1 lakh elements pe ~5000x faster!
</details>

---

## HD6. Quick Sort ⭐⭐
<details><summary>✅ Solution</summary>

```java
static void quickSort(int[] a, int lo, int hi) {
    if (lo >= hi) return;
    int pivot = a[hi], i = lo - 1;
    for (int j = lo; j < hi; j++) {
        if (a[j] < pivot) {
            i++;
            int t = a[i]; a[i] = a[j]; a[j] = t;
        }
    }
    int t = a[i + 1]; a[i + 1] = a[hi]; a[hi] = t;   // pivot apni jagah
    quickSort(a, lo, i);
    quickSort(a, i + 2, hi);
}
```
**Analogy:** Pivot = class monitor. "Mujhse chhote LEFT, bade RIGHT!" — monitor apni final jagah pe. Fir dono groups me naye monitors. Sab apni jagah = sorted!
</details>

---

## HD7. Spiral Matrix Print ⭐
**Problem:**
```
1  2  3
4  5  6   →  1 2 3 6 9 8 7 4 5
7  8  9
```

<details><summary>✅ Solution</summary>

```java
int top = 0, bottom = rows - 1, left = 0, right = cols - 1;
while (top <= bottom && left <= right) {
    for (int j = left; j <= right; j++) System.out.print(m[top][j] + " ");
    top++;
    for (int i = top; i <= bottom; i++) System.out.print(m[i][right] + " ");
    right--;
    if (top <= bottom)
        for (int j = right; j >= left; j--) System.out.print(m[bottom][j] + " ");
    bottom--;
    if (left <= right)
        for (int i = bottom; i >= top; i--) System.out.print(m[i][left] + " ");
    left++;
}
```
**Idea:** 4 boundaries rakho (top/bottom/left/right) — ek layer print karo, boundary andar sikodo. Pyaaz ke chhilke jaisa 🧅
</details>

---

## HD8. Trapping Rain Water ⭐⭐
**Problem:** Buildings ki heights `{4,2,0,3,2,5}` — beech me kitna paani rukega? → `9`

<details><summary>💡 Hint</summary>

Har position pe paani = min(left ka max, right ka max) − meri height.
</details>

<details><summary>✅ Solution</summary>

```java
int n = h.length;
int[] leftMax = new int[n], rightMax = new int[n];
leftMax[0] = h[0];
for (int i = 1; i < n; i++) leftMax[i] = Math.max(leftMax[i - 1], h[i]);
rightMax[n - 1] = h[n - 1];
for (int i = n - 2; i >= 0; i--) rightMax[i] = Math.max(rightMax[i + 1], h[i]);
int water = 0;
for (int i = 0; i < n; i++)
    water += Math.min(leftMax[i], rightMax[i]) - h[i];
```
**Idea:** Paani wahi tak bharega jahan tak DONO taraf ki sabse chhoti deewar allow kare. leftMax/rightMax pre-compute = O(n). MD8 (leaders) wala running-max idea, dono directions me!
</details>

---

## HD9. Search in Rotated Sorted Array ⭐
**Problem:** `{4,5,6,7,0,1,2}, target=0 → index 4` — O(log n) me!

<details><summary>✅ Solution</summary>

```java
int lo = 0, hi = arr.length - 1;
while (lo <= hi) {
    int mid = lo + (hi - lo) / 2;
    if (arr[mid] == target) { System.out.println(mid); break; }
    if (arr[lo] <= arr[mid]) {                    // left half sorted hai
        if (target >= arr[lo] && target < arr[mid]) hi = mid - 1;
        else lo = mid + 1;
    } else {                                       // right half sorted hai
        if (target > arr[mid] && target <= arr[hi]) lo = mid + 1;
        else hi = mid - 1;
    }
}
```
**Idea:** Binary search (MD5) ka twist — rotated array me EK half hamesha sorted hota hai. Sorted half me target hai ya nahi — ye check karke side chuno.
</details>

---

## HD10. Kth Largest Element
**Problem:** `{3, 2, 1, 5, 6, 4}, k=2 → 5`

<details><summary>✅ Solution</summary>

```java
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
for (int x : arr) {
    minHeap.add(x);
    if (minHeap.size() > k) minHeap.poll();   // sabse chhota nikaal do
}
System.out.println(minHeap.peek());
```
**Idea:** **PriorityQueue** = naya collection unlock! Min-heap me sirf k sabse bade rakho — top wala hi kth largest. VIP list me sirf k seats — chhota aaya toh bahar!
</details>

---

## HD11. Longest Substring Without Repeating Characters ⭐⭐
**Problem:** `"abcabcbb" → 3` ("abc")

<details><summary>💡 Hint</summary>

Sliding window (MD23) + HashSet — duplicate aaya toh left se sikodo.
</details>

<details><summary>✅ Solution</summary>

```java
HashSet<Character> window = new HashSet<>();
int left = 0, best = 0;
for (int right = 0; right < s.length(); right++) {
    while (window.contains(s.charAt(right)))
        window.remove(s.charAt(left++));    // duplicate? left se hatao
    window.add(s.charAt(right));
    best = Math.max(best, right - left + 1);
}
```
**Idea:** Window me kabhi duplicate nahi — aate hi left se sikod ke nikal do. Sliding window + Set ka classic combo.
</details>

---

## HD12. Longest Palindromic Substring ⭐
**Problem:** `"babad" → "bab"` (ya "aba")

<details><summary>✅ Solution</summary>

```java
static String longestPalin(String s) {
    String best = "";
    for (int c = 0; c < s.length(); c++) {
        best = better(best, expand(s, c, c));       // odd length center
        best = better(best, expand(s, c, c + 1));   // even length center
    }
    return best;
}
static String expand(String s, int l, int r) {
    while (l >= 0 && r < s.length() && s.charAt(l) == s.charAt(r)) { l--; r++; }
    return s.substring(l + 1, r);
}
static String better(String a, String b) { return a.length() >= b.length() ? a : b; }
```
**Idea:** **Expand around center** — har position ko palindrome ka CENTER maano aur dono taraf phailo jab tak match ho. 2n-1 centers (odd + even).
</details>

---

## HD13. Fibonacci with Memoization — DP INTRO ⭐⭐
**Problem:** M8 wala recursive fib(50) chalao — hang ho jayega! Fix karo.

<details><summary>💡 Hint</summary>

fib(5) me fib(3) DO baar computed hota hai, fib(2) TEEN baar... Ek baar nikala toh YAAD kar lo!
</details>

<details><summary>✅ Solution</summary>

```java
static long[] memo = new long[51];
static long fib(int n) {
    if (n <= 1) return n;
    if (memo[n] != 0) return memo[n];    // pehle se yaad hai? wahi lauta do
    memo[n] = fib(n - 1) + fib(n - 2);
    return memo[n];
}
```
**Idea:** Ye hai **Dynamic Programming (DP)** — "compute once, remember forever". fib(50): bina memo ~40 MINUTES, memo ke saath 0.001 second. Ek array ne 2.4 million× speed di! 🤯
</details>

---

## HD14. Climbing Stairs (DP) ⭐
**Problem:** n seedhiyan, ek baar me 1 ya 2 chadh sakte ho. Kitne tarike? `n=4 → 5`

<details><summary>✅ Solution</summary>

```java
if (n <= 2) return n;
int a = 1, b = 2;
for (int i = 3; i <= n; i++) {
    int c = a + b; a = b; b = c;
}
return b;
```
**Idea:** Step n tak: (n-1 se 1 chadho) + (n-2 se 2 chadho) → ways(n) = ways(n-1) + ways(n-2). Ye toh Fibonacci hai! DP ka pehla lesson: problem ko PICHLE answers se jodo.
</details>

---

## HD15. Coin Change — Minimum Coins (DP)
**Problem:** Coins `{1, 5, 10}`, amount 18 → min coins = 5 (10+5+1+1+1)

<details><summary>✅ Solution</summary>

```java
int[] dp = new int[amount + 1];
Arrays.fill(dp, Integer.MAX_VALUE - 1);
dp[0] = 0;
for (int amt = 1; amt <= amount; amt++)
    for (int coin : coins)
        if (coin <= amt)
            dp[amt] = Math.min(dp[amt], 1 + dp[amt - coin]);
System.out.println(dp[amount]);
```
**Idea:** dp[amt] = "amt banane ke min coins". Har coin try karo: 1 + dp[bacha hua]. Chhote answers se bade answers — DP table bhardo!
</details>

---

## HD16. Longest Common Subsequence (DP) ⭐
**Problem:** `"abcde", "ace" → 3` ("ace" — order same, continuous zaroori nahi)

<details><summary>✅ Solution</summary>

```java
int[][] dp = new int[s1.length() + 1][s2.length() + 1];
for (int i = 1; i <= s1.length(); i++) {
    for (int j = 1; j <= s2.length(); j++) {
        if (s1.charAt(i - 1) == s2.charAt(j - 1))
            dp[i][j] = 1 + dp[i - 1][j - 1];          // match! dono aage
        else
            dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
    }
}
System.out.println(dp[s1.length()][s2.length()]);
```
**Idea:** 2D DP — dp[i][j] = pehle i aur pehle j characters ka answer. Match = diagonal + 1, nahi = upar/left ka max. Git diff, DNA matching — sab yahi algorithm!
</details>

---

## HD17. Rat in a Maze (backtracking)
**Problem:** 0/1 grid — (0,0) se (n-1,n-1) tak raasta hai? (1 = chal sakte ho)

<details><summary>✅ Solution</summary>

```java
static boolean solve(int[][] maze, int i, int j, int n) {
    if (i < 0 || j < 0 || i >= n || j >= n || maze[i][j] != 1) return false;
    if (i == n - 1 && j == n - 1) return true;       // pahunch gaye!
    maze[i][j] = 2;                                   // visited mark
    if (solve(maze, i + 1, j, n) || solve(maze, i, j + 1, n)
        || solve(maze, i - 1, j, n) || solve(maze, i, j - 1, n)) return true;
    maze[i][j] = 1;                                   // backtrack
    return false;
}
```
**Idea:** Charo directions try karo, visited mark karo (infinite loop se bachne ko), fail toh unmark. N-Queens ka chhota bhai.
</details>

---

## HD18. Valid Sudoku Row/Column Check
**Problem:** 9×9 board — kisi row ya column me 1-9 repeat toh nahi?

<details><summary>✅ Solution</summary>

```java
for (int i = 0; i < 9; i++) {
    HashSet<Integer> row = new HashSet<>(), col = new HashSet<>();
    for (int j = 0; j < 9; j++) {
        if (board[i][j] != 0 && !row.add(board[i][j])) return false;
        if (board[j][i] != 0 && !col.add(board[j][i])) return false;
    }
}
return true;
```
**Idea:** A12 wala HashSet duplicate-check, har row aur column pe. `board[i][j]` vs `board[j][i]` ka ulta trick — ek hi loop me row + column dono!
</details>

---

## 🎯 Hard level complete! Kya seekha:

| Concept | Questions |
|---------|-----------|
| Recursion mastery | HD1 (Hanoi) |
| Backtracking (try → undo) | HD2, HD3, HD4, HD17 |
| Divide & Conquer sorting | HD5 (merge), HD6 (quick) |
| Boundary/layer traversal | HD7 (spiral) |
| Pre-computed max arrays | HD8 (rain water) |
| Modified binary search | HD9 |
| PriorityQueue (heap) | HD10 |
| Sliding window + Set | HD11 |
| Expand around center | HD12 |
| **Dynamic Programming** | HD13, HD14, HD15, HD16 |

DP aur backtracking = placement interviews ke sabse bade topics. Inhe baar-baar revise karo! 🔥

⬅️ [Medium](../medium/01-medium.md) | 🏠 [Roadmap](../../README.md)
