# 🔤 Easy — Strings (S1–S25)

> Note 07 revise karo — `charAt`, `length()`, immutability, `equals` vs `==`. Strings exams ke sabse favourite questions hain!

---

## S1. Reverse a String
**Problem:** `"hello" → "olleh"`
<details><summary>✅ Solution</summary>

```java
StringBuilder rev = new StringBuilder();
for (int i = s.length() - 1; i >= 0; i--) rev.append(s.charAt(i));
// Shortcut: new StringBuilder(s).reverse().toString()
```
</details>

---

## S2. Palindrome String
**Problem:** `"madam" → yes`
<details><summary>✅ Solution</summary>

```java
boolean palin = true;
int l = 0, r = s.length() - 1;
while (l < r)
    if (s.charAt(l++) != s.charAt(r--)) { palin = false; break; }
```
**Idea:** Two-pointer compare — swap nahi, sirf match check.
</details>

---

## S3. Count Vowels & Consonants
<details><summary>✅ Solution</summary>

```java
int v = 0, c = 0;
for (char ch : s.toLowerCase().toCharArray()) {
    if (ch >= 'a' && ch <= 'z') {
        if ("aeiou".indexOf(ch) != -1) v++;
        else c++;
    }
}
```
**Idea:** `"aeiou".indexOf(ch)` — vowel list me dhundo, -1 = nahi mila.
</details>

---

## S4. Count Words
**Problem:** `"Java is fun" → 3`
<details><summary>✅ Solution</summary>

```java
int words = s.trim().isEmpty() ? 0 : s.trim().split("\\s+").length;
```
</details>

---

## S5. Character Frequency ⭐
<details><summary>✅ Solution</summary>

```java
HashMap<Character, Integer> freq = new HashMap<>();
for (char c : s.toCharArray())
    freq.put(c, freq.getOrDefault(c, 0) + 1);
```
</details>

---

## S6. Toggle Case
**Problem:** `"JaVa" → "jAvA"`
<details><summary>✅ Solution</summary>

```java
StringBuilder sb = new StringBuilder();
for (char c : s.toCharArray()) {
    if (Character.isUpperCase(c)) sb.append(Character.toLowerCase(c));
    else sb.append(Character.toUpperCase(c));
}
```
</details>

---

## S7. Remove All Spaces
<details><summary>✅ Solution</summary>

```java
String res = s.replace(" ", "");
```
**Yaad:** String immutable hai — `replace` NAYI string deta hai, `res` me pakdo!
</details>

---

## S8. Count Upper, Lower, Digits, Specials
<details><summary>✅ Solution</summary>

```java
int up = 0, low = 0, dig = 0, spl = 0;
for (char c : s.toCharArray()) {
    if (Character.isUpperCase(c)) up++;
    else if (Character.isLowerCase(c)) low++;
    else if (Character.isDigit(c)) dig++;
    else spl++;
}
```
**Idea:** `Character` class ke ready-made checkers — kaam aasaan.
</details>

---

## S9. First Non-Repeated Character ⭐
**Problem:** `"swiss" → 'w'`
<details><summary>✅ Solution</summary>

```java
HashMap<Character, Integer> freq = new HashMap<>();
for (char c : s.toCharArray()) freq.put(c, freq.getOrDefault(c, 0) + 1);
for (char c : s.toCharArray())
    if (freq.get(c) == 1) { System.out.println(c); break; }
```
**Idea:** Pehle frequency banao, fir string ke ORDER me pehla 1-count wala dhundo.
</details>

---

## S10. Find Duplicate Characters
**Problem:** `"programming" → r, g, m`
<details><summary>✅ Solution</summary>

```java
HashMap<Character, Integer> freq = new HashMap<>();
for (char c : s.toCharArray()) freq.put(c, freq.getOrDefault(c, 0) + 1);
for (var e : freq.entrySet())
    if (e.getValue() > 1) System.out.print(e.getKey() + " ");
```
</details>

---

## S11. Anagram Check ⭐
**Problem:** `"listen", "silent" → yes`
<details><summary>✅ Solution</summary>

```java
char[] a = s1.toCharArray(), b = s2.toCharArray();
Arrays.sort(a); Arrays.sort(b);
System.out.println(Arrays.equals(a, b));
```
**Idea:** Same letters, alag order — sort karo, same nikle toh anagram!
</details>

---

## S12. `==` vs `.equals()` Demo
<details><summary>✅ Solution</summary>

```java
String a = "hello";
String b = new String("hello");
System.out.println(a == b);        // false — alag objects!
System.out.println(a.equals(b));   // true — content same
```
**Yaad:** Content compare = HAMESHA `.equals()` (note 07 ka String Pool funda).
</details>

