# PEA AI Competition 2569

การแข่งขันทักษะการปฏิบัติงาน ครั้งที่ 13 ประจำปี 2569  
**แข่ง:** 8-9 กันยายน 2569 | **สถานที่:** ศฝฟ. นครชัยศรี

---

## Tracks

| # | Track | คะแนน | Notebook |
|---|-------|--------|----------|
| 1 | Enhance Renewable Forecasting | 25 | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/akekapong78/ai-competition/blob/main/01-forecasting/forecasting_xgboost.ipynb) |
| 2 | Image Processing | 25 | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/akekapong78/ai-competition/blob/main/02-image-processing/image_yolo.ipynb) |
| 3 | Agentic AI for Customer Service | 25 | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/akekapong78/ai-competition/blob/main/03-agentic-ai/agentic_ai.ipynb) |
| 4 | Pitching | 25 | [content.md](04-pitching/content.md) |

---

## วิธีรัน Notebook ด้วย VS Code + Google Colab

> **แนะนำ:** เขียน code บน VS Code (local) แต่รันบน Colab GPU — ดีที่สุดของสองโลก

### 1. ติดตั้ง Extension

เปิด VS Code → Extensions (`Ctrl+Shift+X`) → ค้นหา **"Colab"** → ติดตั้ง **Google Colab** (by Google Colab)

หรือกด: [vscode:extension/GoogleColab.colab-vscode](vscode:extension/GoogleColab.colab-vscode)

### 2. เปิด Notebook

เปิดไฟล์ `.ipynb` ในโปรเจกต์นี้ เช่น `01-forecasting/forecasting_xgboost.ipynb`

### 3. เชื่อมต่อ Colab

1. คลิก **"Select Kernel"** มุมขวาบน
2. เลือก **Colab** จาก dropdown
3. เลือก **"Auto Connect"** (ใช้ T4 GPU ฟรี) หรือ **"New Colab Server"** (เลือก GPU type)
4. คลิก **Allow** → Sign in ด้วย Google Account
5. Complete OAuth flow ในเบราว์เซอร์ → กลับมา VS Code อัตโนมัติ

### 4. รันได้เลย

เลือก kernel แล้วรัน cell ตามปกติ — GPU อยู่บน Colab แต่ editor อยู่ที่ VS Code

### Tips

| Feature | วิธีใช้ |
|---------|---------|
| Monitor GPU/RAM | ดูที่ Activity Bar (ไอคอน Colab ด้านซ้าย) |
| Upload file ไป Colab | Right-click ใน Explorer → **Upload to Colab** |
| Mount Google Drive | `Ctrl+Shift+P` → **Colab: Mount Google Drive** |
| Remove server | `Ctrl+Shift+P` → **Colab: Remove Server** |
| Terminal บน Colab | `Ctrl+Shift+P` → **Colab: New Terminal** (experimental) |

> **Prerequisites:** Google Account + internet connection  
> **Full guide:** https://github.com/googlecolab/colab-vscode/wiki/User-Guide

---

## Learning Roadmap

```
Week 1 (ก.ค.)    → 01-forecasting/    XGBoost time series
Week 2 (ก.ค.)    → 02-image-processing/ YOLO fine-tuning
Week 3 (ก.ค.-ส.ค.) → 03-agentic-ai/  RAG + multi-agent
Week 4 (ส.ค.)    → 04-pitching/       Presentation prep
~8 ส.ค.          → ได้ dataset จริงจาก PEA → apply + tune
8-9 ก.ย.         → Competition Day
```

---

## Stack

| Track | Library |
|-------|---------|
| Forecasting | `xgboost`, `pandas`, `scikit-learn` |
| Image | `ultralytics` (YOLO latest) |
| Agentic AI | `langchain`, `chromadb`, `anthropic` |
| Runtime | Google Colab T4 GPU via VS Code extension |

---

## Resources

- [PLAN.md](PLAN.md) — full competition plan
- [CONTEXT.md](CONTEXT.md) — domain glossary
- [Competition Rules](rules/) — กติกาและเกณฑ์การให้คะแนน
