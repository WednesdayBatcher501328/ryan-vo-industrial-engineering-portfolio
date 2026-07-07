# Case Study: Manufacturing Defect & Quality Analytics

### 👤 Author
* **Ryan D. Vo** – Cal Poly Pomona Industrial Engineering
* **Project Methodology:** DMAIC (Define, Measure, Analyze, Improve, Control)
* **Dataset Source:** [Kaggle Manufacturing Defects Dataset](https://kaggle.com)

<br>

---

<br>

## 🏢 1. Define & Measure (DMAIC Framework)
In high-volume manufacturing environments like Caterpillar, minimizing defect rates and predicting repair overhead is essential to sustaining lean production lines. 

### 🎯 Project Objectives & Scope:
* **Analyzed 5,000+ defect logs using SQL/Python to map severity and frequency patterns.**
* **Isolated top 2 defects causing 80% of variation using Excel Pareto and Pivot Tables.**
* **Utilized Python (Matplotlib/Seaborn) to track repair costs and prioritize line fixes.**

---

## 🗄️ 2. Data Engineering & Relational SQL Aggregations
To aggregate the data logs across categorical groups, a relational SQL architecture is utilized to evaluate total defect frequencies and extract financial averages. 

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

## 📊 3. Pareto Principle Modeling (Excel Analysis)
By building out frequency-based Pivot Tables in Microsoft Excel, an industrial 80/20 Pareto distribution is established. This data configuration isolates the exact defect categories that represent the "vital few" root causes behind the majority of manufacturing line disruptions.

### 📈 Manufacturing Defect Pareto Distribution:
*(Placeholder: We will insert your Excel Pareto Chart screenshot image file here!)*

---

## 🐍 4. Exploratory Data Visualization (Python & Inline SQL)
To aggregate our raw logs and isolate process variation metrics without deploying external database engines, the following comprehensive analytical script queries our tracking data inside an in-memory SQL database and renders automated variance boxplots:

```python
import pandas as pd
import sqlite3
import seaborn as sns
import matplotlib.pyplot as plt

# 1. Load data from local production file
df = pd.read_csv("manufacturing_defects.csv")

# 2. Establish in-memory database and populate quality logs
conn = sqlite3.connect(":memory:")
df.to_sql("quality_logs", conn, index=False, if_exists="replace")

# 3. Execute data aggregations using standard SQL syntax
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

# 4. Generate and save our process variation boxplot
sns.set_theme(style="whitegrid")
plt.figure(figsize=(10, 5))
sns.boxplot(data=df, x="severity", y="repair_cost", hue="defect_type", palette="muted")

plt.title("Defect Repair Cost Variation Across Severity Categories")
plt.xlabel("Defect Severity Tiers")
plt.ylabel("Associated Repair Cost (\$)")
plt.legend(title="Defect Type", bbox_to_anchor=(1.05, 1), loc="upper left")
plt.tight_layout()

# Export chart asset for our master portfolio documentation
plt.savefig("repair_cost_variation.png", dpi=300)
plt.show()
```

### 📊 Process Variation Analysis Output:
![Defect Repair Cost Variation](repair_cost_variation.png)
