# 📊 Attrition Analysis using Python

A complete **Exploratory Data Analysis (EDA)** project performed on an **Employee Attrition dataset** using Python.

The purpose of this project is to analyze different factors that may influence employees to leave an organization and extract meaningful insights from the data through **data cleaning, statistical analysis, outlier treatment, and visualization**.

This repository contains both the **Jupyter Notebook** containing the complete analysis and the **CSV dataset** used in the project.

---

## 📌 About the Dataset

The **Attrition Analytics dataset** represents an organization and contains information about employees and various factors related to their work and personal characteristics.

The original dataset contains:

* **1,480 rows**
* **38 columns**

The dataset contains information related to:

* Employee demographics
* Age and age groups
* Attrition
* Business travel
* Department
* Gender
* Education
* Education field
* Job role
* Job level
* Job satisfaction
* Environment satisfaction
* Salary
* Monthly income
* Overtime
* Years at company
* Total working years
* Work-life balance
* Relationship satisfaction
* Stock options
* Training
* And other employee-related attributes

The main objective of the analysis is to understand **why employees leave the organization and which factors are associated with higher attrition**.

---

# 🎯 Objectives

The major objectives of this project are:

* Understand the structure of the employee dataset
* Explore the dataset using Pandas
* Perform statistical analysis
* Identify missing values
* Handle missing data
* Identify numerical and categorical columns
* Analyze distributions of numerical features
* Identify outliers
* Remove/treat outliers
* Identify and remove duplicate records
* Create meaningful visualizations
* Analyze employee attrition based on different factors
* Calculate the overall attrition percentage
* Extract useful business insights from the dataset

---

# 🛠️ Technologies & Libraries Used

| Technology / Library | Purpose                                    |
| -------------------- | ------------------------------------------ |
| 🐍 Python            | Programming language                       |
| 🔢 NumPy             | Numerical operations and outlier treatment |
| 🐼 Pandas            | Data manipulation and analysis             |
| 📊 Matplotlib        | Data visualization                         |
| 🎨 Seaborn           | Statistical visualization                  |
| 📓 Jupyter Notebook  | Development and analysis environment       |

### Libraries Imported

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import warnings

warnings.filterwarnings('ignore')
```

---

# 📂 Repository Structure

```text
Attrition_Analysis/
│
├── 📓 Attrition_Analysis.ipynb
├── 📊 Attrition_Analytics.csv
└── 📖 README.md
```

### 📓 `Attrition_Analysis.ipynb`

Contains the complete Exploratory Data Analysis performed on the dataset.

### 📊 `Attrition_Analytics.csv`

The CSV dataset used for the complete analysis.

### 📖 `README.md`

Project documentation and explanation of the analysis.

---

# 🔍 Exploratory Data Analysis

## 1. Loading the Dataset

The CSV dataset was loaded using Pandas:

```python
df = pd.read_csv('/content/Attrition_Analytics.csv')
```

The dataset contains:

```text
Rows    : 1480
Columns : 38
```

---

# 📋 2. Dataset Statistics

The `describe()` function was used to understand the statistical properties of numerical features.

```python
df.describe()
```

This provides information such as:

* Count
* Mean
* Standard deviation
* Minimum
* 25th percentile
* Median
* 75th percentile
* Maximum

For example, the `Age` column has:

```text
Minimum Age : 18
Maximum Age : 60
Mean Age    : ~36.92
Median Age  : 36
```

---

# 🚨 3. Missing Value Analysis

The dataset was checked for missing values using:

```python
df.isnull().sum()
```

### Initial Result

A total of **57 missing values** were found.

All 57 missing values were present in:

```text
YearsWithCurrManager
```

The mean value of this column was approximately:

```text
4.118
```

The missing values were then replaced using the rounded mean:

```python
df['YearsWithCurrManager'].fillna(
    round(df['YearsWithCurrManager'].mean()),
    inplace=True
)
```

After imputation, the dataset contained **0 missing values**.

---

# 🔢 4. Numerical & Categorical Features

The dataset was divided into numerical and categorical columns.

### Numerical Columns

The dataset contains:

```text
26 Numerical Columns
```

These were identified using:

```python
num_numeric_cols = df.select_dtypes(
    include=['int64','float64']
)
```

### Categorical Columns

The dataset contains:

```text
12 Categorical Columns
```

These were identified using:

```python
num_categorical_cols = df.select_dtypes(
    include=['object']
)
```

---

# 📈 5. Distribution Analysis

Histograms were generated for numerical features to understand their distributions.

```python
df.hist(
    bins=10,
    layout=(6,5),
    figsize=(10,10)
)

