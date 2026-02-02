Task 11: A/B Testing — Hypothesis Testing in Python
📌 Project Overview

This project demonstrates how to perform A/B testing using Python to make data-driven product decisions.
It follows the full statistical workflow:
hypothesis → test → interpretation → business recommendation.

📂 Dataset

One of the following datasets was used:

Marketing A/B Testing Dataset

E-commerce Conversion Dataset

Each dataset contains a Control group (A) and a Test group (B).

🛠 Tools & Libraries

Primary: Google Colab

Alternative: Excel (basic t-test)

Libraries:

pandas

numpy

scipy

matplotlib

📁 Repository Structure
Task_11_AB_Testing/
│
├── task11_abtest.ipynb
├── ab_test_summary.csv
├── final_recommendation.txt
└── README.md

🔹 1. Load & Inspect Data
import pandas as pd
import numpy as np
from scipy import stats
import matplotlib.pyplot as plt

df = pd.read_csv("ab_test_data.csv")
df.head()


Identify groups:

df['group'].value_counts()

🔹 2. Define Hypothesis

H₀ (Null): No difference between Control and Test

H₁ (Alternative): Test group performs better

α = 0.05

🔹 3. Calculate Group Metrics
control = df[df['group'] == 'control']['conversion']
test = df[df['group'] == 'test']['conversion']

control.mean(), test.mean()

🔹 4. Run Hypothesis Test (t-test)
t_stat, p_value = stats.ttest_ind(test, control, equal_var=False)
p_value

🔹 5. Interpret Significance
alpha = 0.05
if p_value < alpha:
    print("Reject H0 – Significant difference")
else:
    print("Fail to reject H0 – No significant difference")

🔹 6. Confidence Interval
diff = test.mean() - control.mean()
se = np.sqrt(test.var()/len(test) + control.var()/len(control))

ci_low = diff - 1.96 * se
ci_high = diff + 1.96 * se

ci_low, ci_high

🔹 7. Visualization
plt.boxplot([control, test], labels=['Control', 'Test'])
plt.title("A/B Test Conversion Distribution")
plt.show()

🔹 8. Export Summary
summary = pd.DataFrame({
    'Group': ['Control', 'Test'],
    'Mean Conversion': [control.mean(), test.mean()]
})

summary.to_csv("ab_test_summary.csv", index=False)

📈 Business Interpretation (Example)

Test group shows higher conversion than Control

p-value < 0.05 → statistically significant

Confidence interval does not include 0

Recommendation:
Deploy the Test version to all users.
