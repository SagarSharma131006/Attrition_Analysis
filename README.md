# 📊 Employee Attrition Analysis

An exploratory data analysis (EDA) project focused on understanding **employee attrition and workforce-related patterns** using Python.

This project analyzes an employee dataset using popular Python data analysis and visualization libraries such as **NumPy, Pandas, Matplotlib, and Seaborn**.

The complete analysis is available in the Jupyter Notebook, along with the original dataset in CSV format.

---

## 📌 Project Overview

Employee attrition is an important problem for organizations because frequent employee turnover can affect productivity, team performance, recruitment costs, and overall business growth.

In this project, I performed **Exploratory Data Analysis (EDA)** on an employee attrition dataset to understand the data, identify patterns, analyze numerical and categorical variables, and detect potential outliers.

The project focuses mainly on:

* Understanding the dataset
* Data inspection and exploration
* Data cleaning and preprocessing
* Statistical analysis
* Numerical and categorical data analysis
* Data visualization
* Outlier identification
* Finding useful patterns and relationships in the data

---

## 🎯 Objectives

The main objectives of this project are:

1. Understand the structure of the employee dataset.
2. Explore different features and their distributions.
3. Perform data cleaning and preprocessing.
4. Analyze numerical and categorical variables.
5. Visualize important patterns using different plots.
6. Identify possible outliers in numerical columns.
7. Understand relationships between different variables.
8. Extract meaningful insights from the dataset.
9. Build practical experience with Python-based Exploratory Data Analysis.

---

## 🛠️ Technologies & Libraries Used

| Technology / Library | Purpose                            |
| -------------------- | ---------------------------------- |
| 🐍 Python            | Programming Language               |
| 🔢 NumPy             | Numerical computations             |
| 🐼 Pandas            | Data manipulation and analysis     |
| 📊 Matplotlib        | Data visualization                 |
| 🎨 Seaborn           | Statistical data visualization     |
| 📓 Jupyter Notebook  | Development & analysis environment |
| 📁 CSV               | Dataset format                     |

---

## 📂 Repository Structure

```text
Attrition_Analysis/
│
├── 📓 Attrition_Analysis.ipynb
├── 📊 Attrition_Analytics.csv
└── 📖 README.md
```

### Files Description

### `Attrition_Analysis.ipynb`

The main Jupyter Notebook containing the complete analysis.

It includes:

* Data loading
* Data inspection
* Data preprocessing
* Exploratory analysis
* Statistical analysis
* Data visualization
* Outlier identification
* Observations and insights

### `Attrition_Analytics.csv`

The dataset used for performing the analysis.

### `README.md`

Project documentation containing information about the project, technologies, methodology, and key observations.

---

# 🔍 Analysis Performed

## 1. Data Loading

The dataset was imported into Python using **Pandas**.

```python
import pandas as pd

df = pd.read_csv("Attrition_Analytics.csv")
```

---

## 2. Data Inspection

The dataset was explored using Pandas functions to understand:

* Number of rows and columns
* Column names
* Data types
* Missing values
* Statistical information
* Unique values

Common functions used include:

```python
df.head()
df.tail()
df.shape
df.info()
df.describe()
df.isnull().sum()
df.nunique()
```

---

## 3. Data Cleaning

Before performing analysis, the dataset was checked for common data quality issues such as:

* Missing values
* Duplicate records
* Incorrect data types
* Inconsistent values
* Unusual observations

The required preprocessing steps were performed before visualization and analysis.

---

# 📊 Exploratory Data Analysis

Exploratory Data Analysis was performed to understand the distribution and characteristics of the employee data.

Different numerical and categorical variables were analyzed using statistical methods and visualizations.

### Numerical Analysis

Numerical columns were analyzed using:

* Mean
* Median
* Minimum
* Maximum
* Standard deviation
* Quartiles
* Distribution plots
* Box plots

Example:

```python
df.describe()
```

---

## 📈 Data Visualization

Several visualization techniques were used to better understand the dataset.

### Libraries Used

```python
import matplotlib.pyplot as plt
import seaborn as sns
```

Visualizations included:

* Histograms
* Count plots
* Box plots
* Distribution plots
* Bar charts
* Relationship plots
* Correlation analysis

Visualization helped make patterns in the dataset easier to understand.

---

# 🚨 Outlier Identification

Outlier detection was also performed as part of the analysis.

For example, a **box plot** was used to analyze the `Age` column.

```python
sns.boxplot(y="Age", data=df)
plt.show()
```

The box plot helped identify whether unusually high or low age values were present.

### Observation

The analysis showed that there were **no significant outliers present in the Age column**.

---

# 🔗 Correlation Analysis

Correlation analysis can be used to understand relationships between numerical variables.