plt.tight_layout()
plt.show()
```

This helped in understanding:

* Feature distributions
* Frequency patterns
* Spread of numerical values
* Possible unusual observations

---

# 🎯 6. Feature Selection

For focused analysis, the following columns were selected:

```python
selected_cols = [
    'EmpID',
    'Age',
    'AgeGroup',
    'Attrition',
    'Department',
    'Gender',
    'EducationField',
    'SalarySlab',
    'YearsAtCompany',
    'MonthlyIncome'
]
```

A new DataFrame was created:

```python
df1 = df[selected_cols]
```

An additional binary column was created to represent attrition:

```python
df1['Attrition Count'] = df1['Attrition'].apply(
    lambda x: 1 if x == 'Yes' else 0
)
```

Where:

```text
1 → Employee left the organization
0 → Employee stayed in the organization
```

---

# 🚨 7. Outlier Identification

Box plots were used to identify outliers in important numerical columns.

### Age

```python
sns.boxplot(y="Age", data=df1)
```

**Observation:**
No significant outliers were identified in the `Age` column.

---

### Years At Company

```python
sns.boxplot(
    y='YearsAtCompany',
    data=df1
)
```

**Observation:**
Outliers were identified in the `YearsAtCompany` column.

---

### Monthly Income

```python
sns.boxplot(
    y='MonthlyIncome',
    data=df1
)
```

**Observation:**
Outliers were identified in the `MonthlyIncome` column.

---

# 🧮 8. Outlier Treatment

The **IQR (Interquartile Range)** method was used to identify the lower and upper bounds.

```python
def remove_outlier(col_name):
    sorted(col_name)
    Q1, Q3 = col_name.quantile([0.25, 0.75])
    IQR = Q3 - Q1

    lower_bound = Q1 - 1.5 * IQR
    upper_bound = Q3 + 1.5 * IQR

    return lower_bound, upper_bound
```

The outliers in:

* `YearsAtCompany`
* `MonthlyIncome`

were treated by capping values at the calculated lower and upper bounds.

Example:

```python
df1['YearsAtCompany'] = np.where(
    df1['YearsAtCompany'] > high,
    high,
    df1['YearsAtCompany']
)
```

The same approach was applied to `MonthlyIncome`.

---

# 🧹 9. Duplicate Removal

The selected dataset initially contained:

```text
1480 rows
```

Duplicate records were removed using:

```python
df_cleaned = df1.drop_duplicates()
```

### Result

```text
Initial Rows       : 1480
Duplicate Rows     : 10
Final Rows         : 1470
```

Therefore, the final cleaned dataset contains:

```text
1470 employee records
```

---

# 📊 Visualization & Attrition Analysis

After cleaning the dataset, different visualizations were created to understand employee attrition.

---

## 👥 10. Attrition by Gender

A bar plot was used to analyze attrition based on gender.

```python
sns.barplot(
    x='Gender',
    y='Attrition Count',
    data=df_cleaned,
    estimator=sum
)

plt.title('Attrition by Gender')
plt.show()
```

### Observation

According to the analysis, **male employees had higher attrition than female employees**.

---

# 🎓 11. Attrition by Education Field

A pie chart was used to analyze attrition based on employees' education fields.

Education fields present in the dataset include:

* Life Sciences
* Medical
* Marketing
* Technical Degree
* Other
* Human Resources

The distribution of employees by education field was also examined.

```python
df_cleaned['EducationField'].value_counts()
```

### Observation

Employees from the **Life Sciences** education field accounted for the highest attrition in the analysis.

---

# 👶 12. Attrition by Age Group

A bar plot was used to analyze attrition across different age groups.

```python
sns.barplot(
    x='Attrition Count',
    y='AgeGroup',
    data=df_cleaned,
    estimator=sum
)

