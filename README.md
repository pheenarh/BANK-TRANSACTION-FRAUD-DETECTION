# BANK-TRANSACTION-FRAUD-DETECTION
## OVERVIEW
This project analyses banking transaction data to uncover transactional behaviour, exploring fraud detection and anomaly identification. The analysis covers transaction volumes, transaction type, channel usage and customer type.
## PROBLEM STATEMENT
The goal of this analysis is to explore fraud detection and identify transaction anomaly. Understand the transaction pattern based on customer occupation. This can help identify anomaly in transaction pattern and detect fraudulent transactions.
## DATA COLLECTION AND DESCRIPTION
The dataset is a real-life dataset gotten from Kaggle (Bank Transaction Dataset for Fraud Detection). It contains 2,512 samples of transaction data, covering various transaction attributes, customer demographics, and usage patterns. The dataset contains columns for transaction ID, account ID, transaction type, transaction date, transaction amount, location, Device IP, IP address, merchant ID, channel, Customer age, customer occupation, transaction duration, login attempts, account balance.
## DATA CLEANING AND PREPARATION
I noticed that the previous transaction date column had future dates compared to the transaction date, which is logically inconsistent. For example, a transaction on June 2023 showing a previous transaction date in 2024. This suggests either a data entry error or an issue with how the dataset was generated. I flagged it during cleaning and choose to remove that column as it was supposed to be used for time-gap based anomaly detection.

I used Excel to standardized the transaction date, transaction amount and account balance formats for easier analysis. I created 4 columns:  High transaction flag, Multiple logins attempt flag, Occupation Flag, Potential Anomaly.
## DATA ANALYSIS
Using the IF function in excel:

a. High Transaction Flag: I flagged transaction amounts that are over $1,000 as suspicious so as to be able to take a closer look at the patterns.

b. Multiple Login Attempts Flag: I flagged transactions with more than 3 login attempts as this could be considered suspicious login attempt and hence fraudulent attempt.

c. Occupation Flag: I flagged transaction based on customer’s occupation. For instance, a student making a withdrawal of over $1,000 could be considered suspicious.

d. Potential Anomaly: Based on the above criteria, I created a resulting column to flag potential fraud with the condition where the other three columns are suspicious.


Using Measures in Power BI:

a. Total transactions: I calculated the total transactions using;

Total Transactions = COUNTX ('Bank Transactions Fraud Cleaned', 'Bank Transactions Fraud Cleaned'[Transaction ID])

b. Suspicious Transaction Count: I calculated the suspicious transaction count using;

Suspicious Transaction Count = CALCULATE (COUNTROWS ('Bank Transactions Fraud Cleaned'), 'Bank Transactions Fraud Cleaned'[Potential Anomaly] = "Potential Fraud")

c. Transaction Amount by Occupation: I calculated the transaction amount by occupation using;

Transaction Amount by Occupation = SUM ('Bank Transactions Fraud Cleaned'[Transaction Amount])

d. Suspicious Transaction Percent: I calculated the percentage of suspicious transactions to the total transactions using;

Suspicious Transaction Percent = CALCULATE ([Suspicious Transaction Count]/[Total Transactions]) * 1.0
## VISUALIZATION




