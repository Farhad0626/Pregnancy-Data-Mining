# 🤰 Pregnancy Risk Prediction

### Data Mining for High-Risk Pregnancy Identification


> An educational data mining project exploring maternal health data, classification models, and their ability to identify high-risk pregnancies.

> [!IMPORTANT]
> **This project is for educational and research purposes only.**
>
> Model predictions are **not medical diagnoses or clinical recommendations**. The models have not been clinically validated and must not be used to make decisions about real patients.

---

## 📌 Overview

Early identification of high-risk pregnancies is an important problem in maternal healthcare.

This project explores how machine learning can be used to classify pregnancy risk using clinical characteristics and maternal health information recorded in the dataset.

The target variable is `Risk Level`, with two classes:

* 🔴 `High` — High-risk pregnancy
* 🟢 `Low` — Low-risk pregnancy

The project follows the **CRISP-DM (Cross-Industry Standard Process for Data Mining)** methodology:

```text
Business Understanding
        ↓
Data Understanding
        ↓
Data Preparation
        ↓
Modeling
        ↓
Evaluation
```

A major focus of the project is that **accuracy alone is not enough**. In a risk-screening scenario, failing to identify a genuinely high-risk case may be more important than generating an additional false alarm.

Therefore, **High-risk Recall** is used as the primary model selection metric.

---

## 🎯 Project Goals

The main objectives are to:

* 🔎 Explore and understand maternal health data
* 🧹 Clean and preprocess the dataset
* 🛠️ Perform feature engineering
* 🤖 Train and compare classification models
* 📊 Evaluate models using multiple performance metrics
* 🚨 Prioritize the detection of high-risk cases
* 🔬 Investigate the impact of data leakage
* 📈 Analyze classification errors
* 🧪 Build a reproducible machine learning workflow

---

## 🧭 Project Workflow

| Stage                     | Notebook                                                                                    | Description                                                            |
| ------------------------- | ------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| 🧠 Business Understanding | [`Business_Understanding.ipynb`](000_Business%20Understanding/Business_Understanding.ipynb) | Defines the problem, objectives, and success criteria                  |
| 🔍 Data Understanding     | [`Data_Understanding.ipynb`](001_Data%20Understanding/Data_Understanding.ipynb)             | Explores features, distributions, relationships, and data quality      |
| 🧹 Data Preparation       | [`Data_Preparation.ipynb`](002_Data%20Preparation/Data_Preparation.ipynb)                   | Cleans data, performs feature engineering, and creates train/test sets |
| 🤖 Modeling               | [`Modeling.ipynb`](003_Modeling/Modeling.ipynb)                                             | Trains, compares, and tunes classification models                      |
| 📊 Evaluation             | [`Evaluation.ipynb`](004_Evaluation/Evaluation.ipynb)                                       | Evaluates performance, analyzes errors, and investigates data leakage  |

---

## 🤖 Machine Learning Models

The project compares four classification algorithms:

* **Logistic Regression**
* **Decision Tree**
* **Random Forest**
* **Gradient Boosting**

Model selection and hyperparameter tuning are performed using **5-fold Stratified Cross-Validation**.

The primary optimization metric is:

> **Recall for the `High` risk class**

This reflects the project's focus on identifying as many genuinely high-risk cases as possible.

---

## 🚨 Why High-Risk Recall?

In a standard classification problem, accuracy can be a useful metric.

However, for risk screening, different types of errors may have different consequences.

| Actual | Predicted | Result                                |
| ------ | --------- | ------------------------------------- |
| High   | High      | ✅ Correctly identified high-risk case |
| Low    | Low       | ✅ Correct classification              |
| Low    | High      | ⚠️ False positive                     |
| High   | Low       | 🚨 False negative                     |

The last case represents a **missed high-risk pregnancy**.

### Recall

Recall is calculated as:

```text
Recall = True Positives / (True Positives + False Negatives)
```

It measures the proportion of actual high-risk cases that the model successfully identifies.

For this reason, the project prioritizes **High-risk Recall** instead of relying solely on overall accuracy.

---

## ⚠️ Data Leakage

An important part of this project is investigating the effect of **data leakage** on model performance.

Two feature configurations are evaluated.

### 🔒 `no_leakage`

Uses features considered more appropriate for prediction at the intended screening stage.

### ⚡ `with_leakage`

Includes additional features that may contain information obtained later in the pregnancy or after a clinical event.

This comparison demonstrates how information that would not necessarily be available at prediction time can artificially improve model performance.

For example, `Gestational Diabetes` may be present in the dataset, but its diagnosis could occur after the intended early prediction point.

> **Important:** Performance obtained with potentially leaked features should not be interpreted as deployable real-world performance.