plt.title('Attrition by AgeGroup')
plt.show()
```

### Observation

The **26–35 age group** had the highest attrition.

Employees in the **55+ age group** had the lowest attrition.

---

# 💰 13. Attrition by Salary Slab

Attrition was analyzed based on salary slabs.

```python
sns.barplot(
    x='SalarySlab',
    y='Attrition Count',
    data=df_cleaned,
    estimator=sum
)

plt.title('Attrition by Salary Slab')
plt.show()
```

### Observation

The analysis showed that employees in the **lower salary slab had higher attrition**, while employees earning in the higher salary slab had comparatively lower attrition.

---

# 🏢 14. Attrition by Years at Company

A line plot was used to analyze attrition based on the number of years employees had spent at the company.

```python
plt.figure(figsize=(10,40))

df_cleaned.groupby(
    ['YearsAtCompany']
).sum().plot(
    kind='line',
    y='Attrition Count'
)

plt.title('Attrition by YearsAtCompany')
plt.show()
```

### Observation

The analysis showed that a large portion of attrition came from employees with **less than approximately 2.5 years of experience at the company**.

Employees with around **12 years at the company** showed comparatively lower attrition.

---

# 🏭 15. Attrition by Department

Department-wise attrition was also analyzed.

```python
sns.barplot(
    x='Department',
    y='Attrition Count',
    data=df_cleaned,
    estimator=sum
)

plt.title('Attrition by Department')
```

### Observation

The **Research & Development** department had the highest attrition.

The **Human Resources** department had the lowest attrition.

---

# 📌 16. Attrition vs Stable Employees

A count plot was used to compare employees who left the organization with those who remained.

```python
sns.countplot(
    x='Attrition Count',
    data=df_cleaned
)

plt.title('Attrition vs Stable Employees')
```

The analysis showed that approximately **237 employees left the organization**.

---

# 📈 17. Overall Attrition Percentage

The total number of employees who left was calculated using:

```python
attrition_count = df_cleaned['Attrition Count'].sum()

print(
    "Total Employees left the Organization:",
    attrition_count
)
```

### Result

```text
Employees who left : 237
```

The final dataset contained:

```text
Total Employees : 1470
```

The overall attrition percentage was calculated using:

```python
attrition_percent = (
    attrition_count / total_employees
) * 100
```

### Result

```text
Attrition Percentage ≈ 16.12%
```

Therefore, approximately **16% of employees in the cleaned dataset had left the organization**.

---

# 💡 Key Insights

Based on the analysis performed in this notebook:

### 👥 Gender

Male employees showed higher attrition than female employees.

### 🎓 Education Field

The **Life Sciences** education field had the highest attrition among the education fields analyzed.

### 👶 Age Group

Employees between **26–35 years** showed the highest attrition.

### 💰 Salary

Employees in lower salary slabs showed comparatively higher attrition.

### 🏢 Department

The **Research & Development** department had the highest attrition.

### ⏳ Years at Company

Employees with relatively short tenure, particularly those with less than approximately **2.5 years at the company**, contributed significantly to attrition.

### 📊 Overall Attrition

The cleaned dataset contained:

```text
1470 Employees
237 Employees Left
16.12% Attrition Rate
```

---

# 🔄 Data Analysis Workflow

The complete workflow followed in this project can be summarized as:

```text
                ┌─────────────────────┐
                │   Load CSV Dataset  │
                └──────────┬──────────┘
                           ↓
                ┌─────────────────────┐
                │   Explore Dataset   │
                └──────────┬──────────┘
                           ↓
                ┌─────────────────────┐
                │ Statistical Analysis│
                └──────────┬──────────┘
                           ↓
                ┌─────────────────────┐
                │ Missing Value Check │
                └──────────┬──────────┘
                           ↓
                ┌─────────────────────┐
                │ Handle Missing Data │
                └──────────┬──────────┘
                           ↓
                ┌─────────────────────┐
                │ Feature Selection   │
                └──────────┬──────────┘
                           ↓
                ┌─────────────────────┐
                │ Outlier Detection   │
                └──────────┬──────────┘
                           ↓
                ┌─────────────────────┐
                │ Outlier Treatment   │
                └──────────┬──────────┘
                           ↓
                ┌─────────────────────┐
                │ Remove Duplicates   │
                └──────────┬──────────┘
                           ↓
                ┌─────────────────────┐
                │ Visualization       │
                └──────────┬──────────┘
                           ↓
                ┌─────────────────────┐
                │ Extract Insights    │
                └──────────┬──────────┘
                           ↓
                ┌─────────────────────┐
                │ Attrition Analysis  │
                └─────────────────────┘
