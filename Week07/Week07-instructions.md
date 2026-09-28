# Lab 7: Battle Command Menu

**GI113 Computer Programming (GI)** · สัปดาห์ที่ 7 · เนื้อหา: `switch` statement, switch expression, relational patterns, ternary `? :`

---

## 🎯 วัตถุประสงค์

สร้างเมนูต่อสู้ Hero vs Slime แบบ 1 ตา: ผู้เล่นเลือกคำสั่ง แล้วโปรแกรมตัดสินว่าเกิดอะไรขึ้น โดยใช้เครื่องมือตัดสินใจทั้ง 4 แบบที่เรียนสัปดาห์นี้ครบทุกแบบ
**Part A** (ขั้นที่ 1–6) ทุกคนเขียนเหมือนกัน · **Part B** เพิ่มคำสั่งที่ 5 ที่ออกแบบเอง

**เตรียมโปรเจกต์**: Console App ชื่อ **`Lab07`** ใน repo `GI113-2026-<รหัสนักศึกษา>` (ติ๊ก "Place solution and project in the same directory") · วาง `HEADER-TEMPLATE.txt` ไว้บนสุดของ `Program.cs` แล้วกรอกให้ครบ

**กติกา**: ทุก `switch` ต้องมี `default` · ทุก switch expression ต้องจบด้วย `_` · ข้อความใน Console เป็นภาษาอังกฤษ · ไม่ใช้ loop

> ⚠️ ถ้า Visual Studio ขีดเส้นใต้ `Console.ReadLine()` แล้วขึ้น **warning CS8600** ปล่อยไว้ได้เลย warning ไม่ใช่ error โปรแกรมยัง build และรันได้ตามปกติ

**รันทุกครั้งที่เขียนจบแต่ละขั้น** แต่ละขั้นจะพิมพ์บรรทัดของตัวเองออกมาทันที ถ้าบรรทัดไหนผิดจะรู้ได้ตรงนั้นเลย

---

## Part A

### Step 1: ตั้งค่าการต่อสู้

`MonsterHp` เป็น `const` เพราะค่านี้ไม่เปลี่ยน (Week 3) ส่วนค่า Defense ให้ผู้เล่นพิมพ์ แล้วแปลงด้วย `TryParse` (Week 4) ถ้าพิมพ์ผิด ค่าจะเป็น `0`

```csharp
const int MonsterHp = 10;

Console.Write("Monster Defense: ");
int.TryParse(Console.ReadLine(), out int monsterDefense);
Console.WriteLine($"A Slime appears! HP {MonsterHp}, DEF {monsterDefense}");
```

### Step 2: เมนูและ `switch` statement

เอาค่าเดียว (`command`) มาเลือกว่าจะ**ทำ**อะไร ทุก section ต้องจบด้วย `break;` ถ้าลืม C# จะไม่ยอม build (error CS0163) · ถ้าพิมพ์ `abc` แล้ว TryParse ไม่ผ่าน `command` จะเป็น `0` ซึ่งไม่ตรงกับ case ไหน โปรแกรมจึงไปเข้า `default`

```csharp
Console.WriteLine("=== BATTLE MENU ===");
Console.WriteLine("1) Attack");
Console.WriteLine("2) Fire Magic");
Console.WriteLine("3) Defend");
Console.WriteLine("4) Run");
Console.Write("Choose (1-4): ");
int.TryParse(Console.ReadLine(), out int command);

switch (command)
{
    case 1:
        Console.WriteLine("Hero swings the sword!");
        break;
    case 2:
        Console.WriteLine("Hero casts Fire!");
        break;
    case 3:
        Console.WriteLine("Hero raises the shield.");
        break;
    case 4:
        Console.WriteLine("Hero looks for a way out...");
        break;
    default:
        Console.WriteLine("Hero hesitates. Invalid command!");
        break;
}
```

### Step 3: พลังโจมตีด้วย switch expression

ถ้าทุก case แค่**เลือกค่า** ให้ใช้ switch expression ได้เลย อ่าน `=>` ว่า "ได้ค่า" ส่วน `_` จะจับทุกค่าที่เหลือ (คำสั่ง 3, 4 และคำสั่งที่ไม่ถูกต้อง จะได้ power 0) `Math.Max(0, ...)` ใส่ไว้กันไม่ให้ดาเมจติดลบ (Week 5)

```csharp
int power = command switch
{
    1 => 12,
    2 => 18,
    _ => 0
};
int damage = Math.Max(0, power - monsterDefense);
Console.WriteLine($"Damage: {damage}");
```

### Step 4: ให้เกรดการโจมตีด้วย relational patterns

