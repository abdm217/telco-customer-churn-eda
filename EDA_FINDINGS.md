# EDA Findings — Telco Customer Churn

## 1. Project Overview

This project performs exploratory data analysis (EDA) and statistical profiling on the Telco Customer Churn dataset. The objective is to understand the dataset's structure, examine numerical distributions, identify data quality issues, investigate relationships between customer characteristics and churn, and establish a foundation for future classification tasks.

The dataset contains **7,043 customer records and 21 original columns**, including the target variable `Churn`. The target indicates whether a customer discontinued the company's services.

## 2. Data Quality Assessment

The initial inspection found no duplicate rows. The `TotalCharges` column was initially stored as text because some entries contained blank strings.

After converting `TotalCharges` to a numeric data type, **11 missing values** were identified. These entries correspond to customers whose tenure is zero months. They were preserved as missing values rather than automatically replaced with zero, because missing values should be handled according to their meaning.

The dataset also contains categories such as `No internet service` and `No phone service`. These are valid categorical values and should not automatically be treated as missing data.

No negative values were identified in `MonthlyCharges` or the non-missing values of `TotalCharges`, and tenure values were within the expected range of 0 to 72 months.

## 3. Statistical Profiling and Distribution Analysis

Numerical columns were examined using summary statistics, including mean, median, variance, standard deviation, and skewness. Histograms were used to inspect the shapes of the numerical distributions.

### 3.1 SeniorCitizen

The mean of `SeniorCitizen` is approximately 0.162, the median is 0, and the skewness is approximately 1.834. Since this variable is binary, its mean indicates that approximately 16.2% of customers are senior citizens. Its positive skewness reflects the larger proportion of customers coded as non-senior citizens.

Because this is a binary variable, its distribution is best understood through category proportions rather than treating it as a continuous measurement.

### 3.2 TotalCharges

`TotalCharges` has a mean of approximately 2,283.30 and a median of approximately 1,397.48. Its skewness is approximately 0.962, indicating a positively skewed distribution.

The mean being higher than the median suggests that a smaller group of customers with high accumulated charges pulls the average upward. The median may therefore provide a more representative description of a typical customer's total charges.

### 3.3 Additional Numerical Findings

The `tenure` variable has a mean of approximately 32.37 months, a median of 29 months, and skewness of approximately 0.240, indicating slight positive skewness.

`MonthlyCharges` has a mean of approximately 64.76 and a median of approximately 70.35, with skewness of approximately -0.221. This indicates slight negative skewness.

These findings demonstrate that numerical variables can have different distribution shapes. Skewness, mean, median, and histograms should be interpreted together, considering the meaning of each variable.

## 4. Target Distribution and Class Imbalance

The target variable contains the following classes:

- **No Churn:** 5,174 customers (73.46%).
- **Churn:** 1,869 customers (26.54%).

The target is imbalanced because customers who remained with the company substantially outnumbered those who left.

A classifier that always predicts `No` can achieve approximately 73.46% accuracy on this dataset without identifying a single customer who churned. Therefore, accuracy alone is insufficient for evaluating a churn classifier.

Precision, recall, and F1-score for the churn class should also be considered. Recall is particularly useful for assessing how many actual churners are identified.

## 5. Bivariate Analysis

### 5.1 Contract Type vs. Churn

A comparison of churn rates across month-to-month, one-year, and two-year contracts shows that churn is substantially more common among customers with month-to-month contracts than among customers with longer-term contracts.

This association suggests that contract type is an important variable to investigate in customer retention analysis. However, the results do not establish that contract type alone causes customers to remain with or leave the company. Other characteristics, such as tenure, service subscriptions, and monthly charges, may also be relevant.

### 5.2 Tenure vs. Churn

A boxplot and grouped descriptive statistics were used to compare customer tenure between the two churn categories.

Customers who churned generally have shorter subscription histories, whereas customers who remained tend to have longer tenures. This pattern suggests that customers in the early stages of their relationship with the company may represent an important group for further retention analysis.

The observed relationship is an association and should not be interpreted as proof of causation.

### 5.3 Monthly Charges vs. Churn

Monthly charges were compared between customers who churned and those who remained using boxplots and descriptive statistics.

The comparison investigates whether the distribution of monthly charges differs by churn status. Monthly charges may help distinguish customer groups, but they should be interpreted alongside contract type, tenure, and subscribed services rather than considered in isolation.

The boxplots and grouped statistics provide descriptive evidence of differences between the groups; they do not establish that higher or lower charges directly cause churn.

## 6. Multivariate Analysis

Churn rates were also examined across combinations of contract type and internet service. This analysis provides additional context because churn behaviour may differ across groups with different contract arrangements and service subscriptions.

Tenure groups were created to examine how churn rates vary across customer subscription durations and contract types. These grouped comparisons can help identify customer segments for further investigation.

The results are descriptive and do not establish causal relationships.

## 7. Correlation Analysis

A correlation heatmap was created for `SeniorCitizen`, `tenure`, `MonthlyCharges`, and `TotalCharges`.

The strongest positive relationship is expected between `tenure` and `TotalCharges`, because customers who remain subscribed longer generally accumulate more charges. `MonthlyCharges` is also related to `TotalCharges`, although the relationship is not exact because service subscriptions and prices may change over time.

The relationship between `tenure`, `MonthlyCharges`, and `TotalCharges` is important for future feature engineering. `TotalCharges` partly reflects subscription duration and recurring charges, so these variables may contain overlapping information.

Correlation describes the direction and strength of a linear relationship. It does not establish causation.

## 8. Outlier Review

Potential outliers were investigated using the Interquartile Range (IQR) method and boxplots for `tenure`, `MonthlyCharges`, and `TotalCharges`.

Observations outside the IQR boundaries were treated as potential outliers rather than automatic data errors. High total charges may reflect long-term customers, while unusual monthly charges may represent valid service arrangements.

No observations were removed solely because they were flagged as potential outliers.

## 9. Naive Baseline Implications

The majority-class baseline always predicts `No Churn`, the most frequent target class. Its expected full-dataset accuracy is approximately 73.46%, while precision, recall, and F1-score for the churn class are zero.

This baseline demonstrates that a seemingly reasonable accuracy score can conceal a complete inability to identify customers who leave. It provides a simple reference point for evaluating future classification models.

The baseline metrics are descriptive full-dataset results, not test-set performance.

## 10. Conclusion

The exploratory analysis identified an imbalanced target variable, 11 missing `TotalCharges` values associated with zero-tenure customers, and different distribution patterns among numerical features.

The bivariate analyses examined relationships between churn and contract type, tenure, and monthly charges. Multivariate comparisons explored churn across contract, internet service, and tenure groups. Correlation analysis highlighted the relationship between accumulated charges and other numerical variables.

These findings provide a foundation for future classification work. Subsequent models should be evaluated against the majority-class baseline using churn-specific precision, recall, and F1-score alongside accuracy.

This analysis identifies associations and patterns in the dataset; it does not establish causal relationships.