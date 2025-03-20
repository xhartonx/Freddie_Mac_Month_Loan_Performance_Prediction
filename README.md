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
### Primary Datasets
- **Freddie Mac Single Family Loan-Level Dataset**
   - **Standard Origination Data (1999-2024)**: 40+ million rows & 32 columns.
   - **Standard Monthly Performance Data (1999-2024)**: 2000+ million rows & 32 columns.
   - **Source**: [Loan-Level Dataset](https://www.freddiemac.com/research/datasets/sf-loanlevel-dataset)
### Supplemental Data Datasets
- **Freddie Mac House Price Index (FMHPI)** – 260k rows & 7 columns.
   - **Source**: [FMHPI Dataset](https://www.freddiemac.com/research/indices/house-price-index)
   - **Importance**: Indicators of housing market trends and economic conditions.

- **Unemployment Rate Data**
   - **Source**: [California Unemployment Data](https://data.ca.gov/dataset/civilian-unemployment-rate-for-us-and-california)
   - **Importance**: Proxy for economic health and its relation to delinquency risk.


### Data Cleaning & Processing
- **Missing Value Handling**
  - Numerical data: Median/mode replacement.
  - Categorical data: Mode or domain knowledge-based placeholders.
- **Data Consistency Adjustments**
  - ELTV values missing before 2017 were filled based on other loan-to-value ratios.
  - Date formats standardized to 'YYYY-MM'.
- **Filtering**
  - Focused on delinquency status of **60 days past due**.
  - Removed non-California records and duplicate entries.

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

### Feature Engineering
- **LTV Difference** = Estimated Loan-to-Value (ELTV) - Original Combined Loan-to-Value (CLTV).
- **Loan Age Percentage** = Loan Age / (Remaining Months to Maturity + 1e-6).
- **Debt-to-Income (DTI) Categorization** = 'Low', 'Middle', 'High', or 'Very High'.
- **Unemployment Rate % Change** = Monthly percentage change in unemployment rate.

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
- **Best Performance**: Predicting transitions from **status 2 to status 3**.
- **Worst Performance**: Predicting transitions to **status 1**.

### COVID-19 Impact
- **Prediction Mismatch (April-July 2020)**
  - The model predicted an **increase** in **status 2** loans.
  - In reality, **status 2 loans decreased**, while **status 3 increased**.
- **Unemployment Rate Surge**
  - The rapid increase in unemployment was not captured effectively by pre-2019 trained models.
- **Unexpected Borrower Trends**
  - A higher proportion of "Very Good" and "Exceptional" credit score borrowers transitioned to status 3 during COVID-19.

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

---

## Credits
This presentation template was created by **Slidesgo**, with icons by **Flaticon**, and infographics/images by **Freepik**.

**Thank You!**