A correlation matrix can be generated using:

```python
df.corr(numeric_only=True)
```

A heatmap can then be used to visualize these relationships:

```python
sns.heatmap(df.corr(numeric_only=True), annot=True)
plt.show()
```

This helps identify variables that have positive, negative, or weak relationships with each other.

---

# 💡 Key Learning Outcomes

Through this project, I gained practical experience in:

* Working with real-world datasets
* Loading CSV files using Pandas
* Understanding DataFrames
* Data inspection and cleaning
* Handling numerical and categorical data
* Performing exploratory data analysis
* Creating statistical visualizations
* Using Matplotlib and Seaborn
* Detecting outliers using box plots
* Understanding correlations between variables
* Extracting insights from data
* Working with Jupyter Notebooks

---

# 🧠 Concepts Practiced

The major Python and Data Analysis concepts practiced in this project include:

```text
Python
│
├── NumPy
│   ├── Arrays
│   ├── Numerical Operations
│   └── Statistical Operations
│
├── Pandas
│   ├── DataFrames
│   ├── Data Loading
│   ├── Data Cleaning
│   ├── Data Filtering
│   └── Data Analysis
│
├── Matplotlib
│   ├── Line Plots
│   ├── Bar Charts
│   ├── Histograms
│   └── Custom Visualization
│
└── Seaborn
    ├── Count Plots
    ├── Box Plots
    ├── Distribution Plots
    ├── Heatmaps
    └── Statistical Visualization
```

---

# 🚀 How to Run This Project

## 1. Clone the Repository

```bash
git clone https://github.com/SagarSharma131006/Attrition_Analysis.git
```

## 2. Navigate to the Project Directory

```bash
cd Attrition_Analysis
```

## 3. Install Required Libraries

```bash
pip install numpy pandas matplotlib seaborn jupyter
```

Or:

```bash
pip install -r requirements.txt
```

> If a `requirements.txt` file is not available in the repository, install the libraries using the first command.

---

## 4. Start Jupyter Notebook

```bash
jupyter notebook
```

Then open:

```text
Attrition_Analysis.ipynb
```

Run the notebook cells sequentially to reproduce the analysis.

---

# 📸 Project Preview

The project includes different visualizations for understanding the employee dataset.

One of the analyses performed in the notebook is **outlier identification using a box plot**.

Example:

```text
                Age Distribution

        ┌──────────────────────────┐
        │        ┌──────────┐       │
        │        │          │       │
        │────────│   Age    │────────
        │        │          │       │
        │        └──────────┘       │
        └──────────────────────────┘

        No significant outliers
        detected in Age column.
```

---

# 📌 Project Highlights

✨ Complete Exploratory Data Analysis

📊 Multiple data visualizations

🐼 Pandas-based data manipulation

🔢 NumPy-based numerical analysis

📈 Matplotlib visualizations

🎨 Seaborn statistical visualizations

🚨 Outlier detection

🔍 Data exploration and pattern identification

📁 Dataset included with the project

📓 Complete analysis available in Jupyter Notebook

---

# 📚 What I Learned

This project helped me understand how Python can be used to analyze a dataset from beginning to end.

Instead of only learning individual libraries theoretically, I practiced using **NumPy, Pandas, Matplotlib, and Seaborn together in a practical data analysis workflow**.

The project also improved my understanding of how to inspect data, visualize distributions, identify outliers, and extract meaningful information from a dataset.

---

# 🔮 Future Improvements

The project can be extended further by adding:

* [ ] More detailed statistical analysis
* [ ] Advanced feature relationships
* [ ] Interactive visualizations
* [ ] Dashboard using Power BI or Tableau
* [ ] Employee attrition prediction using Machine Learning
* [ ] Feature engineering
* [ ] Classification models
* [ ] Model evaluation
* [ ] Deployment of an attrition prediction model

---

# 🤝 Contribution

This repository is primarily created for learning and documenting my progress in **Python, Data Analysis, and Machine Learning**.

Suggestions, improvements, and feedback are always welcome.

If you find something useful or have an idea for improving the analysis, feel free to contribute.

---

# ⭐ Support

If you found this project useful, consider giving the repository a ⭐ on GitHub.

---

## 👨‍💻 Author

**Sagar Sharma**

B.Tech CSE — Artificial Intelligence & Machine Learning

Interested in:

* 🤖 Artificial Intelligence
* 🧠 Machine Learning
* 📊 Data Science
* 🐍 Python
* 💻 Problem Solving
* 📈 Data Analysis

---

## 📌 Repository

**Attrition Analysis**

> A practical Python Exploratory Data Analysis project using NumPy, Pandas, Matplotlib, and Seaborn.

---

### 📜 License

This project is created for **educational and learning purposes**.
