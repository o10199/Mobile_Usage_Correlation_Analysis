# Mobile Usage Correlation Analysis

## Overview
This project explores the relationships between different mobile phone usage metrics to understand how various usage patterns are interconnected. The central research question is: **How do screen time, battery level, data usage, physical activity, and call duration correlate with each other?** Understanding these relationships could help users better manage their phone habits and battery life.

---

## 🛠️ Tools & Technologies
- Python
- Pandas
- Seaborn
- Matplotlib
- Google Colab

---

## 📂 Dataset
- **Source:** [Mobile Usage Dataset – Kaggle](https://www.kaggle.com/datasets/nitingoyal8/mobile-usage-dataset)
- **Size:** 20 users over a 10-day period (January 2024)
- **Variables Analyzed:**

| Variable | Description |
|---|---|
| Screen Time (mins) | Daily screen time in minutes |
| Battery Level (%) | Battery percentage at time of record |
| Data Usage (MB) | Mobile data consumed in MB |
| Steps Count | Number of steps taken |
| Call Duration (mins) | Total call duration in minutes |

---

## 🗄️ Setup

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

from google.colab import files
uploaded = files.upload()

df = pd.read_csv('mobile_life_sample.csv')

print("First few rows of our data:")
print(df.head())
```

---

## 🔍 Analysis & Solutions

### 1️⃣ Define Variables of Interest
Selects the five numerical columns used in the correlation analysis.

```python
numerical_columns = ['Screen_Time (mins)', 'Battery_Level (%)',
                    'Data_Usage (MB)', 'Steps_Count', 'Call_Duration (mins)']
```

### 2️⃣ Compute the Correlation Matrix
Calculates pairwise correlations between all five variables.

```python
correlation = df[numerical_columns].corr()

print("\nCorrelation values:")
print(correlation)
```

### 3️⃣ Visualize with a Heatmap
Generates a heatmap to visually represent the strength and direction of correlations.

```python
plt.figure(figsize=(10, 8))
sns.heatmap(correlation, annot=True)
plt.title('Correlation Heatmap')
plt.show()
```

### 4️⃣ Inspect Key Correlations
Pulls out specific correlation values to highlight notable relationships.

```python
print("\nLet's see how different things are related:")

print("\nCorrelation between Screen Time and Battery Level:")
print(correlation['Screen_Time (mins)']['Battery_Level (%)'])

print("\nCorrelation between Screen Time and Data Usage:")
print(correlation['Screen_Time (mins)']['Data_Usage (MB)'])

print("\nCorrelation between Steps Count and Call Duration:")
print(correlation['Steps_Count']['Call_Duration (mins)'])
```

---

## 📊 Key Findings

1. Most correlations between variables are surprisingly **weak (below 0.2)**, suggesting mobile usage behaviors are largely independent of one another.
2. **Strongest positive correlations:**
   - Steps Count & Call Duration: **0.13** — people may tend to walk while on a call
   - Screen Time & Battery Level: **0.13** — users may use their phones more when battery is higher
3. **Strongest negative correlation:**
   - Battery Level & Data Usage: **−0.09** — higher data use may slightly drain battery
4. Screen time showed very weak positive correlations with all other variables.
5. Data usage showed mostly negative correlations with other metrics, except for call duration.

---

## Conclusion
Mobile usage patterns are largely independent of each other, with no strong correlations between the measured variables. The weak positive correlation between screen time and battery level may suggest users are more active on their phones when battery is sufficient. The steps-call duration link could reflect a common habit of walking while talking. These findings could inform more personalized battery management strategies and usage recommendations.

---

## References
Goyal8, N. (2025, February 9). *Mobile usage dataset*. Kaggle. https://www.kaggle.com/datasets/nitingoyal8/mobile-usage-dataset
