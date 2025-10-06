# 🚗 เทมเพลตเว็บไซต์ **jaijaicarrental**

<p align="center">
  <img src="./public/preview/homepage.png" alt="ตัวอย่างหน้าแรก" width="800"/>
</p>

เทมเพลตเว็บไซต์**เช่ารถ**ที่ทันสมัยและตอบสนองทุกหน้าจอ (Responsive) สร้างด้วย **Next.js 14**, **Tailwind CSS**, และ **TypeScript**
ออกแบบมาสำหรับธุรกิจให้เช่ารถโดยเฉพาะ — มีโครงสร้างแบบโมดูลาร์, ปรับแต่ง SEO ได้ง่าย, และปรับแก้ได้สะดวก

---

## ✨ คุณสมบัติเด่น
- 🧱 โครงสร้างคอมโพเนนต์แบบโมดูลาร์ (ส่วน Hero, ส่วนยานพาหนะ, ส่วนข้อมูล, ส่วนติดต่อ, ส่วนที่ตั้ง)
- 🧭 พร้อมสำหรับ SEO (Metadata, Open Graph, Canonical URLs)
- ⚡ สร้างด้วย Next.js 14 App Router
- 🖼️ การออกแบบที่ปรับให้เหมาะสมด้วย Tailwind CSS
- 📜 หน้าเอกสารทางกฎหมายที่สร้างไว้ล่วงหน้า (นโยบายคุกกี้, นโยบายความเป็นส่วนตัว, ข้อกำหนดและเงื่อนไข)
- 🔍 ข้อมูลโครงสร้าง (JSON-LD) สำหรับการทำดัชนีของ Google
- 💬 เทมเพลตมีคำอธิบาย (Fully commented) สำหรับนักพัฒนา

---

## 🖼️ ตัวอย่าง

เพิ่มภาพหน้าจอของคุณใน `public/preview/` และอัปเดตพาธรูปภาพด้านล่าง:

### 🏠 หน้าแรก
![ตัวอย่างหน้าแรก](./public/preview/homepage.png)

### 🚘 ส่วนยานพาหนะ
![ตัวอย่างส่วนยานพาหนะ](./public/preview/fleet-section.png)

### 🧾 ส่วนข้อมูล
![ตัวอย่างส่วนข้อมูล](./public/preview/info-section.png)

### ☎️ ส่วนติดต่อ
![ตัวอย่างส่วนติดต่อ](./public/preview/contact-section.png)

### 📍 ส่วนที่ตั้ง
![ตัวอย่างส่วนที่ตั้ง](./public/preview/location-section.png)

---

## ⚙️ การติดตั้ง

โคลน Repository และติดตั้ง Dependencies:

```bash
git clone [https://github.com/USERNAME/CARrental-template.git](https://github.com/USERNAME/CARrental-template.git)
cd CARrental-template
npm install
npm run dev

```

แอปพลิเคชันจะทำงานที่ http://localhost:3000

🧩 คู่มือการปรับแต่ง
แก้ไข Hero.tsx → อัปเดตรูปภาพ Hero, ชื่อเรื่อง, และปุ่ม Call-to-Action (CTA)

แก้ไข Fleet.tsx → ปรับเปลี่ยนรายการรถและคุณสมบัติต่างๆ

แก้ไข Info.tsx → ปรับเปลี่ยนจุดเด่นและข้อดีของบริษัท

แก้ไข Contact.tsx → แทนที่ข้อมูลเบอร์โทรศัพท์, WhatsApp, และอีเมล

แก้ไข Footer.tsx → เพิ่มที่อยู่ธุรกิจและลิงก์ต่างๆ

🧠 เทคโนโลยีที่ใช้ (Tech Stack)
Next.js 14 (App Router)

TypeScript

Tailwind CSS

Lucide React (ไอคอน)

Firebase Ready (รองรับการผสานรวมทางเลือก)

🧰 การนำไปใช้งานจริง (Deployment)
คุณสามารถนำเทมเพลตนี้ไปใช้งานได้ทันทีด้วย Vercel:

พุชโปรเจกต์ของคุณไปที่ GitHub

ไปที่ vercel.com/new

นำเข้า Repository ของคุณ แล้วคลิก Deploy

🧭 โครงสร้างโปรเจกต์
src/app/
  ├── (main)/               → โครงสร้างหลักและหน้าแรก
  ├── politica-cookies/     → โครงสร้างและหน้าสำหรับนโยบายคุกกี้
  ├── politica-de-confidentialitate/ → โครงสร้างและหน้าสำหรับนโยบายความเป็นส่วนตัว
  ├── termeni-conditii/     → โครงสร้างและหน้าสำหรับข้อกำหนดและเงื่อนไข
  └── components/           → คอมโพเนนต์ UI ที่ใช้ซ้ำได้ (Hero, Fleet, Info, Contact, Locations)
📄 ใบอนุญาต
เทมเพลตนี้เป็น Open-Source ภายใต้ MIT License — อนุญาตให้ใช้งานในโปรเจกต์ส่วนตัวหรือเชิงพาณิชย์ได้

👨‍💻 ผู้พัฒนา
## พัฒนาโดย gitmint
สำหรับการสนับสนุนหรือสอบถามข้อมูล ติดต่อได้ทาง GitHub
