# Pitching Content — PEA AI Competition

**เวลา:** 8 นาที นำเสนอ + 7 นาที ถาม-ตอบ  
**Scope:** ครอบคลุมทั้ง 3 tracks

---

## Story หลัก: "PEA Smart Operation"

> **"3 AI หนึ่งเดียว เพื่อ PEA ที่แม่น เร็ว และดูแลลูกค้า 24/7"**

---

## โครงสร้าง 8 นาที

### นาที 1 — Problem (ปัญหา)

**Hook:** "วันนี้ DSO ต้องบริหารระบบไฟฟ้าแบบตาบอด"

- **Forecasting:** พยากรณ์ Solar/Wind ไม่แม่น → inbalance → ระบบไม่เสถียร
- **Image:** ตรวจสอบอุปกรณ์ด้วยมือ → ช้า → error สูง
- **Customer Service:** ลูกค้าโทร 1129 รอนาน → ไม่พอใจ

**Data ที่ควรใส่:**
- % error ของ forecast ปัจจุบัน (ถ้ามี)
- เวลาเฉลี่ยที่ลูกค้ารอสาย

---

### นาที 2-3 — Solution (วิธีแก้)

#### Track 1: Enhance Renewable Forecasting

```
ข้อมูล Wind/Solar → XGBoost Model → พยากรณ์แม่น → DSO บริหารได้ดีขึ้น
```

- **Input:** historical production data (15 นาที / 1 ชั่วโมง)
- **Model:** XGBoost + time features + lag features
- **Output:** กำลังการผลิต next 24h
- **ผลลัพธ์:** ลด inbalance X%

#### Track 2: Image Processing

```
ภาพอุปกรณ์ → YOLO Model → จำแนก/ตรวจจับ → Excel/CSV
```

- **Input:** ภาพจากระบบ Bisme, MRM, U_cube
- **Model:** YOLO fine-tuned บน PEA equipment
- **Output:** class + confidence + location
- **ผลลัพธ์:** ลดเวลาตรวจสอบ X%

#### Track 3: Agentic AI for Customer Service

```
ลูกค้า → Router Agent → Specialist Agent → RAG (KB) → ตอบทันที
```

- **Input:** คำถามลูกค้า (text/voice)
- **Model:** Claude + RAG (1129 data + km cs)
- **Output:** คำตอบภาษาไทย + action (เช่น สร้าง ticket)
- **ผลลัพธ์:** ตอบ 24/7 ลดภาระ call center X%

---

### นาที 4 — Demo (ถ้ามีเวลา)

- แสดง forecast graph — actual vs predicted
- แสดง image detection บนหน้าจอ
- สาธิต chatbot ตอบคำถามลูกค้า live

---

### นาที 5 — Results & Metrics

| Track | Metric | ผลลัพธ์ |
|-------|--------|---------|
| Forecasting | MAPE | < X% |
| Image | mAP50 | > X% |
| Agentic AI | Intent Accuracy | > X% |

---

### นาที 6 — Scalability (การขยายผล)

**ระยะสั้น (3-6 เดือน):**
- Deploy Forecasting บน DSO dashboard
- ขยาย Image model ให้ครอบคลุมอุปกรณ์ทุกประเภท
- เปิด Chatbot ผ่าน LINE Official PEA

**ระยะกลาง (1-2 ปี):**
- Integrate กับระบบ SCADA
- Real-time anomaly detection
- Predictive maintenance จาก image data

**ระยะยาว:**
- PEA Digital Twin
- Autonomous grid management

---

### นาที 7 — Business Impact

| ด้าน | ผลกระทบ |
|------|---------|
| ลดต้นทุน | ลด outsource ด้าน AI solution |
| เพิ่มประสิทธิภาพ | DSO บริหารโครงข่ายแม่นขึ้น |
| ลูกค้าพึงพอใจ | ตอบเร็ว 24/7 |
| In-house capability | พนักงาน PEA พัฒนา AI เองได้ |

---

### นาที 8 — สรุป + Call to Action

> "3 AI ที่เราสร้าง ไม่ใช่แค่ competition — มันคือ proof of concept ที่ PEA ทำเองได้"

**สิ่งที่ต้องการ:**
- Support จากผู้บริหาร ขยายผลสู่ production
- ข้อมูลจริงจากระบบ (SCADA, 1129, km cs)

---

## Q&A — คำถามที่น่าจะถาม

**Q: accuracy พอไหม สำหรับ production?**  
A: ผลจาก competition เป็น baseline → fine-tune ด้วย data จริงเพิ่ม accuracy ได้ต่อเนื่อง

**Q: ต้องการ infrastructure อะไร?**  
A: เริ่มต้นที่ server ของ PEA ที่มีอยู่ + GPU สำหรับ training (Google Colab หรือ on-premise)

**Q: data privacy?**  
A: model train บน on-premise ข้อมูลไม่ออกนอกองค์กร, LLM ใช้ private deployment ได้

**Q: ถ้า model ตอบผิดล่ะ?**  
A: มี fallback → ส่งต่อ human agent, ไม่มี auto-action บน critical systems

---

## Slide Structure (แนะนำ)

1. Cover — ชื่อทีม + "PEA Smart Operation"
2. Problem — 3 pain points พร้อม data
3. Solution Overview — diagram ภาพรวม 3 tracks
4. Track 1: Forecasting — diagram + metrics
5. Track 2: Image Processing — ภาพตัวอย่าง + metrics  
6. Track 3: Agentic AI — flow + demo screenshot
7. Results — ตาราง metrics รวม
8. Scalability — roadmap
9. Business Impact — ROI/value
10. สรุป + Q&A

**เวลาต่อ slide:** ~45 วินาที (10 slides × 48 วินาที ≈ 8 นาที)
