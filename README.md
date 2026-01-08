1. Transaction data (most common)

Usually a CSV, Parquet, or database table with rows = transactions.

Typical fields:

transaction_id

user_id / account_id

amount

currency

timestamp

merchant_id

merchant_category

payment_method (card, transfer, wallet, etc.)

country / location

device_id / ip_address

is_fraud (label: 0 = legit, 1 = fraud)

2. Feature file (engineered data)

Used for ML models after preprocessing.

May include:

Transaction velocity (e.g., transactions per hour)

Average spend per user

Distance between transactions

Risk scores

Historical fraud rate per merchant

Example:

user_id,avg_amount_7d,txn_count_1h,merchant_risk_score,is_fraud
U456,180.20,3,0.02,0
3. Model-related files

Used internally by the fraud system:

Trained model (.pkl, .joblib, .onnx)

Configuration files (.yaml, .json)

Threshold and rule definitions

Example (JSON):

{
  "fraud_threshold": 0.87,
  "velocity_limit": 5,
  "high_risk_countries": ["NG", "RU"]
}
4. Logs & alerts

Used for monitoring and investigation:

Fraud alerts

Decision explanations

Rule triggers

Example:

timestamp,transaction_id,alert_reason
2025-01-01 10:15,TX123,High velocity + unusual location
5. Ground truth / investigation outcomes

Used for retraining:

Chargeback results

Manual review decisions

Customer confirmations

transaction_id,user_id,amount,timestamp,merchant,is_fraud
TX123,U456,250.75,2025-01-01 10:15:00,Amazon,0
