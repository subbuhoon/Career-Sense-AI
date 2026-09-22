# Career Sense AI — Predictive Placement & Salary Prediction System

An AI-based student placement analysis system that predicts placement outcomes and estimates expected salary using machine learning, Genetic Algorithm-based feature selection, and a feedback-based feature adjustment mechanism.

## Overview

**Career Sense AI** was developed as a course project for **CSE366: Artificial Intelligence** at East West University.

The system analyzes student attributes such as academic performance, programming skills, aptitude, communication skills, and other candidate information to:

* Predict whether a student is likely to be placed.
* Estimate placement probability.
* Predict expected salary for eligible candidates.
* Select relevant features using a custom Genetic Algorithm.
* Adapt feature weights through a simple feedback-based mechanism.

The project combines supervised machine learning, optimization, and adaptive learning techniques in a single workflow.

## Key Features

### 1. Placement Prediction

A **Random Forest Classifier** is used to predict student placement status.

The model produces a placement probability and classifies candidates as:

* **PLACED**
* **NOT PLACED**

### 2. Genetic Algorithm for Feature Selection

A custom Genetic Algorithm is implemented to identify useful features for placement prediction.

The algorithm includes:

* Random population generation
* Fitness evaluation
* Selection of top individuals
* Crossover
* Mutation
* Multiple generations

Each feature subset is evaluated using **3-fold cross-validation** with a Random Forest classifier.

### 3. Salary Prediction

A **Random Forest Regressor** is trained to estimate the expected salary when the dataset contains the `Salary_Offered_USD` column.

### 4. Feedback-Based Feature Adjustment

The project includes a lightweight feedback mechanism inspired by reinforcement learning.

The mechanism:

* Initializes feature weights to `1.0`.
* Adjusts feature weights based on user feedback.
* Increases weights when a prediction is marked as correct.
* Decreases weights when a prediction is marked as wrong.

This is a simple adaptive mechanism rather than a full reinforcement learning implementation.

## Workflow

```text
Student Dataset
      ↓
Data Preprocessing
      ↓
Categorical Encoding
      ↓
Train/Test Split
      ↓
Base Random Forest Classifier
      ↓
Genetic Algorithm
      ↓
Feature Selection
      ↓
Optimized Random Forest Classifier
      ↓
Placement Probability
      ↓
Salary Prediction
      ↓
Feedback-Based Feature Adjustment
```

## Dataset and Preprocessing

The dataset is uploaded through Google Colab and loaded using Pandas.

The following preprocessing steps are performed:

1. The `Student_ID` column is removed.
2. Categorical attributes are converted into numerical values using `LabelEncoder`.
3. The target variable is `Placement_Status`.
4. The data is divided into training and testing sets.
5. Selected features are evaluated through cross-validation during Genetic Algorithm optimization.

Encoded columns include:

* `Gender`
* `Branch`
* `Programming_Skills`
* `Aptitude_Score`
* `Communication_Skills`
* `Placement_Status`

The dataset itself is **not included in this repository**.

## Machine Learning Models

### Random Forest Classifier

The Random Forest classifier is used for placement prediction.

It is first trained as a baseline model and then retrained using the features selected by the Genetic Algorithm.

### Random Forest Regressor

A Random Forest Regressor is used to estimate salary when `Salary_Offered_USD` is available in the dataset.

## Genetic Algorithm

The feature selection algorithm represents each candidate feature subset as a binary chromosome.

For example:

```text
[1, 0, 1, 1, 0, 1]
```

where:

* `1` = feature selected
* `0` = feature excluded

The implementation uses:

* Population size: **10**
* Generations: **5**
* Fitness evaluation: **3-fold cross-validation**
* Selection of the top 5 individuals
* Random crossover
* Random mutation

The feature subset with the highest fitness in the final generation is selected for the final placement model.

## Feedback Mechanism

The project contains a custom `SimpleRL` class that maintains a weight for each selected feature.

Initially:

```text
Feature weight = 1.0
```

The learning rate is:

```text
0.05
```

After a prediction, the user provides feedback:

```text
correct
```

or

```text
wrong
```

The feature weights are then adjusted accordingly before the next prediction.

## Example Prediction

The notebook includes example student inputs such as:

```python
predict_student([3.2, 1, 1, 6, 7, 5, 1])
```

The system then displays:

* Placement probability
* Placement prediction
* Expected salary when the student is predicted as placed
* Feedback prompt for updating the feature weights

## Technologies Used

* Python
* Pandas
* NumPy
* Scikit-learn
* Google Colab

## Project Structure

```text
Career-Sense-AI/
│
├── 366Project.ipynb
├── README.md
└── requirements.txt
```

## Installation

Install the required Python libraries:

```bash
pip install -r requirements.txt
```

## How to Run

### Using Google Colab

1. Open `366Project.ipynb` in Google Colab.
2. Run the notebook cells sequentially.
3. When prompted, upload the dataset.
4. The notebook will preprocess the data.
5. Train the baseline Random Forest model.
6. Run the Genetic Algorithm for feature selection.
7. Train the optimized classifier.
8. Train the salary prediction model if salary data is available.
9. Run the sample predictions.
10. Provide feedback when prompted.

### Using Jupyter Notebook

Install the required packages:

```bash
pip install -r requirements.txt
```

Then open:

```text
366Project.ipynb
```

and execute the cells sequentially.

## Limitations

* The system depends on the quality and size of the dataset.
* The feedback mechanism is a simple feature-weight adjustment rather than a complete reinforcement learning algorithm.
* Salary prediction is only performed when the dataset contains `Salary_Offered_USD`.
* The current implementation does not generate specific job-role recommendations.
* The dataset is not included in the repository.

## Future Improvements

Possible future improvements include:

* Using larger real-world student and employment datasets.
* Adding additional machine learning and deep learning models.
* Improving the Genetic Algorithm with more advanced selection and mutation strategies.
* Adding proper salary prediction evaluation metrics.
* Developing a web-based interface.
* Integrating real-time job-market information.
* Adding a genuine job recommendation module based on candidate skills and job requirements.
* Developing a more sophisticated feedback or reinforcement learning system.

## Course Information

**Course:** CSE366 — Artificial Intelligence
**Section:** 3
**Semester:** Spring 2026
**Institution:** East West University

### Project Team

| Student ID    | Student Name        | Contribution |
| ------------- | ------------------- | -----------: |
| 2023-2-60-177 | Anjuman Rafiya      |          25% |
| 2023-2-60-202 | Eshrat Jahan Esha   |          25% |
| 2023-2-60-206 | Rahma Kamal         |          25% |
| 2022-2-60-147 | Jannatul Alam Shifa |          25% |

## References

1. C. Romero and S. Ventura, “Educational data mining: A survey from 1995 to 2005,” *Expert Systems with Applications*, vol. 33, no. 1, pp. 135–146, 2007.
2. L. Breiman, “Random forests,” *Machine Learning*, vol. 45, no. 1, pp. 5–32, 2001.
3. F. Pedregosa et al., “Scikit-learn: Machine learning in Python,” *Journal of Machine Learning Research*, vol. 12, pp. 2825–2830, 2011.
4. M. Kumar, N. Walia, S. Bansal, G. Kumar, and K. Cengiz, “Predicting college students’ placements based on academic performance using machine learning approaches,” *International Journal of Modern Education and Computer Science*, vol. 15, no. 6, pp. 1–13, 2023.

