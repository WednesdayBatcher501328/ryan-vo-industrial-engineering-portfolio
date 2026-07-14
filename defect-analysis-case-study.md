# Predictive Defect & Quality Analytics

### 👤 Author
* **Ryan D. Vo** – Cal Poly Pomona Industrial Engineering
* **Project Timeline:** June–July 2026
* **Project Methodology:** DMAIC (Define, Measure, Analyze, Improve, Control)
* **Dataset Source:** [Kaggle Manufacturing Defects Dataset](https://www.kaggle.com/datasets/fahmidachowdhury/manufacturing-defects/data)

<br>

---

<br>

## 1. Define & Measure (DMAIC Framework)
In high-volume manufacturing environments, minimizing defect rates and repair costs is essential for improving product quality and reducing waste. This project analyzes manufacturing defect data using SQL, Python, and Excel to identify defect trends and support process improvement decisions. 

### Project Objectives & Scope:
* **Analyzed 5,000+ defect logs using SQL/Python to map severity and frequency patterns.**
* **Isolated top 2 defects causing 80% of variation using Excel Pareto and Pivot Tables.**
* **Used Python to analyze manufacturing defect data and create visualizations.**

## 2. Data Engineering & Relational SQL Aggregations
The dataset was queried using SQL to summarize defect frequencies and calculate average repair costs for each defect type and severity level. 

```sql
-- Query to map defect distribution and calculate mean repair costs
SELECT 
    defect_type, 
    severity, 
    COUNT(*) AS total_occurrences,
    ROUND(AVG(repair_cost), 2) AS average_repair_cost
FROM quality_logs
GROUP BY defect_type, severity
ORDER BY total_occurrences DESC;
```

---

## 3. Pareto Principle Modeling (Excel Analysis)
Pivot Tables and Pareto charts were created in Microsoft Excel to apply the 80/20 principle. This analysis identified the defect categories that contributed most to overall process variation.

### Manufacturing Defect Pareto Distribution:
![Manufacturing Defect Pareto Chart](batch13_pareto_chart.png)

---

## 4. Exploratory Data Visualization (Python & Inline SQL)
The dataset was loaded into an in-memory SQLite database so SQL queries could be executed directly from Python. The resulting summaries were then visualized using Python to examine repair cost variation across defect categories.

```python
import pandas as pd
import sqlite3
import seaborn as sns
import matplotlib.pyplot as plt

# Load the manufacturing defects dataset
df = pd.read_csv("defects_data.csv")

# Store the dataset in an in-memory SQLite database
conn = sqlite3.connect(":memory:")
df.to_sql("quality_logs", conn, index=False, if_exists="replace")

# Aggregate defect frequency and repair cost using SQL
sql_query = """
SELECT
    defect_type,
    severity,
    COUNT(*) AS total_occurrences,
    ROUND(AVG(repair_cost), 2) AS average_repair_cost
FROM quality_logs
GROUP BY defect_type, severity
ORDER BY total_occurrences DESC;
"""

summary_df = pd.read_sql_query(sql_query, conn)

print("SQL Summary:")
print(summary_df.head())

# Create a boxplot showing repair cost variation
sns.set_theme(style="whitegrid")

plt.figure(figsize=(10, 5))

sns.boxplot(
    data=df,
    x="severity",
    y="repair_cost",
    hue="defect_type",
    palette="muted"
)

plt.title("Defect Repair Cost Variation Across Severity Categories")
plt.xlabel("Defect Severity Tier")
plt.ylabel("Associated Repair Cost ($)")
plt.legend(title="Defect Type", bbox_to_anchor=(1.05, 1), loc="upper left")

plt.tight_layout()

# Save the figure for the portfolio
plt.savefig("repair_cost_variation.png", dpi=300)
plt.show()
```

Note: I primarily used Pandas, SQL, and Matplotlib during the project. The boxplot example was built using Seaborn because it provides a convenient statistical plotting function.

### Process Variation Analysis Output

![Defect Repair Cost Variation](repair_cost_variation.png)
