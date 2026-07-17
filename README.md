# OSO Tasks

เว็บแอปบันทึกและติดตามงานประจำของทีม Onsite Support Officer (OSO) — ใช้งานได้ทุกอุปกรณ์ (คอมพิวเตอร์ / มือถือ / แท็บเล็ต) ผ่านลิงก์เดียว ไม่ต้องติดตั้งอะไร

**ลิงก์ใช้งานจริง:** https://janjirax2000-hash.github.io/oso-tasks/

---

## ภาพรวม

OSO Tasks เป็นไฟล์ HTML เดี่ยว (`index.html`) ที่ไม่มีเซิร์ฟเวอร์ backend ของตัวเอง โดย:

- **ข้อมูลงาน** เก็บได้ 2 แบบ:
  - **โหมดทำงานเดี่ยว** — เก็บใน `localStorage` ของเบราว์เซอร์เครื่องนั้นๆ (ค่าเริ่มต้น ถ้ายังไม่ได้เชื่อมต่อทีม)
  - **โหมดทีม** — เก็บบน **Firebase Realtime Database** แชร์เห็นตรงกันทุกอุปกรณ์แบบเรียลไทม์
- **หน้าเว็บ** โฮสต์ฟรีบน **GitHub Pages**
- **ปฏิทิน** ซิงก์กับ **Google Calendar** ของผู้ใช้แต่ละคนผ่าน OAuth (ไม่บังคับ)

---

## ฟีเจอร์หลัก

- เพิ่ม / แก้ไข / ลบงาน — งานที่ลบไม่หายทันที ถูกเก็บใน "ประวัติที่ลบ" กู้คืนได้ตลอด
- จัดกลุ่มงานตาม **Project** เป็นการ์ดแยกกัน พับ/กางได้
- จัดการ **Project**, **ผู้รับผิดชอบ**, **Status** ได้เอง (เพิ่ม/แก้ชื่อ/ลบ) — Project และผู้รับผิดชอบเลือกสีเองได้
- หนึ่งงานมอบหมาย **ผู้รับผิดชอบได้มากกว่า 1 คน** (แสดงเป็น badge สีต่อคน)
- แจ้งเตือนงาน **เลยกำหนด** อัตโนมัติ (badge สีแดง)
- ค้นหา + กรองตาม Status
- ดาวน์โหลดรายงาน **Excel** — เลือกงานเป็นรายตัว เลือกหัวข้อคอลัมน์ และเลือกรูปแบบ (ตาราง / รายงานแยกหัวข้อ)
- **สำรอง/นำเข้าข้อมูล** เป็นไฟล์ JSON
- ซิงก์งานที่มีวันครบกำหนดขึ้น **Google Calendar** ส่วนตัวอัตโนมัติ (ปุ่ม "ซิงก์ทั้งหมด" สำหรับงานเก่า)
- คู่มือการใช้งานในตัวแอป (ปุ่ม "📘 คู่มือการใช้งาน")

---

## โหมดทีม (Firebase)

เมื่อสถานะบนสุดของหน้าโชว์ **"โหมดทีม (Firebase) — เชื่อมต่อแล้ว"** ทุกคนที่เปิดลิงก์นี้จะเห็น/แก้ไขข้อมูลชุดเดียวกันแบบเรียลไทม์ — ค่า config ของ Firebase ถูกฝังไว้ในโค้ดแล้ว (`firebaseConfig` ในไฟล์ `index.html`) จึงเชื่อมต่ออัตโนมัติทันทีที่เปิดหน้า ไม่ต้องตั้งค่าอะไรเพิ่ม

> ⚠️ **ข้อควรระวังด้านความปลอดภัย**: ระบบใช้ Firebase Anonymous Authentication เพื่อให้ไม่ต้องมีหน้าล็อกอิน ดังนั้น **ใครก็ตามที่มีลิงก์นี้สามารถเพิ่ม/แก้ไข/ลบงานได้เหมือนกัน** โดยไม่มีการยืนยันตัวตนว่าเป็นใคร จึงควรส่งลิงก์เฉพาะให้คนในทีมที่ไว้ใจได้เท่านั้น

---

## Google Calendar

งานที่มีวันที่ "Target Finished" จะซิงก์ขึ้น Google Calendar ส่วนตัวของผู้ใช้แต่ละคนได้ (ต้องกด "เชื่อมต่อ" และอนุญาตสิทธิ์ก่อน) Client ID ของ Google OAuth ก็ถูกฝังไว้ในโค้ดแล้วเช่นกัน (`gcalConfig` ในไฟล์ `index.html`) — ผู้ใช้ทั่วไปแค่กด "เชื่อมต่อ" แล้วเลือกบัญชี Google ของตัวเองก็พอ

**ข้อจำกัดสำคัญ:** เนื่องจากแอปยังอยู่ในสถานะ "Testing" ของ Google OAuth consent screen มีเพียงอีเมลที่แอดมินเพิ่มไว้ใน **Test users** เท่านั้นที่ล็อกอินผ่าน Google Calendar ได้ (ดูวิธีเพิ่มด้านล่าง)

