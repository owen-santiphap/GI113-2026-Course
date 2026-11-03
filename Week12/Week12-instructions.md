# Lab 8: Array Statistics

**GI113 Computer Programming (GI)** · สัปดาห์ที่ 12 · เนื้อหา: array, `Length`, `for`, `foreach`, `Array.Sort`

---

## 🎯 วัตถุประสงค์

เก็บตัวเลข 8 ตัวไว้ใน array เดียว แล้วใช้ loop **พิมพ์** ตัวเลขทั้งหมด **หาผลรวมและค่าเฉลี่ย** หา **ค่าสูงสุดและต่ำสุด** และ **เรียงลำดับ**
**Part A** ทุกคนเขียนเหมือนกัน · **Part B** เปลี่ยนตัวเลขใน array ผ่าน Inspector แล้วตรวจว่าโปรแกรมของคุณยังถูกต้อง

**เตรียมโปรเจกต์:** ใช้ scene จากคาบเรียน หรือสร้าง scene ใหม่ (ดูกล่องด้านล่าง) ตั้งชื่อสคริปต์ว่า **`Lab11`**

**กติกา:** ประกาศตัวแปรไว้เหนือ `Start()` · ประกาศตัวนับของ `for` ใน header (`int i`) · พิมพ์โค้ดเองทุกบรรทัด · ข้อความใน Console เป็นภาษาอังกฤษ

> **ถ้าคุณไม่ได้เข้าคาบสัปดาห์ที่ 12:** (1) เปิด Unity 6000.5.6f1 แล้วสร้าง scene ใหม่ที่ **File > New Scene** (2) ใน Hierarchy คลิกขวา **Create Empty** แล้วเปลี่ยนชื่อเป็น `Lab11` (3) ใน `Assets/Scripts` สร้าง MonoBehaviour Script ชื่อ `Lab11` (4) **เขียนบรรทัดของ Step 1 ลงในสคริปต์ก่อน** แล้วค่อยลากสคริปต์ไปวางบน object `Lab11` (5) เปิด Console ด้วย **Ctrl+Shift+C** และปิด **Collapse**

> **ลำดับสำคัญ** Unity จะคัดลอกตัวเลขจากโค้ดไปใส่ใน Inspector ตอนที่เอาสคริปต์ไปวางบน object ครั้งแรก หลังจากนั้น **ค่าใน Inspector เป็นตัวชนะ** ถ้าเพิ่มบรรทัด array ลงในสคริปต์ *หลัง* ที่วางสคริปต์บน object แล้ว Inspector จะว่างเปล่า ให้กดจุดสามจุดของ component แล้วเลือก **Reset**

**รันทุกครั้งที่เขียนจบแต่ละขั้น** แต่ละขั้นพิมพ์บรรทัดของตัวเองออกมาทันที ถ้าบรรทัดไหนผิดจะรู้ได้ตรงนั้นเลย กด **Ctrl+S** บันทึกก่อนกด Play ทุกครั้ง

---

## Part A

### Step 1: สร้าง array

ชื่อเดียว เก็บตัวเลข 8 ตัว `[SerializeField]` ทำให้ array แสดงใน Inspector ถ้าด้านบนยังไม่มี ให้เพิ่ม `using UnityEngine;`

```csharp
[SerializeField] int[] numbers = { 12, 7, 30, 4, 19, 25, 9, 18 };
```

วางสคริปต์บน object แล้วดูใน Inspector: **Numbers** ต้องมี Size เป็น **8**

### Step 2: พิมพ์ตัวเลขทุกตัว

`numbers.Length` เป็น 8 ดังนั้น `i` วิ่งจาก 0 ถึง 7 เราพิมพ์ `i + 1` เพื่อให้ลำดับที่แสดงเริ่มจาก 1 อย่างที่คนนับ

```csharp
void Start()
{
    for (int i = 0; i < numbers.Length; i++)
    {
        Debug.Log("Number " + (i + 1) + ": " + numbers[i]);
    }
}
```

### Step 3: ผลรวมและค่าเฉลี่ย

`sum` เก็บตัวเลขสะสมทีละตัว ต้องตั้งเป็น 0 *ก่อน* เข้า loop ส่วน `(float)` ทำให้การหารได้ทศนิยม ถ้าไม่ใส่ 124 / 8 จะได้ `15` ไม่ใช่ `15.5`

เพิ่มตัวแปร 2 ตัวไว้เหนือ `Start()` และเพิ่มโค้ดใหม่ท้าย `Start()`:

```csharp
int sum;
float average;
```

```csharp
sum = 0;
for (int i = 0; i < numbers.Length; i++)
{
    sum += numbers[i];
}
average = (float)sum / numbers.Length;
Debug.Log("Sum: " + sum);
Debug.Log("Average: " + average);
```

### Step 4: ค่าสูงสุดและค่าต่ำสุด

