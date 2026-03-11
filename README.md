# Vendor Invoice Intelligence System

**AI-Driven Freight Cost Prediction & Invoice Risk Flagging**

---
## 📌 Table of Contents

- [Project Overview](#-project-overview)
- [Business Objectives](#-business-objectives)
- [Data Source](#-data-source)
- [Exploratory Data Analysis](#-exploratory-data-analysis)
- [Models Used](#-models-used)
- [Evaluation Metrics](#-evaluation-metrics)
- [Application](#-application)
- [Application Preview](#application-preview)
- [Project Architecture](#-project-architecture)
- [Project Structure](#-project-structure)
- [How to Run This Project](#-how-to-run-this-project)
- [Author & Contact](#-author)
---

## 📌 Project Overview

The **Vendor Invoice Intelligence System** is an end-to-end machine learning application that helps finance teams analyze vendor invoices and detect potential financial risks.

The system performs two main tasks:

1. **Freight Cost Prediction** – Estimate expected freight cost for vendor invoices.  
2. **Invoice Risk Flagging** – Automatically identify invoices that may require manual approval due to abnormal patterns.

The models are deployed through an **interactive Streamlit web application**.

Business benefits:

- Detect abnormal invoices early  
- Reduce financial leakage  
- Improve operational efficiency  
- Support faster finance workflows  

---

# 🎯 Business Objectives

## 1️⃣ Freight Cost Prediction (Regression)

**Goal:**  
Predict expected freight cost based on invoice value.

**Business Value**

- Detect freight overcharging
- Improve vendor negotiations
- Improve cost forecasting

Example:

Invoice Value: **$18,500**  
Predicted Freight: **$1,120**

If the billed freight is significantly higher, the invoice may require investigation.

---

## 2️⃣ Invoice Manual Approval Flagging (Classification)

**Goal:**  
Automatically detect invoices that may contain anomalies and require manual review.

The system flags invoices when unusual patterns appear such as:

- Invoice amount mismatch with purchase totals
- Unusual freight ratios
- Suspicious quantity patterns

Example:

Invoice Amount: **$2,468**  
Purchase Total: **$2,476**  
Difference: **$8 → flagged**

This helps finance teams **prioritize risky invoices** before payment.

---

# 📊 Data Source

The project uses data stored in a **SQLite database (`inventory.db`)**.

### Vendor Invoice Data

Includes:

- Invoice quantity
- Invoice dollars
- Freight cost
- Invoice date
- Purchase order reference

### Purchase Data

Includes:

- Purchase quantities
- Purchase dollars
- Receiving delays
- Brand counts

Purchase data is aggregated to generate **invoice-level features**.

---

# 🔍 Exploratory Data Analysis

EDA was performed using **Jupyter notebooks**.

Key insights:

### Freight Patterns
Freight costs strongly correlate with **invoice value**.

### Invoice vs Purchase Difference

Invoices where

`|invoice_dollars - total_item_dollars| > 5`

frequently required manual review.

### Important Features

- `invoice_quantity`
- `invoice_dollars`
- `freight`
- `total_item_quantity`
- `total_item_dollars`

---

# 🧠 Models Used

The system uses **two machine learning pipelines**.

---

## Freight Cost Prediction

Problem type: **Regression**

Models trained:

- Linear Regression
- Decision Tree Regressor
- Random Forest Regressor

The best model is selected using **lowest MAE**.

Saved model:

`predict_freight_model.pkl`

---

## Invoice Risk Flagging

Problem type: **Binary Classification**

Model used:

**Random Forest Classifier**

Saved artifacts:

- `predict_flag_invoice.pkl`
- `scaler.pkl`

---

# 📈 Evaluation Metrics

## Freight Prediction

Metrics:

- MAE
- RMSE
- R² Score

Example results:

Linear Regression Performance

MAE : 24.11  
RMSE : 124.72  
R² : 96.99%

---

## Invoice Risk Detection

Metrics:

- Accuracy
- Precision
- Recall
- F1 Score

Example:

Accuracy: **0.89**  
F1 Score: **0.87**

---

# 💻 Application

The models are deployed through a **Streamlit web application**.

The portal contains two modules.

---

## 🚚 Freight Cost Prediction

User inputs:

- Invoice Quantity
- Invoice Dollars

Output:

**Predicted Freight Cost**

---

## ⚠ Invoice Risk Prediction

User inputs:

- Invoice Quantity
- Invoice Dollars
- Freight Cost
- Total Item Quantity
- Total Item Dollars

Output:

- **Safe for Auto Approval**
- **Manual Approval Required**

The application also displays **model confidence**.

---

## Application Preview

### Vendor Invoice Intelligence Portal

![Application Home](images/app_home.png)

### Freight Cost Prediction

![Freight Prediction](images/freight_prediction.png)

### Invoice Risk Flagging

![Invoice Risk](images/invoice_risk.png)

---

# 🏗 Project Architecture

```
Database
   ↓
Data Preprocessing
   ↓
Feature Engineering
   ↓
Model Training
   ↓
Model Evaluation
   ↓
Model Serialization (PKL)
   ↓
Inference Layer
   ↓
Streamlit Web Application
```

---

# 📁 Project Structure

```
Vendor-invoice-intelligence-system
│
├── Data/
│   └── inventory.db
│
├── freight_cost_prediction/
│   ├── data_preprocessing.py
│   ├── modeling_evaluation.py
│   ├── train.py
│   └── models/
│       └── predict_freight_model.pkl
│
├── invoice_flagging/
│   ├── data_preprocessing.py
│   ├── modeling_evaluation.py
│   ├── train.py
│   └── models/
│       ├── predict_flag_invoice.pkl
│       └── scaler.pkl
│
├── inference/
│   ├── predict_freight.py
│   └── predict_invoice_flag.py
│
├── notebooks/
│   ├── invoice_flagging.ipynb
│   └── Predicting_Freight_Cost.ipynb
│
├── images/
│   ├── app_home.png
│   ├── freight_prediction.png
│   └── invoice_risk.png
│
├── app.py
├── requirements.txt
└── README.md
```

---

# ▶ How to Run This Project

## 1️⃣ Clone repository

```
git clone https://github.com/yourusername/vendor-invoice-intelligence-system.git
cd vendor-invoice-intelligence-system
```

---

## 2️⃣ Create virtual environment

```
python -m venv venv
```

Activate environment

Windows:

```
venv\Scripts\activate
```

Mac/Linux:

```
source venv/bin/activate
```

---

## 3️⃣ Install dependencies

```
pip install -r requirements.txt
```

---

## 4️⃣ Train models

```
python freight_cost_prediction/train.py
```

```
python invoice_flagging/train.py
```

This generates:

- `predict_freight_model.pkl`
- `predict_flag_invoice.pkl`
- `scaler.pkl`

---

## 5️⃣ Run the application

```
streamlit run app.py
```

Application will run at:

```
http://localhost:8501
```

---

# 👤 Author

**Mayuresh Ahire**

Data Analyst | Machine Learning | Business Intelligence

Skills:

- Python
- SQL
- Machine Learning
- Power BI
- Tableau
- Data Analytics

LinkedIn: https://www.linkedin.com/in/mayuresh-ahire-ab079b2a3/