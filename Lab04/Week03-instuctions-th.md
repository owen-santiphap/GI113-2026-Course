# Lab 4 — 4 หน้าจอเกม: Input + TryParse

**วิชา GI113 Computer Programming (GI)** · สัปดาห์ที่ 4 · เนื้อหา: `Console.ReadLine`, `Convert` vs `TryParse`, Input Validation

---

## 🗺️ ถ้าคุณไม่ได้เข้าคาบสัปดาห์ที่ 4

ทำตามนี้ก่อนเริ่ม Lab (repo เดิมของคุณจาก Lab 2/3 — ไม่ต้องสร้าง repo ใหม่):

1. เปิด GitHub Desktop → เลือก repo `GI113-2026-<รหัสนักศึกษา>` ของตัวเอง → กด **Fetch origin** แล้ว **Pull** เพื่อดึงงานล่าสุด
2. สร้าง Console App (C#) ชื่อโปรเจกต์ **`Lab04`** ไว้ในโฟลเดอร์ที่ clone มา (อย่าเอาไปใส่ข้างใน Lab ตัวอื่น เช่น Lab2/Lab03) — **ต้องติ๊ก "Place solution and project in the same directory" ก่อนกด Create**
3. วางเนื้อหาจาก `HEADER-TEMPLATE.txt` ไว้บรรทัดบนสุดของ `Program.cs` เหนือทุกอย่าง ก่อนเขียนโค้ดอะไรเพิ่ม
4. ถ้าจำ `TryParse` ไม่ได้ — ทวนสไลด์ Section 4 "TryParse — The Safe Way" ของ Week 4 (Slide 13-14) ก่อน เพราะ Lab นี้ใช้แนวคิดนั้นตรงๆ ทั้ง 4 หน้าจอ
5. ถ้าพลาดกิจกรรม Hands-On "Build a Character Creation Screen" (Slide 16) — โค้ดของหน้าจอนั้น**คือ Screen 1 ของ Lab นี้เป๊ะ** ดูสเปกเต็มที่ Screen 1 ด้านล่างแทนการเดา

---

## 🎯 วัตถุประสงค์

สร้างเกมจริงที่ถาม-ตอบกับผู้เล่นได้โดยไม่ล่ม — ฝึกอ่าน input ด้วย `Console.ReadLine()` แล้วแปลง/ตรวจสอบด้วย `int.TryParse` / `double.TryParse` ใน **4 หน้าจอเกมจริง** ที่รันต่อกันในโปรแกรมเดียว

Lab นี้ทำตามสเปกที่กำหนดเป๊ะทั้ง 4 หน้าจอ (ตรวจด้วยการเทียบผลลัพธ์แบบ diff ผ่าน 2 ชุด input — ไม่มีส่วนออกแบบอิสระ) **ไม่มี `if`/`else` หรือ loop เกี่ยวข้องเลย** (ยังไม่ได้สอนจนถึง Week 6/10) — ทุกหน้าจอแค่พิมพ์ข้อเท็จจริงสองอย่างออกมา (`bool` กับค่าที่แปลงได้) ไม่ตัดสินใจแตกเงื่อนไขเอง เหมือนที่ทำในคาบทุกกิจกรรม

---

## 📋 Screen 1 — Character Creation *(ทำสดในคาบแล้ว — Slide 16)*

**วัตถุประสงค์**: อ่านชื่อตัวละคร (`string`, ไม่มี TryParse เพราะข้อความรับได้ทุกแบบอยู่แล้ว) + เลือกคลาส (`int.TryParse`) + ค่าโชค (`double.TryParse`) แล้วพิมพ์สรุปตัวละคร

**โค้ด** (ถ้าทำ Hands-On ในคาบแล้ว คัดลอกของตัวเองมาวางได้เลย — โค้ดนี้คือตัวเดียวกัน):

```csharp
Console.WriteLine("+------------------------------+");
Console.WriteLine("|      CHARACTER CREATION       |");
Console.WriteLine("+------------------------------+");
Console.Write("Name your character: ");
string charName = Console.ReadLine();
Console.Write("Choose a class (1-3): ");
bool classOk = int.TryParse(Console.ReadLine(), out int classNum);
Console.Write("Starting luck (0.0-10.0): ");
bool luckOk = double.TryParse(Console.ReadLine(), out double luck);
Console.WriteLine($"{charName} the Class-{classNum} adventurer enters the dungeon. Luck: {luck}");
```

หมายเหตุ: `classOk` และ `luckOk` ประกาศไว้แต่ไม่ต้องพิมพ์ออกจอในหน้าจอนี้ (ต่างจาก Screen 2-4 ที่พิมพ์ `Valid input` ด้วย) — เพราะสเปกของหน้าจอนี้คือประโยคสรุปตัวละครหนึ่งบรรทัด ไม่ใช่รายงานผล validate ตรงๆ แบบหน้าจออื่น

---

## 📋 Screen 2 — Item Shop

**วัตถุประสงค์**: ถามจำนวนไอเทมที่จะซื้อ ตรวจด้วย `int.TryParse` แล้วรายงานผล — pattern เดียวกับ Item Shop demo ในคาบ (Slide 14)

```csharp
Console.WriteLine("+------------------------------+");
Console.WriteLine("|           ITEM SHOP           |");
Console.WriteLine("+------------------------------+");
Console.Write("How many potions? ");
bool quantityOk = int.TryParse(Console.ReadLine(), out int quantity);
Console.WriteLine($"Valid input: {quantityOk}");
Console.WriteLine($"Quantity: {quantity}");
```

---

## 📋 Screen 3 — Settings: Set Volume

**วัตถุประสงค์**: ถามค่าความดังเพลง ตรวจด้วย `double.TryParse` แล้วรายงานผล — pattern เดียวกับ Rate This Level demo ในคาบ (Slide 15)

```csharp
Console.WriteLine("+------------------------------+");
Console.WriteLine("|          SET VOLUME           |");
Console.WriteLine("+------------------------------+");
Console.Write("Set music volume (0.0-1.0): ");
bool volumeOk = double.TryParse(Console.ReadLine(), out double volume);
Console.WriteLine($"Valid input: {volumeOk}");
Console.WriteLine($"Volume: {volume}");
```

---

## 📋 Screen 4 — New Save File

**วัตถุประสงค์**: รวม 2 pattern เข้าด้วยกันเหมือน Screen 1 — อ่านชื่อเซฟ (`string`) แล้วถามช่อง save slot ตรวจด้วย `int.TryParse`

```csharp
Console.WriteLine("+------------------------------+");
Console.WriteLine("|         NEW SAVE FILE         |");
Console.WriteLine("+------------------------------+");
Console.Write("Enter save name: ");
string saveName = Console.ReadLine();
Console.Write("Choose save slot (1-3): ");
bool slotOk = int.TryParse(Console.ReadLine(), out int slot);
Console.WriteLine($"Save name: {saveName}");
Console.WriteLine($"Valid input: {slotOk}");
Console.WriteLine($"Slot: {slot}");
```

---

## 🔗 การรวม 4 หน้าจอ

ถ่าย Screenshot ให้ครบทั้ง 4 Sinarios ของการใช้ TryParse

---

## Test Cases

โปรแกรมรับ input ทีละบรรทัดต่อ 1 คำถาม (`Console.ReadLine()` ทั้งหมด 7 ครั้ง เรียงตามลำดับ Screen 1→4) — ตรวจด้วยการรันโปรแกรมจริงแล้วป้อน input ตามลำดับ แล้วเทียบผลลัพธ์ทั้งหมดแบบ diff ทุกตัวอักษร (**ทดสอบรันจริงแล้วทั้ง 2 เคส: 23 บรรทัด, บรรทัดว่าง 3 บรรทัด ต่อเคส**)

### Test Case 1 — Input ถูกทั้งหมด

| ลำดับ | คำถาม | พิมพ์ |
|---|---|---|
| 1 | Name your character: | `Rin` |
| 2 | Choose a class (1-3): | `2` |
| 3 | Starting luck (0.0-10.0): | `7.5` |
| 4 | How many potions? | `5` |
| 5 | Set music volume (0.0-1.0): | `0.75` |
| 6 | Enter save name: | `Aria` |
| 7 | Choose save slot (1-3): | `2` |

**Output ที่ต้องได้ (23 บรรทัด, บรรทัดว่าง 3 บรรทัด):**

```
+------------------------------+
|      CHARACTER CREATION       |
+------------------------------+
Name your character: Choose a class (1-3): Starting luck (0.0-10.0): Rin the Class-2 adventurer enters the dungeon. Luck: 7.5

+------------------------------+
|           ITEM SHOP           |
+------------------------------+
How many potions? Valid input: True
Quantity: 5

+------------------------------+
|          SET VOLUME           |
+------------------------------+
Set music volume (0.0-1.0): Valid input: True
Volume: 0.75

+------------------------------+
|         NEW SAVE FILE         |
+------------------------------+
Enter save name: Choose save slot (1-3): Save name: Aria
Valid input: True
Slot: 2
```

### Test Case 2 — Input ผิดปนอยู่ (ต้องไม่ crash!)

| ลำดับ | คำถาม | พิมพ์ |
|---|---|---|
| 1 | Name your character: | `Zed` |
| 2 | Choose a class (1-3): | `two` ← ผิด (ตัวหนังสือ ไม่ใช่ตัวเลข) |
| 3 | Starting luck (0.0-10.0): | `7.5` |
| 4 | How many potions? | `ten` ← ผิด |
| 5 | Set music volume (0.0-1.0): | `loud` ← ผิด |
| 6 | Enter save name: | `Echo` |
| 7 | Choose save slot (1-3): | `high` ← ผิด |

**Output ที่ต้องได้ (23 บรรทัด, บรรทัดว่าง 3 บรรทัด — เหมือนเคส 1 ทุกจุดยกเว้นค่าที่ผิด):**

```
+------------------------------+
|      CHARACTER CREATION       |
+------------------------------+
Name your character: Choose a class (1-3): Starting luck (0.0-10.0): Zed the Class-0 adventurer enters the dungeon. Luck: 7.5

+------------------------------+
|           ITEM SHOP           |
+------------------------------+
How many potions? Valid input: False
Quantity: 0

+------------------------------+
|          SET VOLUME           |
+------------------------------+
Set music volume (0.0-1.0): Valid input: False
Volume: 0

+------------------------------+
|         NEW SAVE FILE         |
+------------------------------+
Enter save name: Choose save slot (1-3): Save name: Echo
Valid input: False
Slot: 0
```

**สังเกต**: ทั้งที่ข้อ 2, 4, 5, 7 พิมพ์ผิด **โปรแกรมไม่ล่มสักจุดเดียว** — `classNum` กลายเป็น `0` เงียบๆ ตอนคลาสพิมพ์ผิด นี่คือ safety net ของ `TryParse` ที่เรียนในคาบ เทียบกับ `Convert.ToInt32` ที่จะทำให้ทั้งโปรแกรม crash ทันทีตรงจุดเดียวกัน

---

## Game Context

ทั้ง 4 หน้าจอคือของจริงที่เกมทุกแนวใช้: สร้างตัวละครตอนเริ่มเกม, ร้านค้าในเกม, หน้าตั้งค่าเสียง, และหน้าจอเซฟเกม — ทุกจุดที่ผู้เล่นพิมพ์อะไรเข้ามา โปรแกรมต้องรับมือกับคนที่พิมพ์ผิดได้โดยไม่ทำให้เกมปิดตัวกลางคัน

---

## Implementation Hint

```
// out int / out double ต้องประกาศชนิดตรงกับ TryParse ที่เรียก
// (int.TryParse ต้องคู่กับ out int, double.TryParse ต้องคู่กับ out double)
//
// Console.ReadLine() คืน string เสมอ — ต่อให้ผู้เล่นพิมพ์ตัวเลข ก็ต้องผ่าน TryParse
// ก่อนถึงจะเอาไปคำนวณเป็น int/double ได้จริง
//
// อย่าลืม Console.WriteLine(); (ว่างเปล่า) คั่นระหว่างหน้าจอ — ไม่ใช่ Console.WriteLine("");
// ทั้งสองแบบพิมพ์บรรทัดว่างเหมือนกัน แต่ใช้แบบไม่มีอะไรในวงเล็บให้สม่ำเสมอกับ Lab ที่ผ่านมา
//
// Screen 1 กับ Screen 4 มีการอ่าน string ด้วย Console.ReadLine() ตรงๆ (ไม่ผ่าน TryParse)
// เพราะชื่อตัวละคร/ชื่อเซฟรับได้ทุกข้อความอยู่แล้ว ไม่มีอะไรให้ validate
```

---

## 🧪 Try to Break It *(ไม่คิดคะแนน แต่ให้ทำก่อนส่ง)*

ทดสอบทั้ง 4 หน้าจอด้วย input ที่ผิดแบบอื่นๆ นอกจาก Test Case 2 ด้านบน — ลองตามนี้อย่างน้อย 3 แบบ (เลือกจากหมวดที่ต่างกันให้หลากหลายที่สุด ไม่ใช่ 3 แบบจากหมวดเดียว):

- **ว่างเปล่า**: กด Enter เฉยๆ ไม่พิมพ์อะไร ตอนถูกถามตัวเลข
- **มีช่องว่างรอบตัวเลข**: เช่น `"  5  "` ตอนถามจำนวนโพชั่น
- **ทศนิยมใส่ช่อง int**: เช่น `"2.5"` ตอนเลือกคลาส (1-3)
- **ตัวเลขใหญ่เกินไป**: เช่น `"99999999999"` ตอนเลือก save slot

ถ้าหน้าจอไหน **crash** ตอนเจอ input ผิด แปลว่า `TryParse` ยังต่อโค้ดไม่ถูก (อาจลืม `out` หรือใช้ `Convert` แทน) — กลับไปเช็คตามสเปกด้านบนอีกครั้งก่อนส่ง

---

## ✅ สิ่งที่ต้องส่ง

1. โปรเจกต์เดียว, `Program.cs` ไฟล์เดียว, ชื่อ `Lab04` — ทั้ง 4 หน้าจอรันเรียงต่อกันใน `Ctrl+F5` ครั้งเดียว
2. Header comment (Student ID / Name / Section / No.) อยู่บนสุด เหมือนทุก Lab ที่ผ่านมา
3. แต่ละหน้าจอ print header block ของตัวเองก่อน ("ITEM SHOP", "SET VOLUME", ...) ให้เห็นชัดว่าแยก 4 หน้าจอ
4. "Try to Break It" (ไม่คิดคะแนน แต่ให้ทำ): ทดสอบทุกหน้าจอด้วย input ที่ถูกและผิด ตามหมวดด้านบน — ถ้าหน้าจอไหน crash ตอน input ผิด แปลว่า `TryParse` ยังต่อไม่ถูก
5. Commit ด้วยข้อความที่สื่อความหมายจริง (ห้ามใช้คำว่า `"update"`) push ขึ้น repo `GI113-2026-<รหัสนักศึกษา>` ของตัวเอง โพสต์ลิงก์ commit ใน Teams พร้อมแนบ screenshot ที่รันครบทั้ง 4 หน้าจอ (เห็น Console ตั้งแต่ Character Creation ถึง New Save File)

---

## 💡 คำแนะนำ

- ตั้งชื่อ Solution/Project ว่า `Lab04` (PascalCase) — สคริปต์ตรวจงานเช็คชื่อนี้ ตั้งผิดรูปแบบหักคะแนนแม้โค้ดถูก
- ใช้ `Ctrl+F5` (ไม่ใช่ `F5`) รันโปรแกรม ไม่งั้นหน้าต่าง console จะปิดทันทีก่อนอ่านผลลัพธ์ทัน
- เวลาทดสอบเอง อย่าลืมว่าต้องพิมพ์ครบ **7 ค่า** ตามลำดับ (ชื่อ, คลาส, โชค, จำนวนโพชั่น, ระดับเสียง, ชื่อเซฟ, ช่องเซฟ) — พิมพ์ไม่ครบโปรแกรมจะค้างรอ input ต่อ ไม่ใช่ error
- ถ้า `Valid input` ออกมา `False` ทั้งที่พิมพ์ตัวเลขถูกแล้ว — เช็คว่าใช้ `int.TryParse` ตรงกับ `double.TryParse` ถูกหน้าจอหรือไม่ (Screen 2/4 ใช้ `int`, Screen 3 ใช้ `double`)
- `Console.WriteLine();` (ไม่มีอะไรในวงเล็บ) ใช้พิมพ์บรรทัดว่างได้ ไม่ต้องใส่ `""`
