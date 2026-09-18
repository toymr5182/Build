# ALICE → Minecraft 26.1.2

นี่คือ workspace สำหรับพอร์ต ไม่ใช่ JAR ที่รับประกันว่าใช้ได้ทันที

เหตุผลสำคัญ: Minecraft 26.1 เป็นต้นไปเป็น unobfuscated และ Fabric ระบุว่าม็อดที่คอมไพล์กับ 1.21.11 หรือต่ำกว่าจะไม่สามารถนำมาใช้กับ 26.1 ได้ตรง ๆ ต้องพอร์ต source/mixins ไปยังชื่อ API ใหม่ก่อน

ไฟล์ต้นฉบับอยู่ที่ `input/alice-offline-1.21.11-latest.jar`

## ก่อน build

1. ใส่ `meteor-client.jar` ของ Meteor Client ที่ตรงกับ Minecraft 26.1.2 ลงใน `input/`
2. ต้องมี JDK 25
3. ต้องมี Gradle 9.4+ หรือใช้ wrapper ที่สร้างเอง
4. ต้อง decompile JAR เป็น source ก่อน แล้วนำ source ไปไว้ใน `src/main/java/`
5. แก้ references จาก Intermediary/Yarn ของ 1.21.11 เป็น Mojang names ของ 26.1.2 และแก้ Mixins ทุกตัวที่ target class/method เปลี่ยน

## ตรวจสอบว่า build environment ถูกต้อง

```bash
gradle --version
gradle build
```

ถ้า source ยังไม่มี `src/main/java/com/nnpg/alice/...` การ build จะยังไม่สร้าง ALICE จริง

## จุดที่ต้องพอร์ต

- `net.minecraft.class_*` → Mojang names ของ 26.1.2
- `net.minecraft.field_*` / `method_*` → fields/methods ของ 26.1.2
- Mixins ใน `alice.mixins.json`
- Fabric API imports ที่เปลี่ยนชื่อ
- Meteor Client API ที่เปลี่ยนจากรุ่น 1.21.11

อย่าแก้แค่ `fabric.mod.json` เพราะจะทำให้ Loader ยอมอ่าน metadata แต่ bytecode เดิมยังอ้างอิง Minecraft 1.21.11 อยู่
