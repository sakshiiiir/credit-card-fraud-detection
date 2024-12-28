### Credit Card Fruad Detection

Data: 
- Link: https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud 
- Description: The dataset contains transactions made by credit cards in September 2013 by European cardholders.
This dataset presents transactions that occurred in two days, where we have 492 frauds out of 284,807 transactions. The dataset is highly unbalanced, the positive class (frauds) account for 0.172% of all transactions.
- Features: It contains only numerical input variables which are the result of a PCA transformation. Unfortunately, due to confidentiality issues, we cannot provide the original features and more background information about the data. Features V1, V2, … V28 are the principal components obtained with PCA, the only features which have not been transformed with PCA are 'Time' and 'Amount'. Feature 'Time' contains the seconds elapsed between each transaction and the first transaction in the dataset. The feature 'Amount' is the transaction Amount, this feature can be used for example-dependant cost-sensitive learning. Feature 'Class' is the response variable and it takes value 1 in case of fraud and 0 otherwise.

Data Preprocessing:

- Analyzing Variation: variation of features (Time and Amount) with respect to the Class (Fraud/Non-Fraud).
- Dropping Time:it may not directly contribute to fraud detection.
- Scaling Features:Applied StandardScaler to normalize Amount and other features to ensure consistent scale.
- Transforming Skewed Features:Used PowerTransformer to address skewness and make feature distributions more normal.

Modeling and Addressing Class Imbalance Techniques:

- Random Undersampling (RUS): Reduced the majority class to match the minority class.
- Random Oversampling (ROS): Duplicated samples from the minority class to balance the dataset.
- SMOTE: Applied Synthetic Minority Oversampling Technique to generate synthetic samples for the minority class.

Model Performance: ROC-AUC Score on Unsampled Test Set
- Random Undersampling (RUS):
  - Logistic Regression: 0.96
  - XGBoost: 0.99
  - Decision Tree: 0.97
- Random Oversampling (ROS):
  - Logistic Regression: 0.97
  - XGBoost: 0.97
  - Decision Tree: 0.89
- SMOTE Sampling:
  - Logistic Regression: 0.97
  - XGBoost: 0.96
  - Decision Tree: 0.86
 
Inference:
- Undersampling: significantly reduces the amount of training data and can lead to overfitting,
- Logistic Regression showed promising results with SMOTE.
 
From a Bank's Perspective: For lower amounts, high precision because we only want to label relevant transactions as fraud. For higher amounts, high recall in order to detect actual fraud transactions.
Logistic Regression is a solid choice for this fraud detection problem, as it achieves a good balance between performance (ROC-AUC) and interpretability. Its high recall, especially after applying SMOTE for balancing the dataset, aligns well with the goal of catching fraudulent transactions, even if it means having a few more false positives.



