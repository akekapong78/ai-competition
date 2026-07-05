# Week 3: Agentic AI for Customer Service

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR_GITHUB/ai-competition/blob/main/03-agentic-ai/agentic_ai.ipynb)

---

## โจทย์การแข่งขัน

ลูกค้า PEA มีปัญหาหลากหลาย:
- แจ้งปัญหาระบบไฟฟ้า (ไฟดับ, ไฟกระชาก)
- สอบถามค่าไฟ
- ขอใช้บริการใหม่
- สอบถามข้อมูลทั่วไป

**Data source:** การแจ้งปัญหา 1129, km cs (knowledge management)  
**Scoring:** ด้านไอเดีย (pitching) + ชุดคำถามวัดผลจริง

---

## Architecture: Multi-Agent Router

```
User Input
    ↓
[Router Agent]  ← classify intent
    ├── "แจ้งปัญหาไฟฟ้า"  → [Power Outage Agent]
    ├── "สอบถามค่าไฟ"     → [Billing Agent]
    ├── "ขอบริการใหม่"    → [Service Agent]
    └── "ทั่วไป"          → [General Agent]
         ↓
    [RAG Tool] ← ดึงข้อมูลจาก KB
         ↓
    Response to User
```

**ทำไม Multi-Agent?**
- แต่ละ domain มี knowledge base ต่างกัน
- Context ไม่ปนกัน → ตอบแม่นกว่า
- ขยายผลได้ง่าย (เพิ่ม agent ใหม่ไม่กระทบ agent อื่น)

---

## RAG (Retrieval-Augmented Generation) คืออะไร?

LLM ตอบจาก training data → ไม่รู้ข้อมูลเฉพาะของ PEA

RAG แก้ปัญหานี้:

```
คำถาม: "ค่าไฟเดือนนี้ทำไมแพง?"
    ↓
1. Embed คำถาม → vector
2. ค้น vector DB → เจอ document ที่เกี่ยวข้อง
3. ส่ง context + คำถาม → LLM
4. LLM ตอบโดยใช้ context จริง
```

---

## Tools ที่ Agent ใช้

```python
tools = [
    search_knowledge_base,    # RAG ค้น KB
    get_complaint_status,     # ดูสถานะแจ้งซ่อม (จาก 1129 data)
    calculate_electricity_bill,  # คำนวณค่าไฟ
    create_service_request,   # สร้างคำขอบริการใหม่
]
```

---

## Stack

| Component | Tool |
|-----------|------|
| LLM | Claude API (claude-haiku-4-5) |
| Embedding | `sentence-transformers` |
| Vector DB | ChromaDB (local, ไม่ต้อง deploy) |
| Agent Framework | LangChain |
| API Server | FastAPI (optional) |

---

## Learning Path (notebook นี้)

1. **Setup** — install LangChain, ChromaDB, sentence-transformers
2. **Knowledge Base** — สร้าง sample KB จาก text files
3. **RAG Pipeline** — embed → store → retrieve → generate
4. **Tools** — สร้าง custom tools
5. **Router Agent** — classify intent + route
6. **End-to-End Test** — ทดสอบด้วยชุดคำถาม
7. **Evaluation** — วัด accuracy ของการตอบ