```

---

# 🧠 Concepts Practiced

Through this project, I practiced:

* Python programming
* NumPy
* Pandas
* DataFrames
* CSV data handling
* Data inspection
* Descriptive statistics
* Missing value detection
* Missing value imputation
* Numerical and categorical feature identification
* Feature selection
* Lambda functions
* Data transformation
* Histograms
* Bar plots
* Pie charts
* Line plots
* Count plots
* Box plots
* Outlier detection
* IQR method
* Outlier capping
* Duplicate detection and removal
* GroupBy operations
* Data aggregation
* Exploratory Data Analysis
* Business-oriented data interpretation

---

# 🚀 How to Run the Project

## 1. Clone the Repository

```bash
git clone https://github.com/SagarSharma131006/Attrition_Analysis.git
```

## 2. Navigate to the Project

```bash
cd Attrition_Analysis
```

## 3. Install Required Libraries

```bash
pip install numpy pandas matplotlib seaborn jupyter
```

## 4. Start Jupyter Notebook

```bash
jupyter notebook
```

Open:

```text
Attrition_Analysis.ipynb
```

Make sure the following files are available in the same project environment:

```text
Attrition_Analysis.ipynb
Attrition_Analytics.csv
```

Then run the notebook cells sequentially.

---

# 📌 Project Highlights

✨ Complete Employee Attrition EDA

🐍 Python-based data analysis

🐼 Pandas data manipulation

🔢 NumPy numerical operations

📊 Matplotlib visualization

🎨 Seaborn visualization

🚨 Missing value handling

📉 Outlier detection and treatment

🧹 Duplicate removal

📈 Attrition percentage calculation

🔍 Business-oriented insights

📁 Dataset included

📓 Complete Jupyter Notebook included

---

# 🔮 Future Improvements

This project currently focuses on **Exploratory Data Analysis**.

Possible future improvements include:

* [ ] Feature engineering
* [ ] Correlation analysis
* [ ] Advanced statistical analysis
* [ ] Interactive dashboard using Power BI
* [ ] Interactive dashboard using Streamlit
* [ ] Employee attrition prediction
* [ ] Machine Learning classification models
* [ ] Logistic Regression
* [ ] Decision Tree
* [ ] Random Forest
* [ ] Model evaluation
* [ ] Hyperparameter tuning
* [ ] Deployment of an attrition prediction model

---

# 📚 Learning Outcome

This project helped me understand how to perform a complete **Exploratory Data Analysis workflow** on an employee dataset.

I learned how to move from raw CSV data to a cleaned dataset and then use visualization and statistical techniques to identify patterns related to employee attrition.

The project also provided practical experience with **NumPy, Pandas, Matplotlib, and Seaborn** and strengthened my understanding of data cleaning, missing value handling, outlier treatment, duplicate removal, and data visualization.

---

# 👨‍💻 Author

**Sagar Sharma**

B.Tech CSE — Artificial Intelligence & Machine Learning

### Interests

* 🤖 Artificial Intelligence
* 🧠 Machine Learning
* 📊 Data Science
* 📈 Data Analysis
* 🐍 Python
* 💻 Problem Solving

---

# ⭐ Support

If you found this project useful or interesting, consider giving this repository a ⭐ on GitHub.

---

## 📜 License

This project is created for **educational and learning purposes**.
