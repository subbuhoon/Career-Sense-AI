# Career Sense AI 🎓

> **Predictive Placement & Salary Estimation using Machine Learning**

Career Sense AI is a machine learning system that predicts whether a student will be placed and estimates their expected salary — based on academic performance, skills, and other attributes. It combines a **Random Forest Classifier**, a **Genetic Algorithm for feature selection**, and a **feedback-based adaptive mechanism** into one end-to-end pipeline.

---

## 🚀 Demo

> Run on Google Colab — no local setup needed.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/)

---

## 📌 Features

- ✅ Predicts **placement status** (Placed / Not Placed)
- ✅ Estimates **expected salary** when salary data is available
- ✅ Uses a **Genetic Algorithm** to automatically select the best features
- ✅ Includes a **feedback mechanism** that adjusts feature weights after each prediction
- ✅ Fully runnable in **Google Colab** — just upload your dataset and go

---

## 🧠 How It Works

```
Student Dataset
      │
      ▼
Data Preprocessing & Encoding
      │
      ▼
Random Forest Baseline Classifier
      │
      ▼
Genetic Algorithm — Feature Selection
      │
      ▼
Optimized Feature Set
      │                │
      ▼                ▼
RF Classifier     RF Regressor
(Placement)        (Salary)
      │
      ▼
Feedback → Feature Weight Update
```

### Pipeline Steps

| Step | Description |
|------|-------------|
| **1. Preprocessing** | Load data, remove IDs, encode categoricals, train/test split |
| **2. Baseline Model** | Train a Random Forest on all features |
| **3. Feature Selection** | Genetic Algorithm finds the best feature subset |
| **4. Optimized Model** | Retrain Random Forest on selected features |
| **5. Salary Model** | Train a Random Forest Regressor (if salary column exists) |
| **6. Prediction** | Predict placement + estimate salary for new candidates |
| **7. Feedback** | User marks prediction correct/wrong → weights update |

---

## ⚙️ Genetic Algorithm Details

Each individual in the population is a **binary chromosome** representing which features to include:

```
[1, 0, 1, 1, 0, 1]
 ↑        ↑
selected  excluded
```

| Parameter | Value |
|-----------|-------|
| Population Size | 10 |
| Generations | 5 |
| Cross-Validation | 3-Fold |
| Selection | Top 5 individuals |
| Crossover | Single-point |
| Mutation | Random bit flip |

---

## 🔄 Feedback Mechanism

After each prediction, the user provides feedback:

```
correct   →  feature weights increase slightly
wrong     →  feature weights decrease slightly
```

- Initial weight per feature: `1.0`
- Learning rate: `0.05`

> ⚠️ This is a lightweight adaptive mechanism, not a full reinforcement learning system.

---

## 📂 Project Structure

```
Career-Sense-AI/
│
├── 366Project.ipynb      # Main notebook
├── README.md             # Project documentation
└── requirements.txt      # Python dependencies
```

---

## 🛠️ Tech Stack

| Technology | Purpose |
|------------|---------|
| Python | Core language |
| Pandas | Data loading & manipulation |
| NumPy | Numerical operations & GA logic |
| Scikit-learn | ML models & evaluation |
| Google Colab | Development environment |

---

## 📦 Installation

```bash
git clone https://github.com/subbuhoon/Career-Sense-AI.git
cd Career-Sense-AI
pip install -r requirements.txt
```

---

## ▶️ Running the Project

### Option 1 — Google Colab (Recommended)

1. Open `366Project.ipynb` in Google Colab
2. Run all cells from top to bottom
3. Upload your dataset when prompted
4. View placement predictions and salary estimates
5. Provide feedback when asked

### Option 2 — Local Jupyter

```bash
pip install -r requirements.txt
jupyter notebook 366Project.ipynb
```

Run cells sequentially.

---

## 📊 Input Features

The model uses the following encoded attributes:

- `Gender`
- `Branch`
- `Programming_Skills`
- `Aptitude_Score`
- `Communication_Skills`
- `Placement_Status` *(target)*
- `Salary_Offered_USD` *(optional — for salary prediction)*

> The dataset is not included in this repository. Bring your own placement dataset in CSV format.

---

## ⚠️ Limitations

- Salary prediction requires a `Salary_Offered_USD` column in the dataset
- No regression metrics (MAE, RMSE, R²) are currently calculated
- The feedback system is simplified — not a true RL implementation
- Model performance depends heavily on dataset size and quality
- Does not recommend specific job roles

---

## 🔮 Future Improvements

- [ ] Add a job recommendation engine based on candidate skills
- [ ] Include classification and regression evaluation metrics
- [ ] Compare multiple ML algorithms (XGBoost, SVM, etc.)
- [ ] Upgrade the Genetic Algorithm with advanced evolutionary strategies
- [ ] Build an interactive web app (Streamlit or Flask)
- [ ] Integrate real-time job market data
- [ ] Replace the feedback mechanism with proper reinforcement learning

---

## 👤 Author

**Rahma Kamal**
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin)](https://www.linkedin.com/in/rahma-kamal-228766439)
[![GitHub](https://img.shields.io/badge/GitHub-subbuhoon-black?logo=github)](https://github.com/subbuhoon)

---

## 📄 License

This project is intended for **educational and portfolio purposes** only.
