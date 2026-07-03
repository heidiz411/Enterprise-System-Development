# เริ่มต้นใช้ Git CLI สำหรับมือใหม่

คู่มือนี้รวมขั้นตอนพื้นฐานในการใช้ Git ผ่าน command line ตั้งแต่ติดตั้ง ตั้งค่า ไปจนถึงการล็อกอินเพื่อ push ขึ้น GitHub

---

## 1. ติดตั้งและตั้งค่าครั้งแรก

```bash
# ตรวจสอบว่าติดตั้ง git แล้วหรือยัง
git --version

# ตั้งชื่อและอีเมล (ทำครั้งเดียว ใช้ทั้งเครื่อง)
git config --global user.name "ชื่อของคุณ"
git config --global user.email "อีเมลของคุณ"
```

---

## 2. เริ่มต้นโปรเจกต์

```bash
cd ไปยังโฟลเดอร์โปรเจกต์ของคุณ
git init                       # สร้าง repository ใหม่
git add .                      # เพิ่มไฟล์ทั้งหมดเข้า staging
git commit -m "first commit"   # บันทึก snapshot พร้อมข้อความ
```

---

## 3. การล็อกอิน (สำคัญสำหรับการ push)

GitHub **ไม่รองรับการใช้รหัสผ่านแล้ว** ต้องใช้ Personal Access Token (PAT) แทน

### สร้าง Token

1. ไปที่ GitHub → **Settings → Developer settings → Personal access tokens → Tokens (classic)**
2. กด **Generate new token** → ติ๊กสิทธิ์ `repo`
3. คัดลอก token เก็บไว้ (จะเห็นแค่ครั้งเดียว)

### เมื่อ git ถาม username/password ตอน push

- **Username** = ชื่อ GitHub ของคุณ
- **Password** = วาง **token** ลงไป (ไม่ใช่รหัสผ่านจริง)

แนะนำให้จำ credential ไว้ไม่ต้องพิมพ์ซ้ำ:

```bash
git config --global credential.helper store
```

---

## 4. เชื่อมกับ GitHub และ push

```bash
# เชื่อม repo บนเครื่องกับ repo บน GitHub
git remote add origin https://github.com/ชื่อคุณ/ชื่อrepo.git

# push ครั้งแรก
git branch -M main
git push -u origin main
```

หลังจากครั้งแรกแล้ว push ครั้งต่อไปแค่:

```bash
git add .
git commit -m "ข้อความอธิบายการแก้ไข"
git push
```

---

## คำสั่งที่ใช้บ่อย

| คำสั่ง | ความหมาย |
|--------|----------|
| `git status` | ดูสถานะไฟล์ที่เปลี่ยนแปลง |
| `git log` | ดูประวัติ commit |
| `git pull` | ดึงโค้ดล่าสุดจาก GitHub |
| `git clone <url>` | โคลน repo ที่มีอยู่แล้ว |

---

## หมายเหตุ

ทางเลือกที่ปลอดภัยกว่า PAT คือใช้ **SSH key** ซึ่งไม่ต้องพิมพ์ token ทุกครั้ง เหมาะกับการใช้งานระยะยาว
