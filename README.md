# 🌍 River Plastic Contribution Classifier

This project uses supervised machine learning to classify rivers as **high** or **low** plastic contributors to ocean pollution, based on geographic and environmental features. The classification helps prioritize cleanup efforts, especially for rivers in developing regions where waste management infrastructure is limited.

---

## 📌 Project Objective

The goal is to predict whether a river is a **high plastic contributor** based on features like:
- Area
- Rainfall
- Coastline length
- Waste management indicators
- Slope and precipitation factors

### 🎯 Target Label:
- A binary column `plastic_contribution` is created from the column `M[E] (metric tons year -1)`
  - If `M[E]` > 6008 → label = `0` (Low Priority)
  - Else → label = `1` (High Priority)

🚨 **Important**: Although `M[E]` is used to define the label, it is **excluded from model training** to simulate real-world prediction when that data may not be available.

---

## 📦 Dataset Features

Each row represents a country or river basin, with the following features:

| Feature                      | Description                            |
|-----------------------------|----------------------------------------|
| `Area [km2]`                | Size of the country/region             |
| `Coast length [km]`         | Length of coastline                    |
| `Rainfall [mm year -1]`     | Annual rainfall                        |
| `Factor L/A [-]`            | Terrain slope factor                   |
| `Factor (L/A) *P [-]`       | Slope × population indicator           |
| `P[E] [%]`                  | Population exposed to riverine plastic |
| `MPW (metric tons year -1)` | Mismanaged plastic waste               |
| `Ratio Me/MPW`              | Emission-to-waste ratio                |

📁 **Dataset Link**: [Download CSV on Google Drive](https://drive.google.com/file/d/1zIk9JOdJEu9YF7Xuv2C8f2Q8ySfG3nHd/view?usp=drive_link)

---

## ⚙️ Tools & Technologies

- Python (3.x)
- [Scikit-learn](https://scikit-learn.org/)
- Pandas & NumPy
- Matplotlib & Seaborn (for visualization)
- Google Colab or Jupyter Notebook

---

## 🧪 ML Pipeline

### 1. Data Cleaning
- Removed non-numeric characters (e.g., `'`, `%`, `,`)
- Converted all columns to numeric
- Dropped rows with missing values

### 2. Feature Engineering
- Created the target column `plastic_contribution` using a threshold on `M[E]`
- Dropped `M[E]` and non-predictive columns (`Country or Administrative area`) from training features

### 3. Model Training
Used **Random Forest Classifier** (`RandomForestClassifier`) due to its:
- Robustness to non-linear relationships
- No need for feature scaling
- Built-in support for feature importance visualization
- Strong performance on tabular, structured datasets

```python
from sklearn.ensemble import RandomForestClassifier

model = RandomForestClassifier(random_state=42)
model.fit(X_train, y_train)
