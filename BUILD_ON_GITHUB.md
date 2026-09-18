# ALICE 26.1.2 — GitHub Actions Build

## วิธีใช้บนมือถือ

1. เข้า GitHub และสร้าง repository ใหม่
2. แนะนำให้ตั้งเป็น Private ถ้าโค้ดม็อดไม่ควรเผยแพร่
3. แตก ZIP นี้ แล้วอัปโหลดไฟล์/โฟลเดอร์ทั้งหมดเข้า repository
4. ตรวจว่ามีไฟล์:
   `.github/workflows/build.yml`
5. ตรวจว่ามี `gradlew` และ `gradle/wrapper/` อยู่ที่ root ของโปรเจกต์
6. ไปที่แท็บ Actions
7. เลือก `Build ALICE 26.1.2`
8. กด `Run workflow`
9. รอจนงาน Build เสร็จ
10. เปิดรายการ workflow ที่เพิ่งรัน
11. เลื่อนลงไปที่ `Artifacts`
12. ดาวน์โหลด `alice-26.1.2-build`

## สำคัญ

GitHub Actions ทำหน้าที่ "คอมไพล์" โปรเจกต์เท่านั้น
ถ้า source code ยังไม่ได้ port จาก Minecraft 1.21.11 เป็น 26.1.2,
workflow จะหยุดด้วย compile error ซึ่งต้องแก้ source ก่อน

Minecraft 26.1+ ใช้ Loom สำหรับ non-obfuscated Minecraft:
`net.fabricmc.fabric-loom`

ส่วน Minecraft 1.21.11 และเก่ากว่าใช้ remap Loom:
`net.fabricmc.fabric-loom-remap`

ดังนั้น build.gradle ต้องตรงกับโปรเจกต์ 26.1.2
