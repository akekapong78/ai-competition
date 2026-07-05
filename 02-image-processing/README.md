# Week 2: Image Processing with YOLO

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR_GITHUB/ai-competition/blob/main/02-image-processing/image_yolo.ipynb)

---

## โจทย์การแข่งขัน

ตรวจสอบข้อมูลในการปฏิบัติงานด้านระบบไฟฟ้า หรือด้านคลัง  
Data source: Bisme, MRM, U_cube

**Task Day 1:** รับภาพ → ส่งผล excel/csv ก่อน 16:30

---

## Classification vs Detection — เลือกอะไร?

ยังไม่รู้โจทย์ชัด → เตรียมทั้งสองแบบ:

| Task | โจทย์แบบไหน | Output |
|------|------------|--------|
| **Classification** | "ภาพนี้คืออะไร?" เช่น transformer / meter / pole | class label ต่อภาพ |
| **Detection** | "อุปกรณ์อยู่ตรงไหนในภาพ?" | bounding box + class |

**กลยุทธ์:** ใช้ YOLO — handle ได้ทั้งสอง  
- ถ้าโจทย์ = classification → ใช้ YOLO classify mode  
- ถ้าโจทย์ = detection → ใช้ YOLO detect mode (default)

---

## YOLO Architecture (ย่อ)

```
Input Image
    ↓
Backbone (feature extraction)
    ↓
Neck (feature pyramid — จับ object หลายขนาด)
    ↓
Head
 ├── Bounding boxes (x, y, w, h)
 ├── Confidence score
 └── Class probabilities
```

**ทำไม YOLO?**
- Single-pass → เร็วมาก (real-time)
- Fine-tune ด้วย dataset เล็กได้
- Ultralytics API ใช้ง่าย — 5 บรรทัด train ได้

---

## Transfer Learning คืออะไร?

แทนที่จะ train จาก scratch (ต้องการ data แสนรูป) → ใช้ pretrained weights ที่ train บน COCO แล้ว (80 classes) → fine-tune เฉพาะ domain PEA

```
COCO pretrained weights  →  fine-tune  →  PEA equipment model
   (general knowledge)       (ไม่กี่ epoch)    (specific knowledge)
```

เหมาะมากสำหรับ competition ที่มี data ไม่มาก

---

## Dataset Format (YOLO)

```
dataset/
├── images/
│   ├── train/   ← รูปสำหรับ train (70-80%)
│   └── val/     ← รูปสำหรับ validate (20-30%)
├── labels/
│   ├── train/   ← .txt ต่อรูป
│   └── val/
└── data.yaml    ← config file
```

**Label format (.txt):**
```
class_id  cx  cy  w  h    ← normalized 0-1
0         0.5 0.5 0.3 0.4
```

---

## Learning Path (notebook นี้)

1. **Setup** — install ultralytics, ดู YOLO API
2. **Dataset** — โหลด public dataset (electrical equipment จาก Roboflow)
3. **Explore** — ดูภาพ + labels
4. **Train** — fine-tune YOLO บน dataset
5. **Evaluate** — mAP, Precision, Recall
6. **Inference** — ทดสอบกับภาพใหม่
7. **Export** — บันทึก model พร้อมใช้วันแข่ง
8. **Submission Pipeline** — ส่งผลเป็น CSV

---

## เมื่อได้ Data จริงจาก PEA

1. ดูว่า task คือ classification หรือ detection
2. Label data ด้วย [Label Studio](https://labelstud.io/) หรือ [Roboflow](https://roboflow.com/)
3. Export เป็น YOLO format
4. Fine-tune จาก checkpoint ที่ train ไว้แล้ว (ใน notebook นี้)
