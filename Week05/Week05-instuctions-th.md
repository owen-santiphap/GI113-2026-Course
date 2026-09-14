# Lab 5 — Battle Damage Calculator

**วิชา GI113 Computer Programming (GI)** · สัปดาห์ที่ 5 · เนื้อหา: Arithmetic/Assignment/Comparison/Logical Operators, Precedence, `Math`, `Random`

---

## 🎯 วัตถุประสงค์

สร้าง **หน้าจอคำนวณดาเมจก่อนต่อสู้จริง** (damage preview / scouting report) — แบบเดียวกับที่เกม RPG หลายเกมโชว์ก่อนให้คุณกดโจมตีจริง (Fire Emblem's damage forecast, การเดา type effectiveness ใน Pokémon) ไม่ใช่การจำลองการต่อสู้หลายยกแบบเดิม — เกือบทุกบรรทัดในแล็บนี้คือ **ข้อเท็จจริงที่คำนวณแยกกันเป็นอิสระ** เกี่ยวกับคู่ต่อสู้ (ดาเมจถ้าโจมตีปกติ, ดาเมจถ้าใช้ท่าแรง, ดาเมจถ้าโดนสวนกลับ, ฯลฯ) ไม่ใช่ state ที่ไล่เปลี่ยนไปเรื่อยๆ ทีละก้าว — มี compound assignment ที่ทำจริงแค่ 2 จุดเท่านั้น (ดื่มยา, โจมตีจริงตอนจบ) นอกนั้นเป็นการคำนวณล้วนๆ ใช้ทุกค่าที่อ่านเข้ามาจริง (ไม่มีค่าที่อ่านมาแล้วไม่ได้ใช้) นี่คือ **v1**, สัปดาห์ที่ 6/10 จะได้อัปเกรดให้ตัดสินใจได้เองว่าจะโจมตีแบบไหนจริงๆ

---

## ขั้นตอน

### 1. อ่านค่าเริ่มต้น 6 ค่าด้วย TryParse แล้วแสดงสถานะเริ่มเกม

Hero และ Monster มีค่าละ 3 ค่า (HP, Attack, Defense) — ใช้ `int.TryParse` แบบเดียวกับ Lab 4 ทั้ง 6 ครั้ง แล้วรวมทั้ง 6 ผลลัพธ์เป็น bool เดียวด้วย `&&` (logical AND) จากนั้นแสดงค่าเริ่มต้นเป็นตัวเลขตรงๆ:

```csharp
Console.WriteLine("=== BATTLE DAMAGE CALCULATOR ===");
Console.WriteLine("Hero vs Monster -- scouting the fight before it happens");

Console.Write("Hero HP: ");
bool heroHpOk = int.TryParse(Console.ReadLine(), out int heroHp);
Console.Write("Hero Attack: ");
bool heroAttackOk = int.TryParse(Console.ReadLine(), out int heroAttack);
Console.Write("Hero Defense: ");
bool heroDefenseOk = int.TryParse(Console.ReadLine(), out int heroDefense);
Console.Write("Monster HP: ");
bool monsterHpOk = int.TryParse(Console.ReadLine(), out int monsterHp);
Console.Write("Monster Attack: ");
bool monsterAttackOk = int.TryParse(Console.ReadLine(), out int monsterAttack);
Console.Write("Monster Defense: ");
bool monsterDefenseOk = int.TryParse(Console.ReadLine(), out int monsterDefense);
bool allStatsValid = heroHpOk && heroAttackOk && heroDefenseOk && monsterHpOk && monsterAttackOk && monsterDefenseOk;
Console.WriteLine($"All stats valid: {allStatsValid}");

int monsterMaxHp = monsterHp;
Console.WriteLine($"[Hero]    HP:{heroHp} ATK:{heroAttack} DEF:{heroDefense}");
Console.WriteLine($"[Monster] HP:{monsterHp} ATK:{monsterAttack} DEF:{monsterDefense}");
```

**รันตอนนี้เลย (`Ctrl+F5`)** — แค่นี้ก็รันได้แล้ว ควรเห็น:

```
=== BATTLE DAMAGE CALCULATOR ===
Hero vs Monster -- scouting the fight before it happens
Hero HP: Hero Attack: Hero Defense: Monster HP: Monster Attack: Monster Defense: All stats valid: True
[Hero]    HP:35 ATK:14 DEF:3
[Monster] HP:45 ATK:11 DEF:4
```

### 2. ดื่มยา แล้วคำนวณดาเมจ 3 แบบ (ยังไม่โจมตีจริง แค่ดูตัวเลข)

ดื่มยาก่อน (`+=` — compound assignment แบบ "บวก") จากนั้นคำนวณดาเมจ 3 อย่างแยกกัน โดยยังไม่ apply กับ HP จริง — แค่โชว์ตัวเลขให้ดูเฉยๆ: โจมตีปกติ (`Math.Max`, แพทเทิร์นพื้นฐาน), ท่าแรง (precedence — คูณก่อนลบ, ตรงกับ Slide 21), และถ้า Monster สวนกลับ (สูตรเดียวกับโจมตีปกติ แค่สลับฝั่ง — ใช้ `heroDefense` กับ `monsterAttack` ที่ยังไม่ได้ใช้ที่ไหนมาก่อน):

```csharp
// Before scouting: Hero drinks a potion (compound assignment: +=)
int potionHeal = 8;
heroHp += potionHeal;
Console.WriteLine($"Hero drinks a potion, healing {potionHeal}. Hero HP is now {heroHp}.");

// Damage preview 1: Normal Attack (arithmetic + Math -- the base pattern)
int normalDamage = Math.Max(0, heroAttack - monsterDefense);
Console.WriteLine($"Normal Attack would deal: {normalDamage} damage");

// Damage preview 2: Power Attack (precedence -- multiply before subtract)
int powerDamage = Math.Max(0, heroAttack * 2 - monsterDefense);
Console.WriteLine($"Power Attack would deal: {powerDamage} damage");

// Damage preview 3: what Monster would deal back, if it got a turn (same pattern, other side)
int counterDamage = Math.Max(0, monsterAttack - heroDefense);
Console.WriteLine($"If Monster counters afterward, it would deal: {counterDamage} damage");
```

**รันอีกครั้ง** — ต้องเห็นของเดิมจาก Step 1 เหมือนเดิม บวกอีก 4 บรรทัดใหม่ต่อท้าย:

```
Hero drinks a potion, healing 8. Hero HP is now 43.
Normal Attack would deal: 10 damage
Power Attack would deal: 24 damage
If Monster counters afterward, it would deal: 8 damage
```

### 3. คริติคอลฮิต (จุดเดียวในทั้งแล็บที่ใช้ Random)

สุ่มโอกาส **10% คริติคอล** สำหรับ Normal Attack ด้วย `Convert.ToInt32(bool)` (ทวน Week 3 — ไม่ใช้ `if`) — ทั้งไฟล์เรียก `rng.Next()` แค่ครั้งเดียว ไม่มีจุดที่สองให้สับสนเรื่องลำดับ:

```csharp
Random rng = new Random(14);
int roll = rng.Next(1, 101);
bool isCritical = roll <= 10;
int criticalDamage = normalDamage + Convert.ToInt32(isCritical) * normalDamage;
Console.WriteLine($"Critical hit roll: {roll} (critical: {isCritical})");
Console.WriteLine($"If critical, Normal Attack would instead deal: {criticalDamage} damage");
```

> 💡 ใช้ seed เดียวกับที่สอนในคาบ (`new Random(14)`) เพื่อให้ผลลัพธ์ตรงกับตัวอย่างที่ทำด้วยกัน — ถ้าใช้ `new Random()` เฉยๆ ผลจะสุ่มไม่ซ้ำกันทุกครั้งที่รัน (ซึ่งเป็นเรื่องปกติของเกมจริง แค่ตอนเรียนอยากให้ตัวเลขตรงกันเพื่อคุยกันในห้องง่ายขึ้น)

**รันอีกครั้ง** — เพิ่มอีก 2 บรรทัด:

```
Critical hit roll: 5 (critical: True)
If critical, Normal Attack would instead deal: 20 damage
```

### 4. สรุปรายงานสอดแนม (comparison + logical operators)

เอาตัวเลขที่คำนวณไว้ด้านบนมาตอบคำถามจริงด้วย comparison + logical operator — นี่คือจุดที่ `&&`, `||`, และ `!` ทั้งสามตัวถูกใช้จริง:

```csharp
bool heroHitsHarder = heroAttack > monsterAttack;
bool canOneShotWithNormal = normalDamage >= monsterHp;
bool monsterCanOneShotHero = counterDamage >= heroHp;
bool safeTrade = normalDamage > counterDamage && !monsterCanOneShotHero;
bool luckyOrLethal = isCritical || canOneShotWithNormal;
Console.WriteLine($"Hero hits harder than Monster: {heroHitsHarder}");
Console.WriteLine($"Normal Attack can defeat Monster in one hit: {canOneShotWithNormal}");
Console.WriteLine($"Monster could defeat Hero in one hit back: {monsterCanOneShotHero}");
Console.WriteLine($"This is a safe trade for Hero: {safeTrade}");
Console.WriteLine($"This attack is lucky or lethal: {luckyOrLethal}");
```

**รันอีกครั้ง** — เพิ่มอีก 5 บรรทัด:

```
Hero hits harder than Monster: True
Normal Attack can defeat Monster in one hit: False
Monster could defeat Hero in one hit back: False
This is a safe trade for Hero: True
This attack is lucky or lethal: True
```

### 5. Hero ลงมือจริง แล้วสรุปผล + รางวัล

ทุกอย่างก่อนหน้านี้เป็นแค่การ "ดู" ตัวเลข — ขั้นนี้คือจุดเดียวที่ Hero โจมตีจริงและ HP ของ Monster เปลี่ยนจริง (`-=` — compound assignment แบบ "ลบ") ปิดท้ายด้วยรางวัลที่คำนวณจาก arithmetic ธรรมดา:

```csharp
// Hero commits to the Normal Attack (compound assignment: -=)
monsterHp -= normalDamage;
Console.WriteLine($"Hero attacks! Monster HP: {monsterHp}/{monsterMaxHp}");

// Result + reward
bool monsterDefeated = monsterHp <= 0;
int goldEarned = (monsterMaxHp - monsterHp) * 2;
Console.WriteLine($"Monster defeated: {monsterDefeated}");
Console.WriteLine($"Gold earned: {goldEarned}");
```

**รันอีกครั้ง (ครบทุก step แล้ว)** — เพิ่มอีก 3 บรรทัดสุดท้าย:

```
Hero attacks! Monster HP: 35/45
Monster defeated: False
Gold earned: 20
```

---

## ตัวอย่างผลลัพธ์ฉบับเต็ม

รันด้วยค่า Hero HP `35`, Attack `14`, Defense `3`, Monster HP `45`, Attack `11`, Defense `4` แล้วหน้าตาผลลัพธ์ทั้งหมดตั้งแต่ต้นจนจบประมาณนี้ (ตัวเลขของคุณจะเปลี่ยนตามค่าที่พิมพ์ — นี่แค่ตัวอย่างให้เทียบเฉยๆ ไม่ต้องตรงเป๊ะทุกตัวอักษร):

```
=== BATTLE DAMAGE CALCULATOR ===
Hero vs Monster -- scouting the fight before it happens
Hero HP: Hero Attack: Hero Defense: Monster HP: Monster Attack: Monster Defense: All stats valid: True
[Hero]    HP:35 ATK:14 DEF:3
[Monster] HP:45 ATK:11 DEF:4
Hero drinks a potion, healing 8. Hero HP is now 43.
Normal Attack would deal: 10 damage
Power Attack would deal: 24 damage
If Monster counters afterward, it would deal: 8 damage
Critical hit roll: 5 (critical: True)
If critical, Normal Attack would instead deal: 20 damage
Hero hits harder than Monster: True
Normal Attack can defeat Monster in one hit: False
Monster could defeat Hero in one hit back: False
This is a safe trade for Hero: True
This attack is lucky or lethal: True
Hero attacks! Monster HP: 35/45
Monster defeated: False
Gold earned: 20
```

---

## ✅ สิ่งที่ต้องส่ง

1. โปรเจกต์เดียว, `Program.cs` ไฟล์เดียว, ชื่อ `Lab05`
2. Header comment (Student ID / Name / Section / No.) บนสุด
3. `Random rng = new Random(14);` ตัวเดียว เรียก `rng.Next()` แค่ครั้งเดียวทั้งไฟล์ (seed เดียวกับที่ใช้ในคาบ เพื่อให้ตัวเลขสอดคล้องกับตัวอย่าง)
4. Commit ด้วยข้อความที่สื่อความหมาย (ห้าม `"update"`) push ขึ้น repo `GI113-2026-<รหัสนักศึกษา>` โพสต์ลิงก์ commit ใน Teams พร้อม screenshot ที่รันได้จริง
