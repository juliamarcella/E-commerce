🛒 E-Commerce Retail Analysis & Customer Intelligence
Exploratory analysis, customer segmentation, and revenue prediction on a real-world online retail dataset — uncovering who the customers are, how they behave, and what they're likely to spend next.

📌 Project Overview
This project goes beyond surface-level sales reporting. Starting from raw transaction data, it builds a full customer intelligence pipeline: cleaning messy data, identifying behavioral patterns, segmenting customers into meaningful groups, and predicting future revenue using machine learning.
The goal is to answer questions a real e-commerce business would care about:

Which products and countries drive the most revenue?
Are cancellation rates a concern?
Who are our most valuable customers — and what do they buy?
Can we predict how much a customer will spend in the future?


📂 Dataset
Source: Online Retail Transactions Dataset via Kaggle
Coverage: Transactions from a UK-based online retailer
Key fields: Invoice number, stock code, product description, quantity, invoice date, unit price, customer ID, country

🔍 Analysis Breakdown
1. Data Cleaning & Feature Engineering

Removed products with missing descriptions (all had a unit price of £0, confirming they were safe to drop without distorting the analysis)
Identified negative quantities as cancellations and flagged them with a cancel column rather than blindly dropping them
Removed statistical outliers using IQR filtering on both quantity and total price
Engineered a total_price column (quantity × unit_price) and a month period column for time-series analysis

2. Exploratory Data Analysis

Top 10 products by volume and by revenue
Top 10 countries by quantity sold
Monthly sales trend over the full date range
Cancellation rate analysis — the rate was found to be very low, consistent with healthy e-commerce benchmarks

3. RFM Customer Analysis
Customers were scored on three behavioral dimensions:
DimensionDefinitionRecencyDays since last purchaseFrequencyNumber of unique invoicesMonetaryTotal revenue generated
Key findings:

Average customer returns every 91 days
Most customers make 1–5 purchases, but a small group of power users place hundreds of orders
Average spend per customer is ~£2,453, with a wide range suggesting a mix of retail and likely B2B buyers

4. Cohort & LTV Analysis

Customers grouped into acquisition cohorts by their first purchase month
Cumulative average LTV tracked across cohort months to understand how customer value builds over time

5. K-Means Customer Segmentation

RFM features scaled with StandardScaler before clustering
Optimal number of clusters (k=3) selected using the Elbow Method
PCA applied to reduce dimensionality for visualization
Customers with monetary value > £50,000 excluded from clustering to avoid distortion by bulk/B2B buyers
Top products identified per cluster to understand what each segment actually buys

6. CLV Prediction (Random Forest)
A machine learning model was trained to predict each customer's future revenue using behavioral features:

Recency, Frequency, Monetary (RFM)
Average order value
Days active
Number of unique products purchased
Number of unique countries (purchase geography)
Country encoded as a numeric feature

Target variable (future_revenue) was log-transformed before training to handle the right-skewed distribution of customer spend.
MetricScoreR²0.755MAE£78.40RMSE£250.54
The model explains 75.5% of the variance in future customer revenue. Remaining error is largely driven by unpredictable high-spend customers — an inherent challenge in CLV modelling.

🛠 Tech Stack
ToolPurposePythonCore analysis languagePandas & NumPyData wrangling and feature engineeringMatplotlib & SeabornExploratory visualizationsScikit-learnClustering, PCA, and predictive modellingKaggleHubDataset ingestionJupyter NotebookDevelopment environment

📈 Key Findings

Cancellation rates are low and healthy — no immediate concern for the business
A small segment of high-frequency, high-value customers disproportionately drives revenue, typical of a B2B-influenced retail dataset
K-Means clustering revealed 3 distinct customer profiles with meaningfully different purchase behaviors and preferred products
A Random Forest model achieves R² = 0.755 on CLV prediction, providing a reliable foundation for targeting and retention strategy


🚧 Next Steps

 Build a Looker Studio dashboard to visualize sales trends, customer segments, and CLV by cluster
 Investigate cancellation drivers — do specific products, countries, or customer segments cancel more?
 Explore time-series forecasting for monthly revenue
 Add SQL-based data extraction layer to simulate a production analytics environment


👩‍💻 About This Project
This project was developed independently as part of my data analytics portfolio. All steps — from data cleaning to modelling — were designed and implemented by me.
