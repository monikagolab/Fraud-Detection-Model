# Fraud-Detection-Model
E-Commerce Fraud Detection Model

# Machine-Learning-Project
E-commerce Fraud Detection Model

**I. Problem Statement** 

**Context:** The E-commerce industry faces a continuous threat from sophisticated fraudulent actors. This is a synthetic dataset that provides a simulation of 1.47 million transactions, where approximately 5% are flagged as fraudulent. Unlike simple transactional logs, this data includes customer demographics (Age, Location), technical fingerprints (IP Address, Device Used), and account history (Account Age), providing a holistic view of each purchase.

**The Core Problem:** The goal is to build a classification model that leverages the relationship between user identity, device metadata, and transactional behavior to predict the likelihood of fraud (Is Fraudulent). Specifically, the model must distinguish between a legitimate high-value purchase and a fraudulent one by identifying anomalies in the IP-to-Location mapping and the Account Age-to-Amount ratio.

**Key Technical Challenges:**

Behavioral Profiling: Determining how features like Account Age Days and Transaction Hour correlate with fraudulent behavior (e.g., do newer accounts with high-value orders pose a higher risk?).

Mismatched Identity: Analyzing the relationship between Shipping Address and Billing Address to detect potential "dropshipping" fraud.

Device & Network Intelligence: Effectively encoding categorical data like Device Used and Payment Method to identify high-risk channels.

Success Metrics: The primary metric will be F1-Score (to balance the capture of fraud with the preservation of the customer experience) and Precision-Recall AUC, ensuring the model remains effective despite the 95:5 class imbalance.

**II. Solution Approach**

                ________________________________FEATURE ENGINEERING___________________________

Features identified from the data set: 

-**Transaction Metadata**: Transaction ID, User ID, Timestamp

-**Transaction Specifics**: Transaction Amount, Payment Method (PayPal, credit card, debit card, bank transfer), Product Category (electronics, toys & games, clothing, health & beauty, home & garden, etc.), Quantity, Account Age Days, Transaction Hour

-**User Info**: Customer Age, City, Device Used (desktop, mobile, tablet)

-**Location / Shipping**: Billing Address, Shipping Address, Customer Location, IP Address

OUR DEPENDENT (TARGET) VARIABLE: **Is Fraud**

                 ________________________________ALGORITHM SELECTION______________________________

**Logistic Regression**
Logistic Regression was chosen because it allows for direct observation of how features like Transaction Amount or Account Age contribute to the probability of fraud via their coefficients. Additionally, it maps features to a 0–1 range using the Sigmoid function, which is ideal for binary financial classification tasks.

To address the class imbalance:
To ensure the model didn't simply ignore the minority "Fraud" class, we focused on:
Precision-Recall Trade-off: Area Under the Precision-Recall Curve (AUPRC) was prioritized over standard accuracy to better reflect the model's ability to identify rare fraud events.

Strategic Thresholding: The model was evaluated based on its ability to maximize Recall.

EVALUATION
According to the experimental results:

The Results: The model successfully identified 180 fraudulent transactions (True Positives), but struggled with 1,026 False Positives.

Financial Impact: In a real-world scenario, this high recall is beneficial for security, but the low precision highlights a significant "customer friction" cost where many legitimate users would be incorrectly flagged.

**Random Forest**
Random Forest was chosen to capture complex, non-linear relationships within the transactional data that simpler models might miss. It is highly effective at identifying fraud patterns that rely on a combination of factors. 

To address the class imbalance:
Using Stratified K-Fold ensured that each cross-validation fold maintained the critical 5% fraud ratio.

Hyerparameters:
We utilized RandomizedSearchCV with Stratified K-Fold cross-validation to tune the number of trees in the forest & its maximum depth.


**SVM**
A Support Vector Machine was implemented to test if a higher-dimensional boundary could better isolate fraudulent transactions from legitimate ones. SVM is designed to be less sensitive to individual outliers that don't fall near the decision boundary, which is helpful in noisy e-commerce data. As stated in the lecture notes, SVMs are a staple in credit scoring and fraud detection due to their mathematical rigor and ability to handle high-dimensional feature sets

To address the class imbalance:
Cost-Sensitive Learning: In our implementation, we can adjust the C parameter (the penalty for misclassification). For this dataset, we assigned a higher cost to misclassifying the "Fraud" class to force the model to prioritize catching the 5% minority.
Handling the "Overlap": SVM was chosen to see if it could find a more complex, non-linear boundary that reduces the number of "False Positives" seen in the baseline models.

Hyperparameter tuning:
Stratified K-Fold cross-validation was utilized to ensure that the 5% minority fraud class was represented proportionally in every training and validation fold. This prevented the model from training on subsets that lacked fraudulent examples and provided a more stable, reliable estimate of performance metrics like Average Precision when handling the inherent class imbalance of financial data.

RandomizedSearchCV was utilized for hyperparameter tuning to efficiently explore a wide range of parameter values without the exhaustive computational cost of a full grid search.

**Overall Evaluation**
While the algorithms were effective at Recall (catching the majority of fraudulent transactions), they all produced a high volume of False Positives.The use of Stratified K-Fold and RandomizedSearchCV ensured that all models were evaluated fairly on the 5% minority class. However, the low precision suggests that the "Fraud" and "Non-Fraud" classes in this dataset are not easily separable by current feature signals. The combined evaluation indicates that while the technical pipeline (stratification, tuning, and scaling) was executed correctly, the inherent nature of the dataset poses a limit on precision.


              ________________________________BUSINESS APPLICATION______________________________
              
**Criteria for Success when applied to a business**
High Recall: Maximizing the detection of actual fraudulent transactions to minimize direct financial loss.

Precision Stability: Maintaining a low "False Positive" rate to prevent blocking legitimate customers and causing "reputational" damage.

AUC-PR Performance: Achieving a high Area Under the Precision-Recall Curve, which is a more reliable success metric than accuracy for rare-event financial data.

**Constraints when applied to a business**
Latency: The model must process transactions in milliseconds to support real-time e-commerce checkouts.

Class Imbalance: The 5% fraud rate limits the model's ability to learn distinct patterns without heavy reliance on sampling techniques like SMOTE.

Data Quality: Synthetic datasets (like the one used here) may lack the complex behavioral nuances found in real-world adversarial fraud, creating a "performance plateau".

