Overview

This project uses a Logistic Regression model to predict whether a bank customer will subscribe to a term deposit.

Dataset
File: bank-full.csv
Size: 45,211 rows and 17 columns
Target Variable: y (yes/no — indicates whether the customer subscribed)
Methodology

1. Data Loading and Exploration
All necessary libraries were imported, and the dataset was loaded using Pandas with a semicolon (;) delimiter. Initial exploration was performed to understand the structure and class distribution.

2. Data Cleaning
Irregular values such as -1 in the pdays column and "unknown" in categorical features were identified and replaced with NaN to represent missing data. The dataset was then rechecked to ensure proper cleaning.

3. Handling Missing Values
Missing data was imputed using the most frequent values for some features, while others were filled with a placeholder such as "none".

4. Outlier Treatment
Extreme values in numerical features like balance, duration, and campaign were clipped to reduce their impact.

5. Feature Engineering
The target variable was encoded into binary form (yes = 1, no = 0). Categorical variables were transformed using one-hot encoding.

6. Data Splitting and Scaling
The dataset was divided into features (X) and target (y), followed by an 80/20 train-test split. Feature scaling was applied using StandardScaler to normalize input values.

7. Model Training
A Logistic Regression model was trained with class_weight='balanced' to address class imbalance.

8. Model Evaluation
The model was evaluated using accuracy, precision, recall, F1-score, and confusion matrix.

9. Hyperparameter Tuning
Grid Search was applied to optimize model parameters, followed by re-evaluation and comparison of results.

Libraries Used
Pandas — data loading and manipulation
NumPy — numerical operations and handling missing values
Matplotlib — data visualization
Seaborn — enhanced visualizations
Scikit-learn — model building, tuning, and evaluation
Approach
Performed thorough data cleaning and preprocessing before modeling
Addressed class imbalance using balanced class weights
Converted categorical variables using one-hot encoding
Applied feature scaling for consistent input ranges
Used Grid Search to improve model performance
Results
Before Tuning
| Metric    | Score |
| --------- | ----- |
| Accuracy  | 0.84  |
| Precision | 0.42  |
| Recall    | 0.81  |
| F1 Score  | 0.55  |

After Tuning
| Metric    | Score |
| --------- | ----- |
| Accuracy  | 0.90  |
| Precision | 0.65  |
| Recall    | 0.38  |
| F1 Score  | 0.48  |

Conclusion

After hyperparameter tuning, the model achieved higher accuracy and precision but experienced a significant drop in recall. This highlights a trade-off: the tuned model became more conservative in predicting positive cases, resulting in fewer false positives but more missed subscribers.

If the primary goal is to identify as many potential subscribers as possible, the pre-tuned model may be more suitable due to its higher recall.
