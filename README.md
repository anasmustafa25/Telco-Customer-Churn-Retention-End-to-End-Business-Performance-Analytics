# Telco-Customer-Churn-Retention-End-to-End-Business-Performance-Analytics
An end-to-end data analytics and business intelligence solution analyzing customer churn behavior, statistical pricing drivers, tenure-based flight risk, and high-risk customer segmentation using the IBM Cognos Telco dataset.

Dashboard Preview

<img width="1478" height="822" alt="image" src="https://github.com/user-attachments/assets/67f20517-6158-4ed7-9f3a-60d0de451975" />

Telco Customer Churn: End-to-End Business Performance Analytics

An end-to-end data analytics and business intelligence solution analyzing customer churn behavior, statistical pricing drivers, tenure-based flight risk, and high-risk customer segmentation using the IBM Cognos Telco dataset.

Dashboard Preview

Executive Summary & Core KPIs

Total Customers: 7,043 Unique Accounts
Total Churned Customers: 1,869 Accounts
Overall Churn Rate: 26.54%
Average Monthly Charges: $64.76
Monthly Revenue at Risk: $139,130.85

Project Structure & Deliverables

├── analysis.ipynb                 # Python EDA, data cleaning, feature engineering & hypothesis testing
├── WA_Fn-UseC_-Telco-Customer-Churn.csv  # Raw Telco dataset (7,043 customer records)
├── Task4_Final_Summary.pdf        # Executive 2-page report with empirical findings & recommendations
├── Task4_Churn_Dashboard.pbix     # Interactive Power BI dashboard file
└── README.md                      # Project documentation and summary

Data Architecture & Relational Model

The cleaned dataset (Telco_Churn_Cleaned) evaluates 21 demographic, billing, and subscription variables:
Account Dimensions: customerID, gender, SeniorCitizen, Partner, Dependents
Contract & Billing: tenure, Contract, PaperlessBilling, PaymentMethod, MonthlyCharges, TotalCharges
Subscribed Services: PhoneService, MultipleLines, InternetService, OnlineSecurity, OnlineBackup, DeviceProtection, TechSupport, StreamingTV, StreamingMovies
Engineered Segments & Cohorts:
Tenure_Group: Binned customer tenure (0-12, 13-24, 25-48, 49+ Months)
Customer_Segment: Value-risk quadrants (High-Risk New, Standard New, High-Value Loyal, Standard Retained)
Churn_Flag: Binary target representation (1 for Churned, 0 for Retained)

Key DAX Measures (Power BI)

// Total Customer Base
Total Customers = COUNTROWS('Telco_Churn_Cleaned')

// Churned Customer Count
Churned Customers = CALCULATE(COUNTROWS('Telco_Churn_Cleaned'), 'Telco_Churn_Cleaned'[Churn] = "Yes")

// Overall Churn Rate
Churn Rate =
DIVIDE(
[Churned Customers],
[Total Customers],
0
)

// Average Account Monthly Fee
Avg Monthly Charge = AVERAGE('Telco_Churn_Cleaned'[MonthlyCharges])

// Monthly Recurring Revenue at Risk
Monthly Revenue at Risk =
CALCULATE(
SUM('Telco_Churn_Cleaned'[MonthlyCharges]),
'Telco_Churn_Cleaned'[Churn] = "Yes"
)

Python Visualizations (analysis.ipynb)

Correlation Heatmap & Feature Associations: Bivariate correlation matrix identifying features tied to Churn_Flag.
Tenure Attrition Decay Curve: Histogram and KDE showing churn volume dropping from the initial 12-month period to later tenure stages.
Monthly Fee Density Distribution: Box and violin plot comparisons confirming higher median billing charges for lost accounts.
Contract-Level Survival Matrix: Stacked percentage distributions of cancellations across Month-to-month, 1-year, and 2-year accounts.
Payment Friction Bar Chart: Breakdown showing higher attrition on manual payment forms compared to automated methods.
Segment Risk Matrix: Multi-variable scatter visualization illustrating customer positioning across tenure, monthly fees, and churn status.

Strategic Business Insights

Contract Commitment Gap: Month-to-month users churn at 42.71%, compared to 11.27% for 1-year contracts and 2.83% for 2-year contracts. Action: Offer a guaranteed 12-month rate-lock or a $10/month credit for 6 months to convert flexible accounts into annual commitments.
First-Year Vulnerability Window: Attrition peaks at 47.44% during months 0–12 and falls to 9.51% past month 48. Action: Deploy automated customer success check-ins on Days 15, 30, 60, and 90 to identify setup and connection issues early.
Monthly Price Surcharge & Value Fatigue: Churned subscribers pay an average of $74.44/month versus $61.27/month for retained customers (+$13.17 surcharge). Action: Audit high-tier bundles and provide proactive pricing relief before accounts churn.
Payment Channel Friction: Customers paying via electronic check churn at 45.29%, compared to 15.24% for credit card and 16.71% for bank transfer auto-pay. Action: Provide a one-time $15 account credit for enrolling in automated bank debit or credit card billing.
Protective Add-On Deficit: Accounts without Tech Support churn at 41.64% (vs. 15.17% with), and those lacking Online Security churn at 41.77% (vs. 14.61% with). Action: Bundle 90 days of complimentary security and tech support packages into high-tier Fiber Optic plans.
High-Risk New Cohort Concentration: The High-Risk New segment (tenure ≤12 months, fees ≥$65) shows a 66.43% churn rate with an average bill of $81.72/month. Action: Set up automated early-warning alerts for high-bill accounts in their first year that log technical tickets or show declining usage.

Setup & Reproduction

Clone the Repository: git clone  cd telco-churn-analytics

Run Python Analysis & Hypothesis Testing: pip install pandas numpy scipy matplotlib seaborn
jupyter notebook analysis.ipynb

Open Power BI Dashboard: Double-click Task4_Churn_Dashboard.pbix in Power BI Desktop to interact with slicers, cross-filtering, and bookmark resets.

Review the Final Summary PDF: Open Task4_Final_Summary.pdf for the complete two-page executive presentation, hypothesis validation tables, customer segmentation breakdown, and the 90-day implementation roadmap.