---

## S13. Capitalize Each Word
**Problem:** `"java is fun" → "Java Is Fun"`
<details><summary>✅ Solution</summary>

```java
StringBuilder sb = new StringBuilder();
for (String w : s.split(" ")) {
    sb.append(Character.toUpperCase(w.charAt(0)))
      .append(w.substring(1)).append(" ");
}
String res = sb.toString().trim();
```
**Idea:** Har word: pehla letter upar + baaki jaisa hai.
</details>

---

## S14. Reverse Word Order ⭐
**Problem:** `"Java is fun" → "fun is Java"`
<details><summary>✅ Solution</summary>

```java
String[] words = s.split(" ");
StringBuilder sb = new StringBuilder();
for (int i = words.length - 1; i >= 0; i--)
    sb.append(words[i]).append(" ");
```
**Fark S1 se:** letters nahi, WORDS ulte karne hain — pehle todo, fir ulta jodo.
</details>

---

## S15. Count Occurrences of a Character
**Problem:** `"banana", 'a' → 3`
<details><summary>✅ Solution</summary>

```java
int count = 0;
for (char c : s.toCharArray()) if (c == target) count++;
```
</details>

---

## S16. Remove Duplicate Characters
**Problem:** `"programming" → "progamin"`
<details><summary>✅ Solution</summary>

```java
LinkedHashSet<Character> set = new LinkedHashSet<>();
for (char c : s.toCharArray()) set.add(c);
StringBuilder sb = new StringBuilder();
for (char c : set) sb.append(c);
```
**Idea:** `LinkedHashSet` = HashSet + ORDER yaad rakhta hai. Perfect combo yahan!
</details>

---

## S17. Check String is Numeric
**Problem:** `"12345" → yes, "12a45" → no`
<details><summary>✅ Solution</summary>

```java
boolean numeric = !s.isEmpty();
for (char c : s.toCharArray())
    if (!Character.isDigit(c)) { numeric = false; break; }
```
</details>

---

## S18. Largest & Smallest Word
**Problem:** `"Java is awesome" → largest: awesome, smallest: is`
<details><summary>✅ Solution</summary>

```java
String[] words = s.split(" ");
String big = words[0], small = words[0];
for (String w : words) {
    if (w.length() > big.length()) big = w;
    if (w.length() < small.length()) small = w;
}
```
**Idea:** Max/min pattern (A2/A3) — bas compare `.length()` se.
</details>

---

## S19. String to Integer (aur wapas)
<details><summary>✅ Solution</summary>

```java
int n = Integer.parseInt("123");     // String → int
String s2 = String.valueOf(456);      // int → String
```
**Trap:** `parseInt("12a")` → `NumberFormatException` (note 13) — try-catch lagao user input pe!
</details>

---

## S20. Sort Characters of String
**Problem:** `"banana" → "aaabnn"`
<details><summary>✅ Solution</summary>

```java
char[] ch = s.toCharArray();
Arrays.sort(ch);
String sorted = new String(ch);
```
</details>

---

## S21. Check Substring Present
<details><summary>✅ Solution</summary>

```java
boolean has = s.contains("fun");
int pos = s.indexOf("fun");    // -1 = nahi mila
```
</details>

---

## S22. Compare Two Strings (dictionary order)
<details><summary>✅ Solution</summary>

```java
int cmp = s1.compareTo(s2);
// negative: s1 pehle aata hai, 0: equal, positive: s2 pehle
```
**Use:** Names ko alphabetically sort karne ka base.
</details>

---

## S23. Count Occurrences of a Word
**Problem:** `"the cat and the dog", "the" → 2`
<details><summary>✅ Solution</summary>

```java
int count = 0;
for (String w : s.split("\\s+"))
    if (w.equals(target)) count++;
```
**Trap:** `==` nahi, `.equals()`!
</details>

---

## S24. ASCII Values of String
<details><summary>✅ Solution</summary>

```java
for (char c : s.toCharArray())
    System.out.println(c + " = " + (int) c);
```
</details>

---

## S25. Swap Case of First & Last
**Problem:** `"java" → "Java" style khel — first & last upar: "JavA"`
<details><summary>✅ Solution</summary>

```java
StringBuilder sb = new StringBuilder(s);
sb.setCharAt(0, Character.toUpperCase(s.charAt(0)));
sb.setCharAt(s.length() - 1, Character.toUpperCase(s.charAt(s.length() - 1)));
```
**Idea:** String badal nahi sakte — StringBuilder ka `setCharAt` kaam karta hai!
</details>

---

➡️ **Next category:** [Collections & Methods](mixed.md) | ⬅️ [Arrays](arrays.md) | 🏠 [Roadmap](../../README.md)
