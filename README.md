Task 10: Python EDA — Summary Statistics & Outlier Detection
📌 Project Overview

This project demonstrates Exploratory Data Analysis (EDA) using Python to:

Understand dataset structure

Summarize data

Detect and handle outliers

Analyze correlations
It reflects a real analyst workflow before modeling or reporting.

📂 Dataset

One of the following datasets was used:

House Prices

Students Performance

Credit Card Fraud (sample)

🛠 Tools & Libraries

Primary: Google Colab

Alternatives: Jupyter / Kaggle Notebook

Libraries:

pandas

numpy

matplotlib

📁 Repository Structure
Task_10_Python_EDA/
│
├── task10_eda.ipynb
├── cleaned_dataset.csv
├── eda_findings.txt
└── README.md

🔹 1. Load & Inspect Data
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

df = pd.read_csv("house_prices.csv")

df.shape
df.info()
df.head()

🔹 2. Descriptive Statistics
df.describe()

🔹 3. Missing Values Percentage
missing_pct = (df.isnull().sum() / len(df)) * 100
missing_pct.sort_values(ascending=False)

🔹 4. Distribution Plots
plt.hist(df['SalePrice'], bins=30)
plt.title("Sale Price Distribution")
plt.show()

plt.boxplot(df['SalePrice'])
plt.title("Sale Price Boxplot")
plt.show()

🔹 5. Outlier Detection (IQR Method)
Q1 = df['SalePrice'].quantile(0.25)
Q3 = df['SalePrice'].quantile(0.75)
IQR = Q3 - Q1

lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR

df['outlier_flag'] = np.where(
    (df['SalePrice'] < lower) | (df['SalePrice'] > upper), 1, 0
)

🔹 6. Handle Outliers (Capping)
df['SalePrice'] = np.where(df['SalePrice'] > upper, upper, df['SalePrice'])
df['SalePrice'] = np.where(df['SalePrice'] < lower, lower, df['SalePrice'])

🔹 7. Correlation Matrix
corr = df.corr()
corr['SalePrice'].sort_values(ascending=False)

🔹 8. Save Cleaned Dataset
df.to_csv("cleaned_dataset.csv", index=False)

📈 EDA Findings (Example)

SalePrice is right-skewed with extreme high-value outliers.

OverallQual has the strongest correlation with SalePrice.

Outliers were capped to preserve data while reducing skew.
