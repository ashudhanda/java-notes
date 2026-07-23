# 09 — OOP 1: Classes & Objects (The Heart of Java ❤️)

> Ab tak hum sirf numbers/text pe kaam kar rahe the. OOP me hum REAL WORLD ki cheezein code me bana sakte hain — Student, Car, BankAccount. Yahi Java ka asli power hai.

---

## 1. Why OOP? (The problem it solves)

Ek student ka data rakhna hai: name, roll number, marks. Without OOP:

```java
String student1Name = "Ashu";     int student1Roll = 1;   double student1Marks = 88.5;
String student2Name = "Rahul";    int student2Roll = 2;   double student2Marks = 76.0;
// 50 students? 150 variables!? 😵
```

**OOP solution:** Ek `Student` **class** banao (template), aur 50 **objects** banao (real students). Data + behaviour ek saath, organized.

---

## 2. Class vs Object (THE most important difference)

| | Class | Object |
|--|-------|--------|
| What | **Template / blueprint** | **Real thing** made from template |
| Exists in memory? | No (just design) | Yes (in Heap!) |
| How many? | Written once | As many as you want |

### 🏭 Analogy 1: Cake mould 🎂
Class = cake ka **mould** (shape design). Objects = us mould se bane **real cakes** (chocolate, vanilla, strawberry — sab alag, mould same).

### 🏭 Analogy 2: Aadhaar card form
Class = **blank form ka design** (fields: name, DOB, address). Object = **bhara hua form** (Ashu ka apna data).

---

## 3. Your first class + objects

```java
// The template
class Student {
    // 1. Fields / instance variables (DATA — what a student HAS)
    String name;
    int roll;
    double marks;

    // 2. Methods (BEHAVIOUR — what a student can DO)
    void introduce() {
        System.out.println("Hi, I am " + name + ", roll no. " + roll);
    }

    boolean isPassed() {
        return marks >= 40;
    }
}

// Using it
public class Main {
    public static void main(String[] args) {
        Student s1 = new Student();      // object 1 created in Heap!
        s1.name = "Ashu";
        s1.roll = 1;
        s1.marks = 88.5;

        Student s2 = new Student();      // object 2 — completely separate
        s2.name = "Rahul";
        s2.roll = 2;
        s2.marks = 35.0;

        s1.introduce();                  // Hi, I am Ashu, roll no. 1
        s2.introduce();                  // Hi, I am Rahul, roll no. 2
        System.out.println(s1.isPassed());   // true
        System.out.println(s2.isPassed());   // false
    }
}
```

### Breaking down `Student s1 = new Student();`

| Part | Meaning |
|------|---------|
| `Student` | type (like `int`, but ab custom type!) |
| `s1` | reference variable (Stack me, address slip) |
| `new` | Heap me memory allocate karo (DMA — note 02!) |
| `Student()` | constructor call (next note me detail!) |

### The dot `.` operator = "ka" (possession)
`s1.name` = "s1 **ka** name", `s1.introduce()` = "s1, apna introduce chalao!"

---

## 4. Memory picture (notes 02 & 06 connect ho rahi hain!)

```
        STACK                        HEAP
┌────────────────┐    ┌────────────────────────┐
│ main() frame:  │    │  Student object @101:  │
│  s1 = @101 ────┼───→│   name="Ashu" roll=1   │
│  s2 = @205 ────┼─┐  │   marks=88.5           │
│                │ │  ├────────────────────────┤
└────────────────┘ └─→│  Student object @205:  │
                      │   name="Rahul" roll=2  │
                      │   marks=35.0           │
                      └────────────────────────┘
```

- Har object ki **APNI copy** hoti hai fields ki (s1 ka name alag, s2 ka alag).
- Isliye inhe **instance variables** kehte hain — har instance (object) ke apne.
- Reference trap yahan bhi: `Student s3 = s1;` → s3 aur s1 SAME object (copy nahi!).

