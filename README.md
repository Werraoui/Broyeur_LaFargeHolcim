# Industrial Mill Overload Prediction — LafargeHolcim

## Overview

This project focuses on industrial process optimization through data analysis and machine learning. It aims to predict potential overload conditions in a cement grinding mill using operational data and an XGBoost classification model.

By analyzing key process indicators, the project explores how machine learning can support industrial monitoring, improve operational awareness, and help anticipate potentially critical operating conditions.

## Objectives

* Analyze and preprocess industrial mill operational data.
* Identify relevant variables associated with mill overload conditions.
* Engineer features to capture changes in process measurements over time.
* Develop a machine learning model to classify potential overload conditions.
* Evaluate model performance using classification metrics.
* Analyze feature importance to understand the variables influencing predictions.

## Technologies Used

* **Python** — Data processing and model development
* **Pandas** — Data manipulation and preprocessing
* **NumPy** — Numerical operations
* **Matplotlib** — Data visualization
* **Scikit-learn** — Dataset splitting and model evaluation
* **XGBoost** — Classification model
* **Jupyter Notebook** — Exploratory analysis and experimentation
* **Excel / CSV** — Industrial data storage

## Project Structure

```text
Broyeur_LaFargeHolcim/
├── Prediction_surcharge.ipynb
├── Untitled.ipynb
├── data_broyeur.xlsx
├── mill_overload_dataset.csv
├── LICENSE
└── README.md
```

* `Prediction_surcharge.ipynb`: Main notebook for data preprocessing, feature engineering, overload labeling, model training, and evaluation.
* `Untitled.ipynb`: Additional notebook containing experimentation and model testing.
* `data_broyeur.xlsx`: Source industrial dataset.
* `mill_overload_dataset.csv`: Processed dataset prepared for model training.
* `LICENSE`: Project license.

## Methodology

### 1. Data Collection and Preprocessing

The project uses industrial measurements stored in an Excel file. The preprocessing workflow includes:

* Reading Excel data with multi-level column headers.
* Cleaning and standardizing column names.
* Removing empty rows.
* Converting relevant variables to numeric values.
* Handling missing values in critical measurements.
* Selecting relevant operational indicators.

### 2. Feature Engineering

Additional features are created to capture variations and short-term trends in mill operation:

* `pressure_change`: Change in hydraulic pressure.
* `gasflow_change`: Change in mill gas flow.
* `feed_change`: Change in mill feed.
* `pressure_mean5`: Five-observation rolling average of hydraulic pressure.
* `gasflow_mean5`: Five-observation rolling average of mill gas flow.

These features aim to provide the model with information about process dynamics in addition to individual measurements.

### 3. Overload Classification

A binary target variable named `Overload` is created using predefined operational thresholds.

The current implementation labels a record as an overload when all the following conditions are satisfied:

* MM utilization KPI > 90
* MM optimization KPI > 30
* Mill feed > 80
* Fineness > 80

The target is defined as:

* `1`: Potential overload condition detected by the threshold-based labeling rule.
* `0`: Condition does not satisfy the overload rule.

**Important:** These labels are generated from predefined rules rather than independently verified overload events. Consequently, the model learns to reproduce these rules, and its predictions should not be interpreted as confirmed real-world overload events without further validation.

### 4. Model Training

The processed dataset is divided into training and testing subsets using an 80/20 split.

The project uses **XGBoost Classifier**, configured with:

* `n_estimators = 150`
* `max_depth = 4`
* `learning_rate = 0.05`
* `subsample = 0.8`
* `colsample_bytree = 0.8`

The model learns relationships between the selected operational indicators, engineered features, and the target variable.

### 5. Model Evaluation

Model performance is evaluated using:

* Accuracy
* Precision
* Recall
* F1-score
* Classification report
* Feature importance analysis

The notebook also generates a feature importance plot to help identify which variables contribute most to the model's predictions.

Actual performance values should be obtained by executing the notebook; no specific accuracy is claimed here.

## Installation and Setup

### Prerequisites

* Python 3.10 or a compatible version
* pip
* Jupyter Notebook

### 1. Clone the Repository

```bash
git clone https://github.com/Werraoui/Broyeur_LaFargeHolcim.git
cd Broyeur_LaFargeHolcim
```

### 2. Create a Virtual Environment

**Windows:**

```bash
python -m venv venv
venv\Scripts\activate
```

**Linux / macOS:**

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install pandas numpy matplotlib scikit-learn xgboost openpyxl jupyter
```

### 4. Launch Jupyter Notebook

```bash
jupyter notebook
```

Open `Prediction_surcharge.ipynb` and execute the cells in order.

Make sure `data_broyeur.xlsx` is located in the project directory before running the data preprocessing steps.

## Potential Improvements

* Validate overload labels against actual historical incidents and expert-defined operating limits.
* Use a stratified train/test split when appropriate.
* Evaluate precision, recall, F1-score, and confusion matrices, particularly if overload events are rare.
* Apply time-aware validation to account for the sequential nature of industrial data.
* Tune hyperparameters and compare XGBoost with other classification algorithms.
* Integrate real-time data and monitoring dashboards.
* Add explainability tools such as SHAP to investigate individual predictions.

## Applications

This project illustrates the use of data science and machine learning in industrial process monitoring, predictive analytics, and process optimization.

It provides a foundation for further investigation into early warning systems for cement grinding operations.

## Author

Wiame Erraoui

Data Engineering & Artificial Intelligence Student

## License

See the `LICENSE` file for the applicable terms of use.
