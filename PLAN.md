# PEA AI Competition Plan
## การแข่งขันทักษะการปฏิบัติงาน ครั้งที่ 13 ประจำปี 2569
**Date:** 8-9 September 2569 | **Venue:** ศฝฟ. นครชัยศรี

---

## Team
- 5 คน
- Python/ML: 2 คน
- Domain (ระบบไฟฟ้า): 4 คน
- LLM/RAG: 1 คน

## Scoring
| Track | คะแนน |
|-------|--------|
| Enhance Renewable Forecasting | 25 |
| Image Processing | 25 |
| Agentic AI for Customer Service | 25 |
| Pitching | 25 |
| **รวม** | **100** |

---

## Timeline

### ก่อนแข่ง (ปัจจุบัน → ~8 ส.ค.)
เรียนรู้ ทำ notebook ทีละ track

| Week | Track | Goal |
|------|-------|------|
| 1 (ก.ค.) | Forecasting | XGBoost pipeline พร้อมใช้กับ data จริง |
| 2 (ก.ค.) | Image Processing | YOLOv26n fine-tuning pipeline |
| 3 (ก.ค.-ส.ค.) | Agentic AI | Pure Python RAG + tools |
| 4 (ส.ค.) | Pitching | MD content skeleton |

### หลังได้ Dataset (~8 ส.ค. → 8 ก.ย.)
- Apply pipeline กับ data จริง
- Tune model
- เตรียม inference script พร้อม Day 1

---

## Track Details

### 1. Enhance Renewable Forecasting
- **Pain point:** DSO บริหารโครงข่ายยากเพราะ forecast ไม่แม่น → inbalance
- **Data:** Wind + Solar production data
- **Task Day 1:** รับโจทย์ → เติมค่า production ที่หายไป → ส่งก่อน 16:30
- **Approach:** XGBoost + feature engineering
  - Features: hour, day_of_week, month, lag(t-1, t-24, t-168), rolling_mean
  - Solar: เพิ่ม daylight/solar angle features
  - Wind: lag ยาวกว่า Solar
- **Metric:** ความถูกต้อง (คาดว่า RMSE/MAE)

### 2. Image Processing
- **Pain point:** ตรวจสอบข้อมูลในงานด้านระบบไฟฟ้า/คลัง
- **Data source:** Bisme, MRM, U_cube (ยังไม่รู้ชัด)
- **Task Day 1:** รับภาพ → ส่งผลลัพธ์ excel/csv ก่อน 16:30
- **Approach:** YOLOv26n — เตรียม pipeline ทั้ง classification + detection
  - ถ้า data = object in image → detection
  - ถ้า data = image category → classification
  - ตัดสินใจเมื่อเห็น data จริง
- **Metric:** accuracy

### 3. Agentic AI for Customer Service
- **Pain point:** ตอบสนองลูกค้าช้า ปัญหาหลากหลาย (แจ้งซ่อม, ค่าไฟ, ขอบริการใหม่)
- **Data source:** การแจ้งปัญหา 1129, km cs
- **Approach:** Pure Python
  - **Architecture:** Multi-agent router (ดีสำหรับ pitching)
  - **Implementation:** RAG + tools (เริ่มจากนี้)
  - **Stack:** LangChain/LlamaIndex + vector DB
  - N8N: ไม่ใช้ — pure code
- **Scoring:** ด้านไอเดีย (pitching) + ด้านการใช้งาน (test Q&A set)

### 4. Pitching
- **เวลา:** 8 นาที นำเสนอ + 7 นาที ถาม-ตอบ
- **Scope:** ครอบคลุมทั้ง 3 tracks
- **Story:** "PEA Smart Operation" — พยากรณ์แม่น + ตรวจอุปกรณ์อัตโนมัติ + บริการลูกค้า 24/7
- **Scoring:** ทักษะนำเสนอ + ความเป็นไปได้ในการขยายผล

---

## Repo Structure
```
ai-competition/
├── PLAN.md                    ← this file
├── rules/                     ← competition rules PDFs
├── 01-forecasting/
│   ├── README.md              ← สอน concept + theory
│   └── notebook.ipynb         ← Colab-ready
├── 02-image-processing/
│   ├── README.md
│   └── notebook.ipynb
├── 03-agentic-ai/
│   ├── README.md
│   └── notebook.ipynb
└── 04-pitching/
    └── content.md
```

Each notebook:
- มี Colab badge ด้านบน
- มี MD cells อธิบาย concept ก่อน code
- ใช้ public dataset สำหรับ learning (ก่อนได้ data จริง)

---

## Environment
- Local: Python + VS Code
- GPU: Google Colab (remote via VS Code extension)
- Competition Day: Notebook/PC join domain pea.co.th + own laptop
