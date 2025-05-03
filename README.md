# Bank Transaction Fraud Detection
## Table Of Content
- [Overview](https://github.com/pheenarh/BANK-TRANSACTION-FRAUD-DETECTION/edit/main/README.md#overview)

- [Problem Statement](https://github.com/pheenarh/BANK-TRANSACTION-FRAUD-DETECTION/edit/main/README.md#problem-statement)

- [Tools Used](https://github.com/pheenarh/BANK-TRANSACTION-FRAUD-DETECTION/edit/main/README.md#tools-used)

- [Steps I took](https://github.com/pheenarh/BANK-TRANSACTION-FRAUD-DETECTION/edit/main/README.md#steps-i-took)

  -  [Data Collection And Description](https://github.com/pheenarh/BANK-TRANSACTION-FRAUD-DETECTION/edit/main/README.md#data-collection--description)

  -  [Data Cleaning And Preparation](https://github.com/pheenarh/BANK-TRANSACTION-FRAUD-DETECTION/edit/main/README.md#data-cleaning--preparation)

  -  [Data Analysis](https://github.com/pheenarh/BANK-TRANSACTION-FRAUD-DETECTION/edit/main/README.md#data-analysis)

- [Visualization](https://github.com/pheenarh/BANK-TRANSACTION-FRAUD-DETECTION/edit/main/README.md#visualization)

- [Key Findings And Insights](https://github.com/pheenarh/BANK-TRANSACTION-FRAUD-DETECTION/edit/main/README.md#key-findings--insights)

- [Recommendations](https://github.com/pheenarh/BANK-TRANSACTION-FRAUD-DETECTION/edit/main/README.md#recommendations)

- [Conclusion](https://github.com/pheenarh/BANK-TRANSACTION-FRAUD-DETECTION/edit/main/README.md#conclusion)

## Overview
This project analyses banking transaction data to uncover transactional behaviour, exploring fraud detection and anomaly identification. The analysis covers transaction volumes, transaction type, channel usage and customer type.

## Problem Statement
The goal of this analysis is to explore fraud detection and identify transaction anomaly. Understand the transaction pattern based on customer occupation. This can help identify anomaly in transaction pattern and detect fraudulent transactions.

## **Tools Used:**
  - Excel: For Data cleaning and Preparation
  - Power BI: Dashboard Creation for intuitive analysis and visualization

## **Steps I Took:**
## Data Collection & Description
The dataset is a real-life dataset gotten from Kaggle (Bank Transaction Dataset for Fraud Detection). It contains 2,512 samples of transaction data, covering various transaction attributes, customer demographics, and usage patterns. The dataset contains columns for transaction ID, account ID, transaction type, transaction date, transaction amount, location, Device IP, IP address, merchant ID, channel, Customer age, customer occupation, transaction duration, login attempts, account balance.

## Data Cleaning & Preparation
I noticed that the previous transaction date column had future dates compared to the transaction date, which is logically inconsistent. For example, a transaction on June 2023 showing a previous transaction date in 2024. This suggests either a data entry error or an issue with how the dataset was generated. I flagged it during cleaning and choose to remove that column as it was supposed to be used for time-gap based anomaly detection.

I used Excel to standardized the transaction date, transaction amount and account balance formats for easier analysis. I created 4 columns:  High transaction flag, Multiple logins attempt flag, Occupation Flag, Potential Anomaly.

## Data Analysis
**Using the IF function in excel:**

- High Transaction Flag: I flagged transaction amounts that are over $1,000 as suspicious so as to be able to take a closer look at the patterns.

- Multiple Login Attempts Flag: I flagged transactions with more than 3 login attempts as this could be considered suspicious login attempt and hence fraudulent attempt.

- Occupation Flag: I flagged transaction based on customer’s occupation. For instance, a student making a withdrawal of over $1,000 could be considered suspicious.

- Potential Anomaly: Based on the above criteria, I created a resulting column to flag potential fraud with the condition where the other three columns are suspicious.


**Using Measures in Power BI:**

- **Total transactions:** I calculated the total transactions using;

  ***Total Transactions = COUNTX ('Bank Transactions Fraud Cleaned', 'Bank Transactions Fraud Cleaned'[Transaction ID])***

- **Suspicious Transaction Count:** I calculated the suspicious transaction count using;

  ***Suspicious Transaction Count = CALCULATE (COUNTROWS ('Bank Transactions Fraud Cleaned'), 'Bank Transactions Fraud Cleaned'[Potential Anomaly] = "Potential Fraud")***

- **Transaction Amount by Occupation:** I calculated the transaction amount by occupation using;

  ***Transaction Amount by Occupation = SUM ('Bank Transactions Fraud Cleaned'[Transaction Amount])***

- **Suspicious Transaction Percent:** I calculated the percentage of suspicious transactions to the total transactions using;

  ***Suspicious Transaction Percent = CALCULATE ([Suspicious Transaction Count]/[Total Transactions]) * 1.0***

## Visualization
![image](https://github.com/user-attachments/assets/1aaa280d-d795-44ab-ae42-66e0cc7b6ec8)


## Key Findings & Insights
- **Customer Occupation Risk Analysis**
    Students dominate the suspicious transaction count significantly with 148 suspicious transactions.
    Other Occupations like doctors and retired individuals follow but with much lower counts. Students appear to be more vulnerable or involved in fraudulent activities.
  ![S transaction by occupation](https://github.com/user-attachments/assets/546289d3-6d2e-435e-bd1d-cf987ce98c18)


- **Transaction Amount by Occupation**
    Transaction amounts are relatively high across occupations like student, doctor and engineer. High transaction amounts combined with suspicious activity in specific 
    groups could signal riskier profiles.
  ![T amount by occupation](https://github.com/user-attachments/assets/8c9ac511-a1d1-423c-8ac6-d9eac89acbbe)


- **Channel Performance and Risk**
    ATM channel accounts for most suspicious transactions. Online transactions have lower suspicious counts, implying either better controls or lower usage of the channel.
  ![S transaction by channel](https://github.com/user-attachments/assets/198da6cc-3974-418c-ae81-d11294e5b168)


- **Transaction Type Analysis**
    Debit transactions account for the majority of suspicious activities compared to credit transactions. This indicates that fraudulent activities are more common with 
    debit transactions.
  ![S transaction by T type](https://github.com/user-attachments/assets/b8283eb1-1011-4b93-99e4-0e928e07011f)


- **Suspicious Transaction Rate**
    Out of the 2,512 total transactions, about 256 are flagged as suspicious. This means approximately 10.19% of all transactions are suspicious. This is quite significant 
    and a more thorough investigation should be considered.
  ![fraud KPI](https://github.com/user-attachments/assets/1d267b5d-7999-49ad-914e-4bec924d2d4f)


- **Top Locations with Suspicious Transactions**
    San Diego, Austin and Detroit are the top cities with the highest number of suspicious transactions. These cities recorded between 10 to 12 suspicious transactions 
    each. 
    Concentration in specific urban regions suggest targeted fraud activities which needs to be looked into.
  ![S transaction location](https://github.com/user-attachments/assets/65cae548-9052-43a5-85dc-525914489e5c)


## Recommendations
- **Targeted Monitoring for High-Risk Locations**
    Increase monitoring and preventive controls in San Diego, Austin, Detroit, Los Angeles and other top suspicious locations. The implementation of a location-based fraud 
    detection rules should be considered.

- **Strengthen ATM Security**
    Since ATM channel is the most exploited, enhance the security measures around this channel and a more strict authentication method should be put in place.

- **Student-focused Awareness Campaigns**
    Launch fraud awareness programs targeting students, educating them on how fraudsters operate and how to secure their accounts. Also educate them on the implication of 
    money laundering and being involved in fraudulent activities.

- **Analyse Debit Transactions more deeply**
    Since debit transactions show higher fraud rates, implement a stricter fraud checks for debit card usage and also conduct enhanced due diligence when a customer is 
    making a suspicious withdrawal amount in the branch.
    Also explore transaction patterns like multiple small transactions or cross-region usage of debit cards.

- **Dynamic Risk Scoring**
    Implement a dynamic risk scoring model based on location, occupation, transaction type and amount to prioritize transaction reviews. This will help flag suspicious 
    transactions based on real-time.

- **Review Large Transactions in High-Risk Occupations**
    Pay closer attention to high transaction amounts from students whether credit or debit and newly registered accounts to detect potential money laundering activities 
    early.

## Conclusion
This analysis provides a comprehensive overview of customer transaction patterns and highlights key areas of potential fraud risk. Out of 2,512 transactions, 256 (approximately 10.19% were identified as suspicious. A deeper analysis reveals that; 
- Student account for the highest number of suspicious transactions by occupation.
-	Atm channel is the most common medium for flagged transactions.
-	San Diego, Austin and Detroit rank as the top locations with the highest suspicious transaction counts.
-	The majority of suspicious transactions are carried out via debit cards, making it a key area to monitor.

This analysis emphasizes the need for continuous monitoring of transactional behaviour, particularly across high-risk occupations, channels and locations.




