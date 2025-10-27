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
### 2️⃣ Train-Test Split

Performed train-test split to ensure model evaluation consistency.

### 3️⃣ Applying One-Hot Encoding (OHE)

Pandas’ get_dummies() can perform OHE but does not store encoding references, so sklearn’s OneHotEncoder is preferred.

Created OHE object:

from sklearn.preprocessing import OneHotEncoder
ohe = OneHotEncoder(drop='first', sparse=False)


drop='first': Drops the first column of each feature to avoid dummy variable trap (which causes multicollinearity).

sparse=False: Ensures output is a dense array, making it easier to convert into a DataFrame.

### 4️⃣ Encoding Specific Columns

Fit and transform categorical columns such as Fuel and Owner:

encoded = ohe.fit_transform(df[['Fuel', 'Owner']])
encoded_df = pd.DataFrame(encoded, columns=ohe.get_feature_names_out(['Fuel', 'Owner']))


Concatenated the encoded DataFrame with the rest of the dataset.

### 📈 Key Takeaways

Use OneHotEncoder when you need consistent encoding between train and test data.

Always drop the first column to prevent multicollinearity.

When categories are too many, use a frequency threshold and group rare categories into “Other” to simplify encoding and improve performance