switch expression ใช้กับ**ช่วงค่า**ได้ ตรวจจากบนลงล่าง arm แรกที่ตรงจะเป็นผู้ชนะ (กติกาเดียวกับ `else if` ใน Week 6) ถ้าเรียงผิด เช่น เอา `>= 5` ไว้ก่อน `>= 12` C# จะไม่ยอม build (error CS8510)

```csharp
string rating = damage switch
{
    >= 12 => "Critical hit!",
    >= 5 => "Solid hit.",
    > 0 => "Scratch.",
    _ => "No damage."
};
Console.WriteLine($"Rating: {rating}");
```

### Step 5: Slime ล้มหรือยัง? (ternary)

ใช้เมื่อมีคำถามเดียวที่ตอบได้แค่ใช่/ไม่ใช่ แล้วต้องเลือกค่า 1 ใน 2 ค่า ทั้งสองฝั่งของ `:` ต้องเป็น type เดียวกัน

```csharp
string monsterStatus = damage >= MonsterHp ? "DEFEATED" : "still standing";
Console.WriteLine($"Slime: {monsterStatus}");
```

### Step 6: หนีจริงไหม? (หลาย label ใน section เดียว)

`switch` ใช้กับ `string` ได้ และหลาย `case` ใช้ section เดียวกันได้ ถ้าวางซ้อนกันโดยไม่มีโค้ดคั่นกลาง · การเทียบ string ต้องตรงทุกตัวอักษร ดังนั้น `"yes"` ไม่เท่ากับ `"y"`

```csharp
Console.Write("Really run away? (y/n): ");
string answer = Console.ReadLine();

switch (answer)
{
    case "y":
    case "Y":
        Console.WriteLine("You escaped!");
        break;
    case "n":
    case "N":
        Console.WriteLine("You stay and fight.");
        break;
    default:
        Console.WriteLine("Please type y or n.");
        break;
}
```

### ตัวอย่างผลลัพธ์เมื่อทำ Part A ครบ

พิมพ์ `5` แล้ว `2` แล้ว `y`:

```
Monster Defense: 5
A Slime appears! HP 10, DEF 5
=== BATTLE MENU ===
1) Attack
2) Fire Magic
3) Defend
4) Run
Choose (1-4): 2
Hero casts Fire!
Damage: 13
Rating: Critical hit!
Slime: DEFEATED
Really run away? (y/n): y
You escaped!
```

### เช็กตัวเองก่อนส่ง

ลองรันทุกแถว ผลต้องตรงกับตาราง (ทุกแถวมาจากการรันจริง)

| Defense | Command | y/n | Damage | Rating | Slime | บรรทัดสุดท้าย |
|---|---|---|---|---|---|---|
| `5` | `1` | `N` | 7 | Solid hit. | still standing | You stay and fight. |
| `10` | `1` | `Y` | 2 | Scratch. | still standing | You escaped! |
| `8` | `2` | `Y` | 10 | Solid hit. | DEFEATED | You escaped! |
| `20` | `2` | `x` | 0 | No damage. | still standing | Please type y or n. |
| `5` | `abc` | `n` | 0 | No damage. | still standing | You stay and fight. |

แถว `8 / 2` คือค่าที่อยู่ตรงขอบพอดี: damage 10 เท่ากับ HP 10 พอดี `>=` จึงเป็น true ส่วน `abc` จะพิมพ์ `Hero hesitates. Invalid command!` เพราะไปเข้า `default`

---

## Part B: คำสั่งที่ 5 เพิ่มของตัวเอง

คิดคำสั่งใหม่ขึ้นมาเอง 1 คำสั่ง จะตั้งชื่ออะไรก็ได้ พลังเท่าไรก็ได้ (เช่น Ice Spear, Steal, Heal) แล้วเพิ่มเข้าไปให้ครบ **ทั้ง 3 ที่**:

1. **เมนู**: เพิ่มบรรทัด `5) ...` และเปลี่ยน prompt เป็น `Choose (1-5): `
2. **`switch` statement** (ขั้นที่ 2): เพิ่ม `case 5:` ที่พิมพ์ข้อความการกระทำของคุณ ไว้ก่อน `default`
3. **switch expression** (ขั้นที่ 3): เพิ่ม arm `5 => <พลังของคุณ>,` ไว้ก่อน `_`

ถ้าเพิ่มครบ 3 ที่ เลือก `5` แล้วต้องได้ข้อความของคุณ ได้ Damage จากพลังที่ตั้งไว้ และขั้นที่ 4–6 ต้องทำงานต่อได้ตามปกติ · ส่วนคำสั่ง 1–4 ต้องได้ผลเหมือนตารางด้านบนทุกอย่าง

---

## 📤 ส่งงาน

