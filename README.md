# Career Sense AI

### Predictive Placement & Salary Prediction System

Career Sense AI is a machine learning system designed to analyze student attributes and predict placement outcomes while estimating expected salary. The project combines **Random Forest**, **Genetic Algorithm-based feature selection**, and a **feedback-driven feature adjustment mechanism** into a single predictive workflow.

## Overview

The system takes candidate attributes such as academic performance, programming skills, aptitude, communication skills, and other encoded features to generate a placement prediction.

The workflow consists of four main components:

* **Placement Classification** — Random Forest Classifier
* **Feature Selection** — Custom Genetic Algorithm
* **Salary Estimation** — Random Forest Regressor
* **Adaptive Feedback** — Feature-weight adjustment based on prediction feedback

The Genetic Algorithm searches through different feature combinations and evaluates them using cross-validation before selecting a feature subset for the final placement model.

## System Architecture

```text
                    Student Dataset
                          │
                          ▼
                 Data Preprocessing
                          │
                          ▼
                Categorical Encoding
                          │
                          ▼
              ┌──────────────────────┐
              │ Random Forest        │
              │ Baseline Classifier  │
              └──────────┬───────────┘
                         │
                         ▼
              Genetic Algorithm
              Feature Selection
                         │
                         ▼
              Optimized Feature Set
                    │           │
                    ▼           ▼
          Random Forest       Random Forest
             Classifier        Regressor
                    │           │
                    ▼           ▼
          Placement Status    Salary Estimate
                    │
                    ▼
          Feedback-Based Weight
               Adjustment
```

## Key Components

### 1. Placement Prediction

A **Random Forest Classifier** is used to predict the candidate's placement status.

The model generates a probability for the positive placement class:

```text
Placement Probability → Prediction
```

A probability of `0.5` or higher is classified as **PLACED**; otherwise, the candidate is classified as **NOT PLACED**.

### 2. Genetic Algorithm Feature Selection

A custom Genetic Algorithm is used to identify a useful subset of input features.

Each individual represents a possible feature combination using a binary chromosome:

```text
[1, 0, 1, 1, 0, 1]
```

where:

* `1` → feature selected
* `0` → feature excluded

The algorithm performs:

1. Population initialization
2. Fitness evaluation
3. Selection of top individuals
4. Crossover
5. Mutation
6. Generation of a new population

The fitness of each feature subset is calculated using **3-fold cross-validation** with a Random Forest classifier.

#### Genetic Algorithm Configuration

| Parameter             |               Value |
| --------------------- | ------------------: |
| Population Size       |                  10 |
| Number of Generations |                   5 |
| Cross-Validation      |              3-Fold |
| Selected Individuals  |               Top 5 |
| Crossover             |        Single-point |
| Mutation              | Random bit mutation |

### 3. Salary Prediction

When the dataset contains the `Salary_Offered_USD` attribute, a **Random Forest Regressor** is trained to estimate the expected salary.

The regression model uses the feature subset selected during the feature-selection stage.

### 4. Feedback-Based Adaptation

The project includes a lightweight adaptive mechanism implemented through the `SimpleRL` class.

Each selected feature starts with a weight of:

```text
1.0
```

The learning rate is:

```text
0.05
```

After each prediction, the user can provide feedback:

```text
correct
```

or

```text
wrong
```

The feature weights are then adjusted based on the feedback before subsequent predictions.

This provides a simple mechanism for incorporating user feedback into the prediction process. It is **not a full reinforcement learning implementation**.

## Data Preprocessing

The preprocessing pipeline performs the following operations:

* Loads the dataset using Pandas.
* Removes the `Student_ID` identifier.
* Encodes categorical attributes using `LabelEncoder`.
* Separates the placement target from the input features.
* Splits the data into training and testing sets.
* Evaluates feature subsets through cross-validation during Genetic Algorithm optimization.

The encoded attributes include:

* `Gender`
* `Branch`
* `Programming_Skills`
* `Aptitude_Score`
* `Communication_Skills`
* `Placement_Status`

The original dataset is **not included in this repository**.

## Machine Learning Workflow

### Baseline Model

A Random Forest Classifier is first trained using the available input features to establish a baseline.

### Feature Optimization

The Genetic Algorithm evaluates different feature combinations using cross-validation and selects the best-performing feature subset from the final generation.

### Optimized Model

A second Random Forest Classifier is trained using the selected features.

### Salary Model

A Random Forest Regressor is trained separately when salary data is available.

## Prediction Pipeline

The prediction function follows this process:

```text
Candidate Input
      ↓
Selected Feature Extraction
      ↓
Feature-Weight Adjustment
      ↓
Placement Probability
      ↓
Placement Classification
      ↓
Salary Estimation
      ↓
User Feedback
      ↓
Feature-Weight Update
```

Example:

```python
predict_student([3.2, 1, 1, 6, 7, 5, 1])
```

The system returns the placement probability and prediction and, when applicable, an estimated salary.

## Technologies

| Technology   | Purpose                                    |
| ------------ | ------------------------------------------ |
| Python       | Core implementation                        |
| Pandas       | Data loading and manipulation              |
| NumPy        | Numerical operations and Genetic Algorithm |
| Scikit-learn | Machine learning and evaluation            |
| Google Colab | Development and experimentation            |

## Project Structure

```text
Career-Sense-AI/
│
├── 366Project.ipynb
├── README.md
└── requirements.txt
```

## Installation

Clone the repository and install the required dependencies:

```bash
git clone <your-repository-url>
cd Career-Sense-AI
pip install -r requirements.txt
```

## Running the Project

### Google Colab

1. Open `366Project.ipynb` in Google Colab.
2. Run the notebook from the beginning.
3. Upload the dataset when prompted.
4. Allow the preprocessing and baseline model to run.
5. Run the Genetic Algorithm feature-selection stage.
6. Train the optimized placement classifier.
7. Train the salary regression model if salary data is available.
8. Run the prediction examples.
9. Provide feedback when prompted.

### Local Jupyter Environment

Install the dependencies:

```bash
pip install -r requirements.txt
```

Open:

```text
366Project.ipynb
```

and execute the notebook cells sequentially.


## Future Improvements

* Develop a dedicated job recommendation engine based on candidate skills and job requirements.
* Add comprehensive classification and regression evaluation metrics.
* Compare multiple machine learning algorithms.
* Improve the Genetic Algorithm with more advanced evolutionary strategies.
* Expand the dataset with real-world employment and job-market information.
* Develop an interactive web application for candidate predictions.
* Integrate real-time job-market data.
* Replace the basic feedback mechanism with a more rigorous adaptive learning approach.

## License

This project is intended for educational and portfolio purposes.