ดูคู่มือฉบับภาพสำหรับผู้ใช้ทั่วไปได้ที่ปุ่ม "📘 คู่มือการใช้งาน" ในตัวแอป

---

## Setup สำหรับแอดมิน (ทำครั้งเดียว)

### 1. GitHub Pages

1. สร้าง repository ใหม่บน GitHub (Public) → push โค้ดในโฟลเดอร์นี้ขึ้นไป
2. Settings → Pages → Source: "Deploy from a branch" → Branch: `main` / `(root)` → Save
3. จะได้ลิงก์ `https://<username>.github.io/<repo>/`

### 2. Firebase Realtime Database (โหมดทีม)

1. https://console.firebase.google.com → Add project
2. Build → Realtime Database → Create Database → Start in locked mode
3. แท็บ Rules ใส่:
   ```json
   { "rules": { ".read": "auth != null", ".write": "auth != null" } }
   ```
4. Build → Authentication → Sign-in method → เปิดใช้ **Anonymous**
5. Project settings → General → Your apps → เพิ่ม Web app (`</>`) → คัดลอกค่า `apiKey`, `authDomain`, `databaseURL`, `projectId`, `appId`
6. นำค่าไปแทนที่ตัวแปร `firebaseConfig` ในไฟล์ `index.html`

### 3. Google Calendar OAuth

1. https://console.cloud.google.com → เลือกโปรเจกต์เดียวกับ Firebase (ชื่อเดียวกัน เช่น `oso-tasks`)
2. APIs & Services → Library → เปิดใช้ **Google Calendar API**
3. APIs & Services → OAuth consent screen (Google Auth Platform):
   - Branding: กรอกชื่อแอปและอีเมลติดต่อ
   - Audience: เลือก External → เพิ่มอีเมลผู้ใช้ทุกคนใน **Test users**
4. Clients → Create client → Web application → Authorized JavaScript origins ใส่ URL ของ GitHub Pages (เช่น `https://<username>.github.io`) → Create
5. คัดลอก Client ID (ลงท้ายด้วย `.apps.googleusercontent.com`) ไปแทนที่ตัวแปร `gcalConfig.clientId` ในไฟล์ `index.html`

---

## โครงสร้างไฟล์

```
oso-tasks-site/
├── index.html   # ตัวแอปทั้งหมด (HTML + CSS + JS ในไฟล์เดียว)
├── logo.jpg     # โลโก้บริษัทที่แสดงในหัวเว็บ
└── README.md    # เอกสารนี้
```

---

## ปัญหาที่พบบ่อย

| อาการ | สาเหตุ | วิธีแก้ |
|---|---|---|
| `401: invalid_client` / "Client missing a project id" | ยังไม่ได้เลือกโปรเจกต์ที่ถูกต้องใน Google Cloud Console ตอนสร้าง Client ID | เลือกโปรเจกต์ให้ถูกต้อง แล้วสร้าง Client ID ใหม่ในโปรเจกต์นั้น |
| `401: invalid_client` — "no registered origin" | ยังไม่ได้เพิ่ม URL ของเว็บใน "Authorized JavaScript origins" ของ Client ID | เปิด Client ID ที่สร้างไว้ → เพิ่ม origin → Save (อาจใช้เวลาถึง 2-3 ชม. กว่าจะมีผล) |
| `403: access_denied` — "แอปอยู่ระหว่างทดสอบ" | อีเมลผู้ใช้ยังไม่ถูกเพิ่มเป็น Test user | Google Cloud Console → Audience → Test users → Add users |
| ล็อกอิน Google ไม่ได้เมื่อเปิดจาก LINE/Facebook | Google บล็อกการล็อกอินจากเบราว์เซอร์ในแอปแชท (นโยบายของ Google เอง) | แตะเมนู "•••" เลือก "เปิดในเบราว์เซอร์" ก่อนกดเชื่อมต่อ (แอปมีระบบเตือนอัตโนมัติอยู่แล้ว) |
| Client ID/Firebase config พิมพ์ผิดแล้วเชื่อมต่อไม่ได้ | ค่าที่กรอกในหน้าตั้งค่า (⚙) ไม่ถูกรูปแบบ | แอปมีการตรวจสอบรูปแบบ Client ID อัตโนมัติก่อนบันทึกแล้ว |

---

## หมายเหตุด้านเทคนิค

- ไม่มี build step / dependency ใดๆ — แก้ไข `index.html` แล้ว push ขึ้น GitHub ได้ทันที
- ใช้ไลบรารีภายนอกผ่าน CDN 3 ตัว: SheetJS (export Excel), Google Identity Services (OAuth), Firebase (compat SDK)
- รหัส `id` ของงานเป็น string เสมอ (ตัวเลขนับต่อในโหมดทำงานเดี่ยว, Firebase push key ในโหมดทีม)
