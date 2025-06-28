# 🌍 River Plastic Contribution Classifier

This project leverages **Random Forest Classification** to identify rivers with high or low plastic contribution to ocean pollution using environmental and geographical features.

---

## 🔖 Objective

To classify rivers as either:

* **High Plastic Contributor (1)**: Annual plastic emission $`M[E]`$ <= 6008 metric tons
* **Low Plastic Contributor (0)**: $`M[E]`$ > 6008 metric tons

> This threshold aligns with findings from **The Ocean Cleanup** and peer-reviewed literature.

---

## 🌐 Dataset

* Source: [The Ocean Cleanup - 1000 Rivers Study](https://theoceancleanup.com/press/press-releases/1000-rivers-emit-nearly-80-of-riverine-plastic-pollution-into-worlds-oceans-newly-published-research-shows/)
* CSV Access: [Google Drive Dataset](https://drive.google.com/file/d/1zIk9JOdJEu9YF7Xuv2C8f2Q8ySfG3nHd/view?usp=drive_link)

Each row represents a river basin or country with:

| Feature                      | Description                                            |
| ---------------------------- | ------------------------------------------------------ |
| `Area [km2]`                 | Total area of region                                   |
| `Coast length [km]`          | Coastline distance                                     |
| `Rainfall [mm year -1]`      | Annual rainfall                                        |
| `Factor L/A [-]`             | Slope to area ratio                                    |
| `Factor (L/A) *P [-]`        | Weighted slope indicator                               |
| `P[E] [%]`                   | Population exposure to plastic flow                    |
| `MPW (metric tons year -1)`  | Mismanaged plastic waste                               |
| `M[E] (metric tons year -1)` | Plastic emission (used for target label, not training) |
| `Ratio Me/MPW`               | Emission-to-waste ratio                                |

---

## 📊 Methodology

### 1. **Data Preprocessing**

* Removed apostrophes, percentage symbols
* Converted all numeric strings to float
* Dropped rows with missing `Coast`, `Rainfall`, or `M[E]` data
* Created binary target column: `plastic_contribution`

### 2. **Feature Selection**

Features used for model training:

* `Area [km2]`
* `Coast length [km]`
* `Rainfall [mm year -1]`
* `MPW (metric tons year -1)`
* `P[E] [%]`
* `Factor (L/A) *P [-]`

**Note:** `M[E]` is excluded from training to avoid label leakage.

### 3. **Scaling**

* Applied `RobustScaler` to reduce influence of outliers

### 4. **Model Training**

* Classifier: `RandomForestClassifier`
* Parameters:

  * `n_estimators=500`
  * `max_depth=10`
  * `class_weight='balanced'`
  * `min_samples_leaf=5`

### 5. **Evaluation Metrics**

* **Accuracy**
* **Precision**
* **Recall**
* **Confusion Matrix**
* **AUC / ROC Curve**
* **Feature Importance Plot**
* **Correlation Heatmap**


### 🌟 Top Predictive Features

* Mismanaged Plastic Waste (MPW)
* Rainfall
* Coastline Length

---

## 📊 Visual Outputs

* Bar chart of river class distribution
* Confusion matrix heatmap
* ROC curve
* Feature importance plot
* Correlation with target (heatmap)

---

## 🌞 Insights

* Many high contributors are **not the largest rivers** but coastal and tropical regions with high rainfall and poor waste infrastructure
* Proper feature selection and scaling can yield strong classification accuracy even with limited features

---

## ⚡ Future Work

* Include geographic proximity to coastline
* Use ensemble models for boosted results
* Integrate satellite data for real-time plastic flow monitoring

---

## 📚 References

* [Science Advances 2021 - 1000 Rivers Study](https://www.science.org/doi/10.1126/sciadv.aaz5803)
* [The Ocean Cleanup: 1000 Rivers Initiative](https://theoceancleanup.com/1000rivers)

---

## 🤖 Maintainer

* Project by: **Gebru Meresu**
* For academic, environmental and educational use.

---

> “Solving the plastic crisis starts with knowing where it enters the ocean. This model brings us one step closer.” — *The Ocean Cleanup*
