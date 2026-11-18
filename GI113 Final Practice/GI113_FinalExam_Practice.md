# GI113 แบบฝึกหัดเตรียมสอบ Final Exam (Programming)

แบบฝึกหัดนี้มี 3 ชุด (Final Programming #1–#3) ชุดละ 2 ข้อ ใช้ format เดียวกับข้อสอบ Final Exam ภาคปฏิบัติปีนี้ โดยข้อ 1 ใช้ Array กับ Loop ส่วนข้อ 2 ใช้ Method

## วิธีใช้

1. อ่านข้อกำหนดทีละข้อจากบนลงล่าง ข้อกำหนดเรียงตามลำดับที่ควรเขียนโปรแกรม ทำเสร็จทีละข้อแล้วค่อยไปข้อถัดไป
2. เทียบผลลัพธ์ที่รันกับตัวอย่างผลลัพธ์ใต้โจทย์แต่ละข้อ รูปแบบข้อความที่แสดงบนจอควรเหมือนตัวอย่าง
3. ตรวจเงื่อนไขที่ทำให้ไม่ได้คะแนนก่อนส่ง: ข้อที่ระบุว่าต้องใช้ Loop ต้องมี Loop และข้อ Method ต้องมี Method (ไม่มี Method = ไม่ได้คะแนน)
4. ส่งไฟล์ `Program.cs` และภาพ screenshot ผลลัพธ์การรันโปรแกรม

ตัวอย่างโค้ดเฉลยของ Final Programming #3 อยู่ท้ายเอกสาร ลองทำเองให้เสร็จก่อนแล้วค่อยเทียบ

---

## Final Programming #1

### ข้อ 1 — Array: ราคาไอเท็ม

เขียนโปรแกรมรับค่าราคา Item 3 ชิ้น (ชนิดจำนวนเต็ม) เก็บลง Array แล้วหาผลรวมราคาทั้งหมด และแสดงผลลัพธ์ทาง Console

1. แสดงข้อความขอรับราคาของแต่ละชิ้นตามลำดับ โดยข้อความและค่าที่พิมพ์อยู่ในบรรทัดเดียวกัน
2. เก็บราคาแต่ละชิ้นลง Array
3. หาผลรวมราคาทุกชิ้น
4. แสดงราคารวม (Total Price) ตามตัวอย่าง

ตัวอย่างผลลัพธ์:

```text
Enter price for potion 1: 10
Enter price for potion 2: 20
Enter price for potion 3: 30
Total Price: 60
```

### ข้อ 2 — Method: เพิ่มพลังชีวิต (Heal)

เขียนโปรแกรมสำหรับเพิ่มค่าพลังชีวิต (Heal) ของผู้เล่น โดยมีข้อกำหนดดังนี้

1. ผู้เล่นมีค่าพลังชีวิต
2. ค่าพลังชีวิตมีค่าสูงสุด 100
3. สร้าง method สำหรับเพิ่มค่าพลังชีวิตให้ผู้เล่น โดย
    - method รับ parameter คือ ค่าพลังชีวิตที่จะเพิ่มขึ้น (ชนิด integer)
    - method ต้องคืนค่าผลลัพธ์ (return value) เป็นค่าพลังชีวิตหลังการเพิ่มแล้ว
    - method ต้องตรวจว่าค่าพลังชีวิตหลังเพิ่มแล้ว _ไม่เกิน_ ค่าสูงสุดที่กำหนด ถ้าเกิน ให้ปัดเป็นค่าพลังชีวิตสูงสุด
4. ทดสอบใน Main 2 แบบ
    - แบบที่ 1: หลังเพิ่มแล้ว ค่าพลังชีวิต _ไม่เกิน_ ค่าสูงสุด
    - แบบที่ 2: หลังเพิ่มแล้ว ค่าพลังชีวิต _เกิน_ ค่าสูงสุด
5. ใน Main แสดงผลลัพธ์ทาง Console (ดูตัวอย่าง)

**หากเขียนโปรแกรมแบบไม่มี Method จะไม่ได้คะแนน**

ตัวอย่างผลลัพธ์ (แบบที่ 1):

```text
Current HP: 50, Heal Amount: 20
HP After Heal: 70
```

> **การส่ง** ส่งไฟล์ `Program.cs` และภาพ screenshot ผลลัพธ์การรันโปรแกรมทั้งสองแบบดังกล่าวข้างต้น

---

## Final Programming #2

### ข้อ 1 — Array: คะแนนเฉลี่ย

จงเขียนโปรแกรมรับคะแนนสอบของนักเรียน 3 คน เก็บลง Array แล้วหาค่าเฉลี่ย

1. ประกาศตัวแปรเป็น Array ตัวเลข มี length เป็น 3
2. ใช้ Loop รับค่าคะแนนจากผู้ใช้เก็บลง Array ให้ครบ
3. ประกาศตัวแปรรับผลรวมคะแนนจาก Array
4. คำนวณและแสดงผลค่าเฉลี่ย (Average = ผลรวม / จำนวนข้อมูล) ออกทาง Console

**หากไม่ได้ใช้ Loop จะไม่มีคะแนน**

ตัวอย่างผลลัพธ์:

```text
Enter score for student 1: 1
Enter score for student 2: 2
Enter score for student 3: 3
Average Score: 2
```

### ข้อ 2 — Method with return value: สร้างตัวละคร

เขียนโปรแกรมสร้างตัวละคร โดยผู้เล่นสามารถกำหนดคลาสและ stats ได้ โดยใช้ Method with return value

1. สร้าง **method** ที่ **return** เป็น **string** ข้อความ
2. กำหนดให้ method มี **parameters** เก็บ อักษรตัวละคร (**char**), ความฉลาด, ความแข็งแกร่ง, ความคล่องแคล่ว
3. เช็คเงื่อนไขจากอักษรตัวละครว่าตัวอักษรที่ได้ _ตรงกับชื่อคลาส_ อะไรบ้าง (กำหนดตัวอักษรคลาส เช่น A, B, C ตามลำดับ และตั้งชื่อ 2 คลาสขึ้นไป)
4. แต่ละคลาสชื่อต้องไม่ซ้ำ และแต่ละคลาสจะได้โบนัสค่า **stats** ไม่เหมือนกัน โดยเพิ่มด้วย `+` หรือ `*` ก็ได้ ขนาดโบนัสกำหนดเอง (ตัวอย่างด้านล่าง: คลาส Warrior ได้ +50 Strength)
5. แสดงผลลัพธ์ (Console)
6. เมื่อเจอ **char** ที่ไม่มีคลาสรองรับ ให้แสดงข้อความว่าไม่พบชื่อคลาสที่เลือก
7. เรียก **method** แสดงชื่อคลาส, โบนัส, และ **stats** ให้ถูกต้องหลังจากประมวลผลให้ method

**หากเขียนโปรแกรมแบบไม่มี Method จะไม่ได้คะแนน**

ตัวอย่างผลลัพธ์ (เรียก method ด้วยอักษรของ Warrior และ stats เริ่มต้น Intelligence 10, Strength 10, Dexterity 10):

```text
Bonus: +50 Strength
Class: Warrior, Intelligence: 10, Strength: 60, Dexterity: 10
```

> **การส่ง** ส่งไฟล์ `Program.cs` และภาพ screenshot ผลลัพธ์การรันโปรแกรมดังกล่าวข้างต้น

---

## Final Programming #3

### ข้อ 1 — Array: เวลาที่น้อยที่สุด

เขียนโปรแกรมรับค่า "เวลาที่ผู้เล่นทำภารกิจ" ของผู้เล่น 4 คน (หน่วยเป็นวินาที ชนิดจำนวนเต็ม) แล้วหาค่าเวลาที่น้อยที่สุด เก็บข้อมูลทั้งหมดใน Array โดยใช้ Loop รับค่าจากผู้ใช้ทีละค่าผ่านทางคีย์บอร์ด

1. ประกาศ Array ชนิด int ขนาด 4 และใช้ Loop รับเวลาของผู้เล่นทีละคนเก็บลง Array
2. หาค่าเวลาที่น้อยที่สุดจาก Array (ใช้ built-in method ของ Array หรือใช้ Loop ก็ได้)
3. แสดง "เวลาที่ผู้เล่นทำภารกิจ" ของผู้เล่นทุกคน และเวลาน้อยที่สุด ออกทาง Console
4. ตั้งชื่อโปรเจกต์: _เลขที่-C-StudentName-p1_

**หากไม่ได้ใช้ Loop ในการรับข้อมูล จะไม่ได้คะแนน**

ตัวอย่างผลลัพธ์:

```text
Enter quest time (seconds:int) for player no. 1: 5
Enter quest time (seconds:int) for player no. 2: 7
Enter quest time (seconds:int) for player no. 3: 10
Enter quest time (seconds:int) for player no. 4: 8
***
The minimum time is: 5 seconds.
```

### ข้อ 2 — Method: ทำลายประตู (CanBreakDoor)

ให้เขียนโปรแกรม C# จำลองเหตุการณ์ที่ผู้เล่นพยายามทำลายประตูในเกม ที่มีข้อกำหนดดังนี้

1. มี **method** ชื่อ **CanBreakDoor** ที่คืนค่าผลลัพธ์ (return type) เป็นชนิด **bool**
2. มีพารามิเตอร์ (**parameters**) 2 ตัว คือ
    - `baseDamage` (ความเสียหายพื้นฐาน) ชนิด integer
    - `bonusMultiplier` (ตัวคูณความเสียหายเพิ่มเติม) กำหนดให้มีค่า 2
3. ภายใน method ให้คำนวณ**ค่าความเสียหายจริงของการพังประตู** ตามสูตร: ความเสียหายจริง = `baseDamage * bonusMultiplier + 10`
4. มีค่าความทนทานของประตู ชนิด int นักศึกษากำหนดค่าได้เอง
5. แสดงค่าความทนทานของประตู และความเสียหายจริงที่คำนวณได้ ออกทาง Console
6. method ต้องคืนค่า
    - `true` ถ้าค่าความเสียหายจริง มากกว่าหรือเท่ากับ ค่าความทนทานของประตู
    - `false` ถ้าค่าความเสียหายจริง น้อยกว่า ค่าความทนทานของประตู
7. ใน Main แสดงผลลัพธ์ของเมธอด **CanBreakDoor** โดยนักศึกษากำหนดค่าตัวแปรที่จำเป็นได้เอง
8. แสดงผลลัพธ์ของ method ผ่าน Console ว่าทำลายประตูได้หรือไม่ (ดูตัวอย่าง)

**หากเขียนโปรแกรมแบบไม่มี Method จะไม่ได้คะแนน**

ตัวอย่างผลลัพธ์:

```text
Player is breaking the door!
Door Defense: 70, BreakDoor Actual Damage: 90
Break Door Result: True
```

> **การส่ง** ส่งไฟล์ `Program.cs` และภาพ screenshot ผลลัพธ์การรันโปรแกรมดังกล่าวข้างต้น

---

## ตัวอย่างโค้ดเฉลย: Final Programming #3

โค้ดนี้คอมไพล์และรันแล้ว ได้ผลลัพธ์ตรงกับตัวอย่างของโจทย์ ลองทำเองให้เสร็จก่อนแล้วค่อยเทียบ แนวคิดของ Final Programming #1 และ #2 ใช้โครงเดียวกัน

```csharp
using System;

namespace FinalProgramming3
{
    internal class Program
    {
        // ข้อ 2: method คืนค่า bool
        static bool CanBreakDoor(int baseDamage, int bonusMultiplier = 2)
        {
            int doorDefense = 70;                                  // ค่าความทนทานของประตู (กำหนดเอง)
            int actualDamage = baseDamage * bonusMultiplier + 10;  // ความเสียหายจริง

            Console.WriteLine("Door Defense: " + doorDefense + ", BreakDoor Actual Damage: " + actualDamage);

            return actualDamage >= doorDefense;                    // true ถ้า >= , false ถ้า <
        }

        static void Main(string[] args)
        {
            // ---------- ข้อ 1: Array + Loop ----------
            int[] times = new int[4];

            for (int i = 0; i < times.Length; i++)
            {
                Console.Write("Enter quest time (seconds:int) for player no. " + (i + 1) + ": ");
                int value;
                int.TryParse(Console.ReadLine(), out value);
                times[i] = value;
            }

            int min = times[0];
            for (int i = 1; i < times.Length; i++)
            {
                if (times[i] < min)
                {
                    min = times[i];
                }
            }

            Console.WriteLine("***");
            Console.WriteLine("The minimum time is: " + min + " seconds.");

            // ---------- ข้อ 2: Method ----------
            Console.WriteLine();
            Console.WriteLine("Player is breaking the door!");
            bool result = CanBreakDoor(40);
            Console.WriteLine("Break Door Result: " + result);
        }
    }
}
```

อ่านโค้ดตามลำดับข้อกำหนด:

1. ข้อ 1: สร้าง Array ขนาด 4 แล้วใช้ for-loop รับค่าทีละตัว ส่วน `int.TryParse` แปลงข้อความที่พิมพ์เป็นจำนวนเต็ม
2. หาค่าน้อยสุด: เริ่มจากสมมติว่า `times[0]` น้อยที่สุด แล้ววนเทียบกับช่องอื่น ถ้าเจอค่าที่น้อยกว่าให้เปลี่ยนค่า
3. ข้อ 2: `CanBreakDoor` รับ `baseDamage` ให้ `bonusMultiplier` มีค่าตั้งต้น 2 จึงเรียก `CanBreakDoor(40)` ได้ (เขียน `CanBreakDoor(40, 2)` ก็ได้ผลเท่ากัน) แล้วคำนวณความเสียหายจริงด้วยสูตร `baseDamage * bonusMultiplier + 10`
4. ค่าที่คืนคือ `actualDamage >= doorDefense` ซึ่งเป็น bool อยู่แล้ว จึง return ได้ทันทีโดยไม่ต้องเขียน if
5. ทดสอบให้ครบทั้ง true และ false: `CanBreakDoor(40)` ได้ความเสียหาย 90 (≥ 70 → True) ส่วน `CanBreakDoor(20)` ได้ 50 (< 70 → False)

ผลลัพธ์เมื่อพิมพ์เวลา 5, 7, 10, 8:

```text
Enter quest time (seconds:int) for player no. 1: 5
Enter quest time (seconds:int) for player no. 2: 7
Enter quest time (seconds:int) for player no. 3: 10
Enter quest time (seconds:int) for player no. 4: 8
***
The minimum time is: 5 seconds.

Player is breaking the door!
Door Defense: 70, BreakDoor Actual Damage: 90
Break Door Result: True
```
