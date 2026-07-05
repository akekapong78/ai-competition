# Week 1: Enhance Renewable Forecasting

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR_GITHUB/ai-competition/blob/main/01-forecasting/forecasting_xgboost.ipynb)

---

## โจทย์การแข่งขัน

DSO (Distribution System Operator) ต้องบริหารโครงข่ายไฟฟ้าแบบ real-time แต่พยากรณ์กำลังการผลิต Solar/Wind ไม่แม่น → เกิด inbalance ในระบบ

**Task:** รับ time series ที่มีช่องว่าง (missing values) → เติมค่ากำลังการผลิตให้ถูกต้อง

---

## ทำไม XGBoost ไม่ใช้ ARIMA หรือ LSTM?

| Model | ข้อดี | ข้อเสีย |
|-------|-------|---------|
| ARIMA | เข้าใจง่าย, interpretable | จัดการ multiple seasonality ยาก |
| LSTM | จับ pattern ซับซ้อนได้ | ต้องการ data เยอะ, tune ยาก, overfit ง่าย |
| **XGBoost** | **เร็ว, robust, ไม่ต้อง normalize** | ต้องทำ feature engineering เอง |

XGBoost ชนะ competition time series หลายรายการ เพราะ feature engineering ที่ดีสำคัญกว่า model ที่ซับซ้อน

---

## Concept หลัก

### Time Series = ข้อมูลที่มีลำดับเวลา

```
เวลา:  00:00  01:00  02:00  ...  12:00  ...  23:00
Solar:  0      0      0    ...   500   ...    0
Wind:  120    115    130   ...   200   ...   180
```

**Pattern ของ Solar:**
- กลางวัน (8:00-17:00) → มีค่า ตามมุมดวงอาทิตย์
- กลางคืน → 0 เสมอ
- ฤดูฝน → ต่ำกว่าฤดูแล้ง

**Pattern ของ Wind:**
- ไม่มี pattern ชัดเจนเหมือน Solar
- มี weekly pattern บางส่วน
- ต้องใช้ lag ยาวกว่า

---

## Feature Engineering คืออะไร?

XGBoost ต้องการ "features" (คอลัมน์) ที่อธิบาย pattern ให้ model เรียนรู้

### Time Features (บอก "ตอนนี้อยู่ช่วงไหน")
```python
df['hour']         = df.index.hour          # 0-23
df['day_of_week']  = df.index.dayofweek     # 0=จันทร์, 6=อาทิตย์
df['month']        = df.index.month         # 1-12
df['is_weekend']   = df['day_of_week'] >= 5
```

### Lag Features (บอก "ก่อนหน้านี้ค่าเท่าไหร่")
```python
df['lag_1h']   = df['power'].shift(1)    # 1 ชั่วโมงที่แล้ว
df['lag_24h']  = df['power'].shift(24)   # เมื่อวานนี้เวลาเดียวกัน
df['lag_168h'] = df['power'].shift(168)  # สัปดาห์ที่แล้วเวลาเดียวกัน ← สำคัญมาก
```

### Rolling Features (บอก "ค่าเฉลี่ยช่วงที่ผ่านมาเท่าไหร่")
```python
df['rolling_mean_24h'] = df['power'].rolling(24).mean()
df['rolling_std_24h']  = df['power'].rolling(24).std()
```

### Solar-specific Features
```python
# Solar angle — Solar ผลิตได้มากเมื่อดวงอาทิตย์สูง
df['solar_angle'] = np.sin(2 * np.pi * df['hour'] / 24)
df['is_daylight'] = (df['hour'] >= 6) & (df['hour'] <= 18)
```

---

## Evaluation Metrics

```python
from sklearn.metrics import mean_absolute_error, mean_squared_error
import numpy as np

MAE  = mean_absolute_error(y_true, y_pred)        # ค่าเฉลี่ยความผิดพลาด (MW)
RMSE = np.sqrt(mean_squared_error(y_true, y_pred)) # ลงโทษ error ใหญ่มากกว่า
MAPE = np.mean(np.abs((y_true - y_pred) / y_true)) * 100  # % ผิดพลาด
```

ยิ่งต่ำยิ่งดี — competition วัด accuracy → ต้องการ RMSE/MAE ต่ำ

---

## โครงสร้าง Notebooks

```
01-forecasting/
├── xgboost-timeseries/              ← Main approach (แนะนำ)
│   ├── mini_example.ipynb           รันครบใน 2 นาที — ทดสอบ pipeline
│   ├── full_tutorial.ipynb          สอนละเอียดทุก step
│   └── feature_model_techniques.ipynb  SHAP, Optuna, LightGBM, Fourier
└── alternative-methods/             ← วิธีอื่นที่ไม่ใช้ lag
    └── notebook.ipynb               Interpolation, Prophet, KNN, MLP, SVR
```

## เริ่มจากไหนดี?

```
ใหม่กับ forecasting     → xgboost-timeseries/mini_example.ipynb
เรียนรู้ครบถ้วน          → xgboost-timeseries/full_tutorial.ipynb
เทคนิค feature/model    → xgboost-timeseries/feature_model_techniques.ipynb
วิธีอื่นนอกจาก XGBoost  → alternative-methods/notebook.ipynb
```

---

## เมื่อได้ Data จริงจาก PEA

ต้องทำเพิ่ม:
- ดู format ของ data (resolution: 15 นาที? 1 ชั่วโมง?)
- Handle missing values ใน training data
- ตรวจสอบ outliers (maintenance shutdowns)
- เพิ่ม features ตาม domain knowledge (วันหยุดราชการ, ฤดูกาล)
