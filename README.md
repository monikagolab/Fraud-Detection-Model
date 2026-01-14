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