---

## 5. Local vs Instance variables (scope clear karo)

```java
class Student {
    String name;              // instance variable → Heap, har object ki apni
    // default value milti hai: null / 0 / false (bina set kiye bhi crash nahi)

    void study() {
        int hours = 3;        // local variable → Stack, method khatam = gone
        // default value NAHI milti — use se pehle set karna zaroori!
    }
}
```

| | Instance variable | Local variable |
|--|-------------------|----------------|
| Written | class ke andar, methods ke bahar | method ke andar |
| Memory | Heap (object ke saath) | Stack (frame ke saath) |
| Default value | milti hai (0, null, false) | NAHI milti |
| Life | jab tak object zinda | jab tak method chal raha |

---

## 6. Objects + Methods + Arrays combo (real power!)

```java
public class Main {
    public static void main(String[] args) {
        Student[] classroom = new Student[3];    // array OF objects!

        classroom[0] = makeStudent("Ashu", 1, 88.5);
        classroom[1] = makeStudent("Rahul", 2, 35.0);
        classroom[2] = makeStudent("Priya", 3, 92.0);

        // Topper nikaalo (note 06 ka max pattern — objects pe!)
        Student topper = classroom[0];
        for (int i = 1; i < classroom.length; i++) {
            if (classroom[i].marks > topper.marks) topper = classroom[i];
        }
        System.out.println("Topper: " + topper.name);   // Topper: Priya
    }

    static Student makeStudent(String name, int roll, double marks) {
        Student s = new Student();
        s.name = name; s.roll = roll; s.marks = marks;
        return s;      // methods can return objects too!
    }
}
```

💡 Dekha? **Ab tak ki SAB notes ek saath kaam kar rahi hain** — arrays (06) + loops (05) + methods (08) + objects (09). Yehi programming hai!

---

## 7. Common Beginner Mistakes ❌

1. Class use karne se pehle object banana bhool jaana:
   `Student s; s.name = "Ashu";` → ❌ error/null — `new Student()` zaroori!
2. `NullPointerException`: reference null hai aur tum `.field` access kar rahe ho — Java ki sabse famous error! Pehle object banao/check karo.
3. Sochna ki `Student s2 = s1;` se copy banti hai → nahi, same object ka doosra address slip.
4. Class name small letter me → chalega but WRONG convention. Classes = `PascalCase` (Student, BankAccount), variables/methods = `camelCase`.
5. Ek file me do public classes → ❌ ek file = ek public class (file name = class name).

---

## 8. Practice: predict the output (answers hidden)

```java
class Box {
    int value;
}

public class Main {
    public static void main(String[] args) {
        // Q1
        Box b1 = new Box();
        System.out.println(b1.value);

        // Q2
        Box b2 = new Box();
        b2.value = 10;
        Box b3 = b2;
        b3.value = 99;
        System.out.println(b2.value);

        // Q3
        Box b4 = null;
        System.out.println(b4.value);
    }
}
```

<details>
<summary>👉 Click for answers</summary>

- **Q1:** `0` — instance variables get default values (int → 0)
- **Q2:** `99` — b2 and b3 point to the SAME object!
- **Q3:** 💥 `NullPointerException` — null pe field access = crash

</details>

---

## 9. Quick Revision (30 seconds) ⚡

- **Class = mould/blueprint; Object = real cake** — ek class, kitne bhi objects.
- `new` → Heap me object; reference → Stack me address slip.
- `.` = "ka": `s1.name`, `s1.introduce()`.
- Instance variables: har object ki apni copy + default values milti hain.
- Local variables: method ke andar, default value NAHI.
- `ref2 = ref1` → same object, copy nahi.
- Null reference pe `.` lagaya → `NullPointerException`.

---

⬅️ **Previous:** [08 — Methods](08-methods.md) | ➡️ **Next:** 10 — OOP 2: Constructors, this, static (coming soon)
