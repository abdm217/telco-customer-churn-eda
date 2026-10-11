# Naive Majority-Class Baseline — Telco Customer Churn

## 1. Objective

The objective of this baseline is to establish a simple reference point before developing more advanced classification models.

The baseline uses scikit-learn's `DummyClassifier` with the `most_frequent` strategy. It always predicts the majority class, which is `No Churn`.

## 2. Dataset Distribution

The dataset contains 7,043 customer records:

- **No Churn:** 5,174 customers (73.46%).
- **Churn:** 1,869 customers (26.54%).

Since `No Churn` is the majority class, the classifier predicts `No` for every customer.

## 3. Baseline Metrics

The baseline is evaluated on the full dataset for this exploratory analysis.

| Metric | Score |
|---|---:|
| Accuracy | 73.46% |
| Precision for Churn | 0.00% |
| Recall for Churn | 0.00% |
| F1-score for Churn | 0.00% |

These are expected results based on the dataset's target distribution. The notebook contains the code used to calculate the metrics.

## 4. Metric Interpretation

**Accuracy** measures the proportion of all predictions that are correct. The baseline achieves approximately 73.46% accuracy because that proportion of customers belongs to the `No Churn` class.

**Precision for Churn** measures the proportion of predicted churners who actually churned. Since the baseline never predicts churn, its precision is zero under scikit-learn's zero-division handling.

**Recall for Churn** measures the proportion of actual churners correctly identified. Because the baseline predicts no customer will churn, it identifies none of the 1,869 actual churners, giving it zero recall.

**F1-score for Churn** combines precision and recall. Since both are zero for this baseline, its F1-score is also zero.

## 5. Why Accuracy Is Misleading

The baseline appears reasonably accurate, but it fails to identify every customer who churns. This happens because the dataset is imbalanced: customers who remain with the company substantially outnumber customers who leave.

For this reason, accuracy alone is not a sufficient measure of performance in customer churn classification. Precision, recall, and F1-score for the churn class provide essential additional information.

## 6. Conclusion

The majority-class baseline is not intended to be a useful churn prediction system. It establishes a simple benchmark against which future classification models can be compared.

A future model should aim to identify churners while balancing recall, precision, and overall performance. Any future model evaluation should use an appropriate train/test split or cross-validation strategy to estimate performance on unseen data.

**Evaluation note:** The scores reported here are full-dataset baseline metrics for the EDA assignment. They are not test-set metrics and should not be interpreted as evidence of generalization to unseen customers.