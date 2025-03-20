# Next Month Loan Performance Prediction & Analysis

## Project Overview
This project, in partnership with Freddie Mac, aims to predict loan transitions within 60 days in California. The analysis spans data from 1999 to 2024, covering various economic conditions, including the Great Recession and the COVID-19 pandemic. The primary goal is to determine trends in loan performance over the years based on significant economic and borrower features to enhance financial decision-making

## Business Objectives
- Develop a model to forecast the monthly transition of 60-day past-due loans in California.
- Assist Freddie Mac in identifying potential default loans.
- Support more informed financial decision-making using data-driven strategies.

## Key Goals
1. **Accurate Loan Transition Prediction** – Forecast monthly loan status transitions.
2. **Comprehensive Feature Analysis** – Evaluate key features affecting loan performance.
3. **Leverage Historical Data** – Use data from 1999-2024 to identify economic trends.
4. **Model Optimization and Validation** – Build, test, and optimize the multinomial logistic regression model.

---

## Data Highlights
### Data Sources
- **Primary Dataset**: Single Family Loan-Level Dataset ([Freddie Mac](https://www.freddiemac.com/research/datasets/sf-loanlevel-dataset))
  - Standard Origination Data (1999–2024): 40+ million rows
  - Standard Monthly Performance Data (1999–2024): 2000+ million rows
- **Supplemental Data:**
  - [Freddie Mac House Price Index (FMHPI)](https://www.freddiemac.com/research/indices/house-price-index): 260k rows
  - [California Unemployment Rate Data](https://data.ca.gov/dataset/civilian-unemployment-rate-for-us-and-california)

### Key Data Preparation Steps
- **Data Cleaning:**
  - Handled missing values using median/mode or related variables.
  - Standardized feature definitions across years.
- **Feature Selection:**
  - Focused on records where delinquency status equals 2 (over 60 days past due).
  - Generated approximately 480k records by including corresponding next-month records.
 <img width="650" alt="feature selection" src="https://github.com/xhartonx/Freddie_Mac_Month_Loan_Performance_Prediction/blob/main/asset/feature%20selection.jpg">
 
- **Feature Engineering:**
  - Created features like LTV_Difference, Loan_Age_Percentage, and dynamic unemployment rate changes.
 
- ### Current Loan Delinquency Status *(Supplementary Information)*
  - Each loan is assigned a **status** based on its delinquency level, for examples:

    - **Status 0** = Current or less than 30 days delinquent
    - **Status 1** = 30-59 days delinquent
    - **Status 2** = 60-89 days delinquent
    - **Status 3** = 90-119 days delinquent
    - **...** = Further delinquency stages
    - **Status RA** = REO Acquisition
---

## Model Description
### Model Objective
- Predict the next month's loan status for loans overdue by 60 days.

### Model Selection
- **Final Model**: Multinomial Logistic Regression
- **Alternative Considered**: Random Forest, XGBoost

### Why Multinomial Logistic Regression?
1. **Multi-Class Prediction** – Can handle multiple loan statuses.
2. **Interpretability** – Provides coefficient insights useful for business decisions.
3. **Computational Efficiency** – Less resource-intensive than Random Forest or XGBoost.
4. **Overfitting Risk Reduction** – Lower risk compared to complex ensemble models.

### Training Process
1. **Data Splitting**
   - Training: Data before January 2019.
   - Testing: Data after January 2019.
2. **Feature Scaling**
   - StandardScaler applied for logistic regression compatibility.
3. **Model Training**
   - Optimized with **lbfgs solver** for multinomial classification.

---

## Findings & Insights
- **Overall Model Accuracy**: **62%**
<img width="500" alt="accuracy" src="https://github.com/xhartonx/Freddie_Mac_Month_Loan_Performance_Prediction/blob/main/asset/model%20performence.jpg">

- **Best Performance**: Predicting transitions from **status 2 to status 3**.
- **Worst Performance**: Predicting transitions to **status 1**.
<img width="500" alt="confusion matrix" src="https://github.com/xhartonx/Freddie_Mac_Month_Loan_Performance_Prediction/blob/main/asset/confusion%20matrix.jpg">


### COVID-19 Impact
- **Prediction Mismatch (April-July 2020)**
  - The model predicted an **increase** in **status 2** loans.
  - In reality, **status 2 loans decreased**, while **status 3 increased**.
<img width="550" alt="confusion matrix" src="https://github.com/xhartonx/Freddie_Mac_Month_Loan_Performance_Prediction/blob/main/asset/status%202%20increase.jpg">
<img width="550" alt="confusion matrix" src="https://github.com/xhartonx/Freddie_Mac_Month_Loan_Performance_Prediction/blob/main/asset/status%203%20increase.jpg">

- **Unemployment Rate Surge**
  - The rapid increase in unemployment was not captured well by models trained prior to 2019.
<img width="550" alt="confusion matrix" src="https://github.com/xhartonx/Freddie_Mac_Month_Loan_Performance_Prediction/blob/main/asset/uneployment%20rate.jpg">
 
- **Unexpected Borrower Trends**
  - A higher proportion of "Very Good" and "Exceptional" credit score borrowers transitioned to status 3 during COVID-19.
<img width="550" alt="confusion matrix" src="https://github.com/xhartonx/Freddie_Mac_Month_Loan_Performance_Prediction/blob/main/asset/credit%20score.jpg">

### Summary
1. The model underperformed during the COVID-19 pandemic (April–July 2020), likely due to its reliance on pre-2019 data, which did not account for the sudden unemployment surge.
2. Loans shifting from status 2 to status 3 during the pandemic included more borrowers with "Very Good" and "Exceptional" credit scores than before COVID.

   **Hypothesis:** High-income borrowers with expensive homes often have high spending habits, making them vulnerable to sudden economic changes. Their defaults pose a 
   greater risk to Freddie Mac due to larger loan amounts.

---

## Challenges & Workarounds
| **Challenge** | **Workaround** |
|--------------|--------------|
| Interpreting Data Definitions | Referenced industry standards & domain knowledge |
| Handling Missing/Inconsistent Data | Used median/mode, related variables, and standardization |
| Model Selection Complexity | Chose multinomial logistic regression for balance of performance and interpretability |

---

## Recommendations & Business Opportunities
1. **Refining the Model with Pandemic Insights**
   - Ensure better handling of unexpected economic shocks.
2. **Proactive Engagement with High-Credit Borrowers**
   - Further investigate behavioral trends among borrowers with strong credit scores.
3. **Scenario Analysis & Stress Testing**
   - Prepare for unpredictable shifts in borrower behavior.
4. **Early Warning Systems**
   - Offer refinancing options for high-risk borrowers.
5. **Stability Assurance Mortgage Products**
   - Provide products to support borrowers during financial uncertainty.
6. **Financial Counseling & Education**
   - Help borrowers understand financial impacts during economic downturns.

