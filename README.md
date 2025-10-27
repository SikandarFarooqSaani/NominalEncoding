# 🤖 This README is AI Generated (Custom Prompt) 😊  
*For reader clarity and my own ease of documentation.*

---

# 🧠 Understanding One-Hot Encoding and Handling Many Categories

## 📦 Libraries Used
- numpy  
- pandas  
- sklearn (OneHotEncoder)  

---

## 📊 Dataset
- Dataset is available in the **repo**.  
- The dataset contains categorical columns such as **Brand**, **Fuel**, and **Owner**.  
- The **Brand** column has **32 unique categories**, which makes direct encoding inefficient.

---

## ⚙️ Objective
When a column contains **too many categories**, encoding each one separately increases feature space unnecessarily and may lead to **overfitting** or **sparsity**.  
To handle this:
- Keep the **most frequent categories**.  
- Group **less frequent categories** into a single class — **“Other”**.

---

## 🧩 Steps Performed

### 1️⃣ Data Preparation
- Read dataset from repo.  
- Identified columns with **too many categories** (e.g., `Brand`).  
- Decided to **group less frequent categories** into `"Other"`.  
  ```python
  threshold = 10  # Example threshold
  value_counts = df['Brand'].value_counts()
  df['Brand'] = df['Brand'].apply(lambda x: x if value_counts[x] > threshold else 'Other')




