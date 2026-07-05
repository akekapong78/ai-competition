# AI Competition — Claude Code Instructions

## Project Overview

PEA AI Competition ครั้งที่ 13 ปี 2569  
แข่ง 8-9 กันยายน 2569 ที่ ศฝฟ. นครชัยศรี

## Structure

```
01-forecasting/   ← XGBoost time series (Wind/Solar)
02-image-processing/ ← YOLO object detection/classification
03-agentic-ai/    ← RAG + multi-agent customer service
04-pitching/      ← presentation content
```

## Tech Stack

- **Forecasting:** Python, XGBoost, pandas, scikit-learn
- **Image:** ultralytics YOLO (latest), PyTorch
- **Agentic AI:** LangChain, ChromaDB, Anthropic Claude API
- **Runtime:** Google Colab (GPU) + local VS Code via remote extension

## Conventions

- Notebooks run on Colab — keep GPU-optional (fallback to CPU)
- Each notebook is self-contained — no cross-notebook imports
- Use synthetic/public datasets until PEA data arrives (~8 Aug 2569)
- Submission pipeline functions go at the bottom of each notebook

## Competition Day Notes

- Day 1 (8 ก.ย.): run models, submit results before 16:30
- Day 2 (9 ก.ย.): pitching 8 min + Q&A 7 min
- Bring own laptop (join domain pea.co.th)
