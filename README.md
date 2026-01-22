# Fraud-Detection-Model
E-Commerce Fraud Detection Model

**I. Problem Statement**

E-commerce platforms process thousands of transactions every day, and a small but significant portion of these transactions are fraudulent. Fraudulent transactions lead to direct financial losses, increased chargebacks, and reduced customer trust.

This is a synthethic dataset, only about 5% of transactions are fraudulent, making fraud detection a highly imbalanced, binary classification problem. Traditional accuracy-based models may fail because they tend to favor the majority (non-fraud) class and miss fraudulent activities.

Objective: Build a machine learning model that can accurately identify fraudulent e-commerce transactions using customer and transaction data, while handling class imbalance and maximizing the detection of fraud cases.

**II. Solution Approach**

After exploring the data to understand fraud patterns, key features were engineered such as:
- binary variable "Is Night": marking night transactions that happend between 12 and 5 AM
- binary variable "New Account": created by flagging accounts that are 40 days old or less
- binary variable "High Amount": marking transactions above the 99th percentile of transaction amounts, representing unusually large purchases
These features, combined with interaction variables "Night_NewAccount" and "HighAmount_NewAccount", help the model better distinguish suspicious transactions from normal customer behavior.

Feature selection was performed through an trial-and-error process, testing different combinations of variables and evaluating their impact on model performance. After multiple experiments, the final selected features produced the best results and were therefore kept in the final model. :) 

3 models — *Logistic Regression, Random Forest, and Linear SVM* — were trained and evaluated. A preprocessing pipeline was built to consistently encode categorical variables and scale numerical features (for Logistic Regression and Linear SVM).

To address class imbalance, class_weight="balanced" was used for Logistic Regression and Linear SVM, while class_weight="balanced_subsample" was applied for Random Forest during training.

Hyperparameter tuning for Random Forest and Linear SVM with Stratified 5-Fold CV was applied to optimize model performance. To improve training efficiency, RandomizedSearchCV was used instead of GridSearchCV for hyperparameter tuning, significantly reducing computation time.

Additional threshold tunning was applied for Random Forest, to achieve a recall of 70%. 

**III. Final Results and Evaluation**

Evaluation is done using metrics that reflect real fraud detection needs. Because missing fraud is costly, the approach emphasizes Recall (how many frauds are caught) along with Precision (how many flagged transactions are truly fraud). The F1-score is used as a balanced summary of precision and recall. In addition, the confusion matrix is analyzed to understand the trade-off between false positives and false negatives. Since the dataset is imbalanced, the Average Precision (PR-AUC) is used as key metrics as it provides a more meaningful view of performance than ROC-AUC.

The models are not the best-performing solution, as implied by weak evaluation metrics. A PR-AUC below 0.4 suggests the models do not rank fraudulent transactions consistently higher than non-fraud ones. In evaluation, this translates to a poor trade-off: either many fraud cases are missed (low recall) or too many legitimate transactions are flagged (low precision). Hence, the current model is not optimal and would need improvements. However, since this was the first machine learning model, it served as a strong baseline and helped to understand the complete ML workflow. :)