1. **Commit** พร้อมข้อความที่บอกได้ว่าทำอะไร (เช่น `Lab07: battle menu with switch and Ice Spear`)
2. **Push** ขึ้น GitHub ผ่าน GitHub Desktop
3. ส่งใน Teams: **ลิงก์ commit** (ถ้ายังไม่เคยส่ง) + **screenshot Console** 1 รูปที่เลือกคำสั่งที่ 5 ที่ตั้งขึ้นมาใหม่

---

# Rubric

## Rubric Title

```
Lab 7: Battle Command Menu
```

## Rubric Description

```
5 เกณฑ์ เกณฑ์ละ 1 คะแนน รวม 5 คะแนน
ตรวจจากโค้ดที่ push และจากการรันจริงด้วย input ชุดเดียวกับตาราง "เช็กตัวเองก่อนส่ง" ในบรีฟ
```

## เกณฑ์ทั้ง 5

### 1 · switch statement: เมนูและการหนี (ขั้นที่ 1, 2, 6), เต็ม 1

| คะแนน | ทำถึงระดับนี้ |
|---|---|
| **1** | ใช้ `switch` statement ทั้งเมนูคำสั่งและคำถาม y/n ครบทุก case มี `default` และ `break` · บรรทัด `A Slime appears!`, ข้อความการกระทำ และบรรทัดสุดท้ายถูกต้องทุก input (รวม `abc`, `yes`, `x`) |
| **0.5** | ผลลัพธ์ถูกเกือบทั้งหมด แต่ผิดอยู่ 1–2 กรณี (เช่น ไม่รับ `Y` ตัวใหญ่) หรือใช้ `if` แทน `switch` ในจุดใดจุดหนึ่ง |
| **0** | ไม่มี `switch` statement หรือผลลัพธ์ผิดเกินครึ่ง |

### 2 · switch expression, relational patterns และ ternary (ขั้นที่ 3, 4, 5), เต็ม 1

| คะแนน | ทำถึงระดับนี้ |
|---|---|
| **1** | `power` ได้มาจาก switch expression ที่จบด้วย `_` · `rating` ใช้ relational patterns (`>=`, `>`) · `monsterStatus` ใช้ ternary · บรรทัด `Damage`, `Rating`, `Slime` ถูกต้องทุก input รวมค่าที่ขอบ (Defense 8 + Fire ต้องได้ `DEFEATED`) |
| **0.5** | ผลลัพธ์ถูก แต่ขั้นใดขั้นหนึ่งไม่ได้ใช้เครื่องมือที่กำหนด (เช่น ใช้ `if` แทน ternary) หรือผิดอยู่ 1 บรรทัดในบางกรณี |
| **0** | ผลลัพธ์ผิดเกินครึ่ง หรือไม่มี switch expression เลย |

### 3 · Part B: คำสั่งที่ 5 ของตัวเอง, เต็ม 1

| คะแนน | ทำถึงระดับนี้ |
|---|---|
| **1** | เพิ่มคำสั่งที่ 5 ครบทั้ง 3 ที่ (บรรทัดเมนู + prompt `(1-5)`, `case 5:`, arm `5 =>`) · เลือก 5 แล้วได้ข้อความของตัวเองและ Damage ตามพลังที่ตั้งไว้ · คำสั่ง 1–4 ยังทำงานเหมือนเดิม |
| **0.5** | เพิ่มแล้วแต่ไม่ครบ 3 ที่ (เช่น ลืม arm ใน switch expression ทำให้ Damage เป็น 0 หรือลืมบรรทัดในเมนู) |
| **0** | ไม่มี Part B |

### 4 · Naming Convention & Header, เต็ม 1

| คะแนน | ทำถึงระดับนี้ |
|---|---|
| **1** | ชื่อโปรเจกต์เป็น `Lab07` (PascalCase) · header comment ครบ (รหัสนักศึกษา / ชื่อ / Section / เลขที่) · `MonsterHp` เป็น `const` PascalCase และตัวแปรอื่นเป็น camelCase |
| **0.5** | ชื่อโปรเจกต์ผิดเล็กน้อย หรือ header กรอกไม่ครบ |
| **0** | ไม่มี header comment หรือชื่อโปรเจกต์ไม่ใช่ `Lab07` |

### 5 · Commit, Push & Screenshot, เต็ม 1

| คะแนน | ทำถึงระดับนี้ |
|---|---|
| **1** | commit message มีความหมาย · push ขึ้น repo ของตัวเองถูกต้อง · ลิงก์เปิดได้ · screenshot แสดงรอบที่เลือกคำสั่งที่ 5 |
| **0.5** | commit message กว้างเกินไป (`update`, `fix`) หรือ screenshot ไม่ได้แสดงคำสั่งที่ 5 |
| **0** | ไม่ได้ push, ลิงก์เปิดไม่ได้, หรือไม่มี screenshot |