The leakage experiment is included primarily for educational and analytical purposes.

---

## 📊 Current Results

According to the current evaluation notebook, **Gradient Boosting** is the selected model for both feature configurations.

For the **`no_leakage`** test set:

| Metric                   |      Result |
| ------------------------ | ----------: |
| 🎯 Accuracy              |   **95.8%** |
| 🚨 High-risk Recall      |   **89.5%** |
| ⚖️ F1 Score              |   **94.4%** |
| 📈 ROC-AUC               |   **99.9%** |
| ❌ Missed High-risk Cases | **10 / 95** |

### Key Observation

The model achieves strong overall classification performance, but its **89.5% High-risk Recall** is still below the project's predefined **95% target**.

This highlights an important point:

> **High accuracy does not necessarily mean that a model is sufficiently effective at detecting high-risk cases.**

These results are specific to the current dataset and test split. They do not guarantee similar performance on independent datasets or different populations.

---

## 📏 Evaluation Metrics

The project evaluates models using several complementary metrics:

| Metric               | Purpose                                                             |
| -------------------- | ------------------------------------------------------------------- |
| **Accuracy**         | Overall proportion of correct predictions                           |
| **Precision**        | Proportion of predicted high-risk cases that are actually high-risk |
| **Recall**           | Proportion of actual high-risk cases detected                       |
| **F1 Score**         | Balance between precision and recall                                |
| **ROC-AUC**          | Measures discrimination across classification thresholds            |
| **Confusion Matrix** | Provides a detailed view of classification errors                   |

The primary metric remains:

### 🚨 High-risk Recall

because false negatives are particularly important in a risk-screening context.

---

## 📂 Dataset & Outputs

### Raw Dataset

```text
data/Pregnancy.csv
```

The original dataset used in the project.

### Prepared Dataset

```text
data/pregnancy_prepared.csv
```

The cleaned and transformed dataset generated during data preparation.

### Train/Test Datasets

```text
data/pregnancy_train_*.csv
data/pregnancy_test_*.csv
```

Training and test datasets generated for the different feature configurations.

### Model Outputs

Generated models and evaluation artifacts are stored under:

```text
003_Modeling/
```

These generated files are excluded from version control through `.gitignore`.

To recreate them, run the notebooks in the appropriate order.

---

## 🚀 Getting Started

### Requirements

* Python 3.x
* JupyterLab or Jupyter Notebook
* pip

### Install Dependencies

```bash
python -m pip install jupyterlab numpy pandas matplotlib seaborn scikit-learn joblib
```

### Start JupyterLab

From the repository root:

```bash
jupyter lab
```

Then run the notebooks in this order:

```text
000_Business Understanding
        ↓
001_Data Understanding
        ↓
002_Data Preparation
        ↓
003_Modeling
        ↓
004_Evaluation
```

> **Note:** The notebooks use relative paths. Run each notebook with its corresponding directory as the working directory when required.

---

## 🗂️ Repository Structure

```text
.
├── 000_Business Understanding/
│   └── Business_Understanding.ipynb
│
├── 001_Data Understanding/
│   └── Data_Understanding.ipynb
│
├── 002_Data Preparation/
│   └── Data_Preparation.ipynb
│
├── 003_Modeling/
│   └── Modeling.ipynb
│
├── 004_Evaluation/
│   └── Evaluation.ipynb
│
├── 005_Deployment/
│
├── data/
│   └── Pregnancy.csv
│
├── .gitignore
├── LICENSE
└── README.md
```

---

## 🔬 Future Work

Potential directions for extending the project include:

* 🧪 Validation on independent datasets
* 🌍 Evaluation across different populations
* 🔍 Deeper analysis of false negatives
* ⚖️ Class imbalance analysis
* 🎚️ Classification threshold optimization
* 📊 Probability calibration
* 🔐 Fairness and bias analysis
* 🔄 Stability analysis across multiple train/test splits
* 🚀 Development of a reproducible deployment pipeline after proper validation

Any real-world clinical application would require additional validation, appropriate governance, and clinical oversight.

---

## 🤝 Contributing

Contributions are welcome.

If you find a bug, have an idea, or want to improve the analysis:

1. Open an **Issue**
2. Describe the problem or proposed improvement
3. Submit a **Pull Request**

Areas such as independent validation, error analysis, responsible machine learning, and reproducibility are particularly valuable.

---

## 📄 License

This project is released under the **MIT License**.

See [`LICENSE`](LICENSE) for more information.

---

⭐ **If you find this project useful, consider giving it a star!**

> Built for learning, experimentation, and responsible exploration of machine learning in healthcare.
