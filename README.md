# World Happiness Report (2015–2017) Analysis

## Overview

This project explores and analyzes the World Happiness Report data from 2015 to 2017. The goal is to identify what drives happiness globally, how happiness levels change over time, and which factors show strong correlation with happiness scores. This analysis includes data cleaning, visualization, statistical analysis, and key insights, making it suitable for inclusion in a data analytics portfolio.

## Dataset Summary

* **Source**: World Happiness Report (2015–2017)
* **Columns**: Country, Happiness Score, Economy (GDP per Capita), Family, Health (Life Expectancy), Freedom, Trust (Government Corruption), Generosity, Dystopia Residual, Year

## Tools & Libraries Used

* **Python** (Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn)
* **Jupyter Notebook** for interactive coding

## Step-by-Step Project Workflow

### Step 1: Load and Understand the Dataset

* Load the combined dataset from all 3 years
* Check shape, data types, and preview data
* Review column names and consistency

### Step 2: Data Cleaning

* Checked for and handled missing values
* Verified and ensured consistent country names
* Added a 'Year' column to each dataset before concatenation
* Converted necessary columns to numeric format

### Step 3: Exploratory Data Analysis (EDA)

* **Distribution of Happiness Scores**: Histograms and boxplots used
* **Top & Bottom 10 Countries**: Bar plots created for each year
* **Trends Over Time**: Line plots used to track happiness score changes
* **Pairplot & Correlation Heatmap**: Visualized relationships between happiness and features

### Step 4: Key Questions Answered

#### 1. Which factors are most correlated with happiness?

* A correlation matrix revealed that:

  * **Economy (GDP per Capita)**: 0.78 correlation
  * **Health (Life Expectancy)**: 0.75
  * **Family**: 0.64
  * **Freedom**: 0.56
* These were identified using `df.corr()` and visualized using a heatmap

#### 2. Which countries improved or declined the most?

* Calculated happiness score difference from 2015 to 2017 using:

  ```python
  pivot = world_df.pivot(index='Country', columns='Year', values='Happiness Score')
  pivot['Change_2015_to_2017'] = pivot[2017] - pivot[2015]
  ```
* **Top Improvers**: Latvia, Romania, Togo
* **Top Decliners**: Venezuela, Liberia, Haiti

#### 3. Is GDP strongly linked to happiness?

* Yes, a strong positive correlation (0.78) was found between GDP per capita and happiness score.
* This was verified through correlation analysis and scatter plots.

#### 4. Do people in freer countries report higher happiness?

* Freedom had a moderate correlation of 0.56 with happiness score.
* Analysis was done using the correlation matrix.

### Step 5: Linear Regression

* Built a linear regression model to predict Happiness Score from contributing features.

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score

X = world_df[['Economy (GDP per Capita)', 'Family', 'Health (Life Expectancy)', 'Freedom', 'Trust (Government Corruption)', 'Generosity']]
y = world_df['Happiness Score']

model = LinearRegression()
model.fit(X, y)
y_pred = model.predict(X)

print("R-squared:", r2_score(y, y_pred))
print("Mean Squared Error:", mean_squared_error(y, y_pred))
```

* **R-squared**: 0.75 (model explains 75% of the variance)
* **Mean Squared Error**: 0.32

### Key Insights

* **GDP per Capita** is the strongest contributor to happiness.
* **Health** and **Family** also show significant influence.
* Happiness increased in several Eastern European and African countries.
* Countries with high freedom scores tend to report higher happiness, but not as strongly as GDP.


## Future Work

* Predict happiness scores using advanced models (Random Forest, XGBoost)
* Add regional clustering to visualize happiness by continent
* Time series forecasting for future happiness trends

---