ให้ตัวแปรทั้งสองเริ่มจาก **ตัวเลขตัวแรก** ไม่ใช่เริ่มจาก 0 แล้วเก็บตัวที่ดีที่สุดเท่าที่เจอมาจนถึงตอนนี้ loop เริ่มที่ 1 เพราะ index 0 อยู่ในตัวแปรแล้ว

ตัวแปรเหนือ `Start()`:

```csharp
int maximum;
int minimum;
```

โค้ดท้าย `Start()`:

```csharp
maximum = numbers[0];
minimum = numbers[0];
for (int i = 1; i < numbers.Length; i++)
{
    if (numbers[i] > maximum)
    {
        maximum = numbers[i];
    }
    if (numbers[i] < minimum)
    {
        minimum = numbers[i];
    }
}
Debug.Log("Maximum: " + maximum);
Debug.Log("Minimum: " + minimum);
```

### Step 5: เรียงลำดับแล้วพิมพ์อีกครั้ง

`System.Array.Sort` เรียงจากน้อยไปมาก และเปลี่ยนค่าใน `numbers` เอง ให้เขียน `System.Array` เต็มๆ ส่วน `foreach` เหมาะกับการพิมพ์ทุกตัวเมื่อไม่ต้องใช้ index

```csharp
System.Array.Sort(numbers);
foreach (int n in numbers)
{
    Debug.Log("Sorted: " + n);
}
```

### ผลลัพธ์เมื่อทำ Part A ครบ

ได้ 20 บรรทัดใน Console เรียงตามนี้ ไม่มีบรรทัดว่าง แต่ละแถวใน Console จะมีบรรทัดเทาบรรทัดที่สอง `UnityEngine.Debug:Log (object)` นั่นเป็นของ Unity ไม่ใช่ของคุณ

```
Number 1: 12
Number 2: 7
Number 3: 30
Number 4: 4
Number 5: 19
Number 6: 25
Number 7: 9
Number 8: 18
Sum: 124
Average: 15.5
Maximum: 30
Minimum: 4
Sorted: 4
Sorted: 7
Sorted: 9
Sorted: 12
Sorted: 18
Sorted: 19
Sorted: 25
Sorted: 30
```

### เช็กตัวเองก่อนส่ง

| อาการ | สาเหตุที่เป็นไปได้ |
|---|---|
| Console ว่าง | ยังไม่ได้วางสคริปต์บน object หรือยังไม่ได้กด Play |
| ขึ้นแดง `IndexOutOfRangeException` | ใช้ `<=` แทน `<` ใน loop หรือ **Numbers** ใน Inspector ว่างจึงไม่มี `numbers[0]` (ดูกล่อง **ลำดับสำคัญ**) |
| `Average: 15` | ลืม `(float)` |
| `Maximum: 0` หรือ `Minimum: 0` | ไม่ได้ให้ตัวแปรเริ่มจาก `numbers[0]` |
| บรรทัด `Number` เรียงลำดับอยู่แล้ว | วาง `Sort` ไว้ก่อน Step 2 |

---

## Part B: ตัวเลขของคุณเอง

โปรแกรมต้องใช้ได้กับ array **ใดก็ได้** ไม่ใช่แค่ตัวเลข 8 ตัวนี้

1. เลือก object `Lab11` ใน Inspector ตั้ง **Numbers > Size** เป็น **5** แล้วพิมพ์ **ตัวเลข 5 ตัวของคุณเอง** (พิมพ์ใน Inspector ไม่ต้องแก้โค้ด)
2. กด Play ตรวจผลทั้ง 4 อย่างด้วยมือ: ผลรวม ค่าเฉลี่ย ค่าสูงสุด ค่าต่ำสุด
3. ลองตัวเลข `3, 40, 8, 15, 22` ต้องได้ Sum **88**, Average **17.6**, Maximum **40**, Minimum **3**
4. ลองตัวเลข **ติดลบ** 3 ตัว เช่น `-5, -2, -9` Maximum ต้องเป็น **-2** และ Minimum ต้องเป็น **-9**

ถ้าผลไม่ถูกกับตัวเลขของคุณ แปลว่าโค้ดมีบั๊ก แก้โค้ดแล้วรันใหม่

---

## 📤 ส่งงาน

1. สร้างโฟลเดอร์ `Lab11` ใน repo `GI113-2026-<รหัสนักศึกษา>` แล้วคัดลอก **`Lab11.cs`** ไปใส่ วาง `HEADER-TEMPLATE.txt` ไว้บนสุดของไฟล์แล้วกรอกให้ครบ
2. **Commit** พร้อมข้อความที่บอกได้ว่าทำอะไร (เช่น `Lab11: array statistics`) แล้ว **Push** ผ่าน GitHub Desktop
3. ส่งใน Teams: **ลิงก์ commit** และ **screenshot 1 รูป** ของหน้าต่าง Unity ที่เห็น Console จากการรัน **Part B** (ให้เห็น Inspector ที่มีตัวเลขของคุณด้วย)
