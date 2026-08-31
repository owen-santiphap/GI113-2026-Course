# Lab 3 — Kirin's Save Converter

**วิชา GI113 Computer Programming (GI)** · สัปดาห์ที่ 3 · เนื้อหา: Type Conversion (Implicit / Explicit Cast / Convert), `var`, `const`, ข้อควรระวังการหารจำนวนเต็ม

---

## 🗺️ ถ้าคุณไม่ได้เข้าคาบสัปดาห์ที่ 3

ทำตามนี้ก่อนเริ่ม Lab (repo เดิมของคุณจาก Lab 2 — ไม่ต้องสร้าง repo ใหม่):

1. เปิด GitHub Desktop → เลือก repo `GI113-2026-<รหัสนักศึกษา>` ของตัวเอง → กด **Fetch origin** แล้ว **Pull** เพื่อดึงงานล่าสุด
2. สร้าง Console App (C#) ชื่อโปรเจกต์ **`Lab03`** ไว้ในโฟลเดอร์ที่ clone มา (โฟลเดอร์เดียวกับที่มี `Lab02` อยู่ แต่คนละโฟลเดอร์ย่อย) — **ต้องติ๊ก "Place solution and project in the same directory" ก่อนกด Create**
3. วางเนื้อหาจาก `HEADER-TEMPLATE.txt` ไว้บรรทัดบนสุดของ `Program.cs` เหนือ `using System;` ก่อนเขียนโค้ดอะไรเพิ่ม
4. ถ้าจำเนื้อหาปริศนา "HP Percent 72% หรือ 0%" จาก Week 2/Lab 2 ไม่ได้ — ทวนสไลด์ Section 3 ของ Week 3 ก่อน เพราะ Lab นี้ใช้ความเข้าใจนั้นต่อ

---

## 🎯 วัตถุประสงค์

ต่อเนื่องจาก Lab 2: Kirin โดนโจมตีไปแล้วเหลือ HP 115/240 — Lab นี้ฝึกแปลงชนิดข้อมูลของ Kirin ให้พร้อมใช้งานในระบบอื่น (Implicit Conversion, Explicit Cast, `Convert.ToXxx()`), ประกาศตัวแปรด้วย `var`/`const` ให้ถูกกฎ, และแก้กับดัก `int` หารกันแล้วปัดเศษทิ้งที่ค้างมาจาก Week 2 ให้ได้เปอร์เซ็นต์ที่เป็นทศนิยมจริง

Lab นี้ทำตามสเปกที่กำหนดเป๊ะจุดเดียว (ตรวจด้วยการเทียบผลลัพธ์แบบ diff) — ไม่มีส่วนออกแบบอิสระ

---

## 📋 Kirin's Save Converter

**วัตถุประสงค์**

แปลงค่าต่างๆ ของ Kirin (ที่เก็บเป็น `int`/`float`/`double` อยู่แล้ว) ให้พร้อมใช้ในระบบเซฟเกม/UI ที่ต้องการชนิดข้อมูลต่างจากที่เก็บไว้ตอนแรก — ฝึก Implicit Conversion, Explicit Cast และ `Convert.ToInt32` ในสถานการณ์เดียวกัน เพื่อให้เห็นความต่างของทั้ง 3 แบบชัดๆ

**Variables** (ประกาศด้วยชื่อ/ชนิด (หรือ `var` ตามที่กำหนด) และค่าตามนี้เป๊ะ — ห้ามเปลี่ยน เพราะสคริปต์ตรวจงานจะเทียบผลลัพธ์แบบ diff):

```csharp
const int MaxLevel = 10;

var bossName = "Kirin";   // ต้องประกาศด้วย var ห้ามเขียน string ตรงๆ
var rank = 'S';            // ต้องประกาศด้วย var ห้ามเขียน char ตรงๆ
int level = 7;
int maxHp = 240;
int currentHp = 115;       // ค่าตั้งต้นของ Lab นี้คือ HP "หลังโดนโจมตี" จาก Lab 2 แล้ว ไม่ใช่ 175
float attackPower = 42.5f;
double critMultiplier = 1.75;
bool isBoss = true;
```

**Logic ที่ต้อง implement**

1. พิมพ์หัวข้อ `===== KIRIN SAVE CONVERTER =====`
2. พิมพ์ค่าตัวแปรทั้ง 7 บรรทัดตามลำดับใน Test Cases ด้านล่าง (บรรทัด Level ต้องโชว์คู่กับ `MaxLevel` แบบ `Level: 7 / 10`, บรรทัด HP โชว์คู่กับ `maxHp` แบบ `HP: 115 / 240`)
3. พิมพ์บรรทัดว่าง 1 บรรทัด
4. พิมพ์ `----- Implicit Conversion: HP as double -----`
5. แปลง `currentHp` (`int`) เป็น `double` แบบ **implicit** เก็บใส่ตัวแปรชื่อ `currentHpDouble` — **ห้ามใช้ `(double)` cast** ต้องปล่อยให้ compiler แปลงให้เองเฉยๆ
6. พิมพ์ `HP (double): {currentHpDouble}`
7. พิมพ์บรรทัดว่าง 1 บรรทัด
8. พิมพ์ `----- Exact HP Percent (no integer truncation) -----`
9. คำนวณตัวแปร `double` ชื่อ `hpPercentExact` ด้วยสูตร **`currentHpDouble * 100 / maxHp`** (ต้องใช้ `currentHpDouble` ที่แปลงไว้แล้วในข้อ 5 ห้ามใช้ `currentHp` ตรงๆ)
10. พิมพ์ `HP Percent (exact): {hpPercentExact}%`
11. พิมพ์บรรทัดว่าง 1 บรรทัด
12. พิมพ์ `----- Explicit Cast: Attack Power -> Display Int -----`
13. cast `attackPower` (`float`) เป็น `int` ด้วย `(int)` เก็บใส่ตัวแปรชื่อ `attackDisplay`
14. พิมพ์ `Attack Power (int cast): {attackDisplay}`
15. พิมพ์บรรทัดว่าง 1 บรรทัด
16. พิมพ์ `----- Cast vs Convert: Crit Multiplier -----`
17. แปลง `critMultiplier` เป็น `int` **สองวิธีคู่กัน**: `(int)critMultiplier` เก็บใส่ `critCast`, และ `Convert.ToInt32(critMultiplier)` เก็บใส่ `critConvert`
18. พิมพ์ `Crit Multiplier (int cast): {critCast}`
19. พิมพ์ `Crit Multiplier (Convert rounded): {critConvert}`

กติกา: ทุกบรรทัดที่มีตัวแปรอยู่ในข้อความ ต้องพิมพ์ด้วย string interpolation (`$"..."`) เท่านั้น ห้ามใช้เครื่องหมาย `+` ต่อสตริง

**Test Cases**

Lab นี้ไม่มี input ที่เปลี่ยนค่าได้ — ใช้ตัวแปรคงที่ด้านบนเสมอ และตรวจด้วยการเทียบผลลัพธ์ทั้งโปรแกรมแบบ diff ไม่ใช่ทีละ test case:

| # | เงื่อนไข | Output ที่ต้องได้ |
|---|---|---|
| 1 | รันด้วยค่าตัวแปรตั้งต้นตามด้านบน | ผลลัพธ์ตรงกับบล็อกด้านล่างทุกตัวอักษร รวมบรรทัดว่าง (ทดสอบรันจริงแล้ว: 21 บรรทัด, บรรทัดว่าง 4 บรรทัด) |

```
===== KIRIN SAVE CONVERTER =====
Name: Kirin
Rank: S
Level: 7 / 10
HP: 115 / 240
Attack Power: 42.5
Crit Multiplier: 1.75
Is Boss: True

----- Implicit Conversion: HP as double -----
HP (double): 115

----- Exact HP Percent (no integer truncation) -----
HP Percent (exact): 47.916666666666664%

----- Explicit Cast: Attack Power -> Display Int -----
Attack Power (int cast): 42

----- Cast vs Convert: Crit Multiplier -----
Crit Multiplier (int cast): 1
Crit Multiplier (Convert rounded): 2
```

**Game Context**

ระบบเซฟเกม/UI จริงต้องแปลงชนิดข้อมูลไปมาแบบนี้ตลอด — ค่าที่เก็บในตัวละคร (`int` HP, `float` attack) มักต้องแปลงเป็น `double` เพื่อคำนวณละเอียด (เช่น เปอร์เซ็นต์สำหรับ health bar) หรือแปลงกลับเป็น `int` เพื่อแสดงผลบนจอ (star rating, ตัวเลขจำนวนเต็มบน UI)

**Implementation Hint**

```
// currentHpDouble ต้องมาจาก currentHp แบบ "implicit" ล้วนๆ — เขียนแค่
// double currentHpDouble = currentHp;  ไม่ต้องมี (double) นำหน้าเลย
//
// ถ้าคำนวณ hpPercentExact จาก currentHp (int) ตรงๆ โดยไม่ผ่าน currentHpDouble ก่อน
// จะเจอกับดัก int/int=int แบบ Week 2 อีกรอบ (ได้ 47 จำนวนเต็ม ไม่ใช่ 47.916666666666664)
//
// (int)critMultiplier ตัดเศษทิ้งเสมอ ได้ 1 ไม่ใช่ 2 — คนละอย่างกับ Convert.ToInt32
// ที่ปัดเศษ (1.75 ปัดขึ้นเป็น 2) ทั้งสองค่านี้ต้องไม่เท่ากันถ้าทำถูก
//
// bossName และ rank ต้องประกาศด้วย var เป๊ะๆ (ไม่ใช่ string/char ตรงๆ) —
// สคริปต์ตรวจงานจะอ่าน source code เช็คด้วย ไม่ใช่แค่เช็ค output
```

---

## ✅ สิ่งที่ต้องส่ง

1. **Header comment** (Student ID / Name / Section / No.) อยู่บรรทัดบนสุดของ `Program.cs` เหนือ `using System;`
2. ผลลัพธ์ตรงกับ Test Case ด้านบนทุกตัวอักษร (diff เป๊ะ)
3. ทุกบรรทัดที่พิมพ์ค่าตัวแปรใช้ string interpolation
4. `bossName` และ `rank` ต้องประกาศด้วย `var` ตามสเปก
5. Commit ด้วยข้อความที่สื่อความหมายจริง (ห้ามใช้คำว่า `"update"`) แล้ว push ขึ้น repo `GI113-2026-<รหัสนักศึกษา>` ของตัวเอง
6. วางลิงก์ commit ใน Teams ตามช่องที่กำหนด — **ลิงก์นี้คือสิ่งที่ใช้ตรวจ** ไม่ใช่ตัวไฟล์

---

## 💡 คำแนะนำ

- ตั้งชื่อ Solution/Project ว่า `Lab03` (PascalCase) — สคริปต์ตรวจงานเช็คชื่อนี้ ตั้งผิดรูปแบบหักคะแนนแม้โค้ดถูก
- ใช้ `Ctrl+F5` (ไม่ใช่ `F5`) รันโปรแกรม ไม่งั้นหน้าต่าง console จะปิดทันทีก่อนอ่านผลลัพธ์ทัน
- ถ้า `HP Percent (exact)` ออกมาเป็นจำนวนเต็มไม่มีทศนิยม (เช่น `47%` แทนที่จะเป็น `47.916666666666664%`) แปลว่ายังคำนวณจาก `currentHp` (`int`) ตรงๆ ไม่ได้ผ่าน `currentHpDouble` ก่อน — กลับไปเช็คข้อ 5 อีกครั้ง กับดักนี้คือปริศนาที่ค้างมาจาก Week 2/Lab 2 นั่นเอง
- `(int)ค่า` ตัดเศษทิ้งเสมอ ส่วน `Convert.ToInt32(ค่า)` ปัดเศษ — สองค่านี้ควรไม่เท่ากันถ้าเขียนถูก (ดู Cast vs Convert ในสไลด์ Section 1)
- `Console.WriteLine();` (ไม่มีอะไรในวงเล็บ) ใช้พิมพ์บรรทัดว่างได้ ไม่ต้องใส่ `""`
