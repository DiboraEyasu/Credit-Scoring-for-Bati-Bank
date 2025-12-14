# Credit Scoring Risk Probability Model for Alternative Data
# Project Overview
This project implements an end-to-end credit risk scoring model for Bati Bank's buy-now-pay-later partnership with an e-commerce platform. The model transforms customer transaction data into a predictive risk signal using RFM (Recency, Frequency, Monetary) analysis and machine learning techniques.

**Credit Scoring Business Understanding**
**1. Basel II Accord and Model Requirements**
The Basel II Capital Accord establishes a three-pillar framework for banking supervision:

**Pillar 1 (Minimum Capital Requirements):** Directly influences our modeling by requiring banks to maintain capital reserves proportionate to their credit risk exposure. This creates a business imperative for accurate risk quantification.

**Pillar 2 (Supervisory Review):** Requires banks to develop robust internal risk assessment processes and maintain sufficient capital to cover all risks. Our model must be transparent enough for internal validation and regulatory scrutiny.

**Pillar 3 (Market Discipline):** Mandates public disclosure of risk management practices and capital adequacy, creating external pressure for model accountability.

## Impact on Our Model Development:

We must prioritize model interpretability to satisfy Pillar 2 supervisory review requirements.

The model must be well-documented with clear audit trails to demonstrate compliance.

Validation and backtesting capabilities are essential for regulatory approval.

Risk quantification must be precise to ensure adequate capital allocation under Pillar 1.

**2. Proxy Variable Necessity and Risks**
Why a Proxy Variable is Necessary:
The e-commerce transaction dataset lacks explicit loan default labels. Traditional credit scoring uses historical repayment data, but here we only have purchase transaction patterns. We must infer credit risk from behavioral proxies.

Chosen Approach: We'll use RFM (Recency, Frequency, Monetary) analysis and clustering to identify customer segments. Customers with low engagement (infrequent, low-value transactions) will be labeled as high-risk proxies since disengaged customers typically represent higher credit risk.

## Potential Business Risks of Proxy-Based Predictions:

**Conceptual Mismatch Risk:** E-commerce engagement ≠ creditworthiness. Active shoppers may still default on loans.

**Sample Selection Bias:** Our training data may not represent the actual loan applicant population.

**Regulatory Compliance Risk:** Regulators may question the validity of using transaction patterns as a credit risk proxy.

**Fair Lending Risk:** If transaction patterns correlate with protected characteristics, the model could inadvertently create discriminatory outcomes.

**Performance Drift:** E-commerce behavior may change over time, requiring continuous monitoring and recalibration.

**Mitigation Strategies:**

Clearly document proxy variable methodology and assumptions

Implement ongoing model performance monitoring

Maintain human oversight for borderline cases

Regularly validate proxy correlation with actual defaults as data becomes available

**3. Model Selection Trade-offs in Regulated Finance**
The choice between simple interpretable models and complex high-performance models involves critical trade-offs:

Model Characteristic	Simple Model (Logistic Regression with WoE)	Complex Model (Gradient Boosting)	Regulatory Implication
Interpretability	High. Each feature's contribution is linear and easily explained.	Low. Non-linear interactions create "black box" behavior.	Regulators favor interpretable models for Pillar 2 validation.
Performance	Lower predictive accuracy, especially with complex patterns.	Higher accuracy through non-linear feature interactions.	Better risk discrimination improves capital efficiency under Pillar 1.
Regulatory Acceptance	Well-established, statistically transparent methodology.	May require extensive documentation and SHAP/LIME explanations.	Simpler models reduce approval timelines and compliance burden.
Implementation	Easy to deploy, monitor, and explain to stakeholders.	Requires specialized expertise for maintenance and explanation.	Affects operational risk management requirements.
Auditability	Complete audit trail of scoring decisions.	Difficult to trace specific decisions to input features.	Affects compliance with record-keeping regulations.
Our Strategic Approach:
Given Bati Bank's regulatory environment and the innovative nature of using alternative data, we recommend a hybrid approach:

**Initial Deployment**: Use Logistic Regression with Weight of Evidence (WoE) encoding for maximum transparency and regulatory acceptance.

**Validation Phase:** Simultaneously develop Gradient Boosting models for comparison and to establish performance benchmarks.

**Phased Implementation:** Begin with interpretable models while developing the governance framework for more complex models.

**Documentation Priority:** Regardless of model choice, maintain comprehensive documentation of data sources, transformations, modeling decisions, and validation results.

# Key Decision Factors for Bati Bank:

 * Regulatory constraints and supervisory expectations

* Availability of model risk management expertise

 * Business appetite for model innovation versus compliance certainty

* Strategic importance of the buy-now-pay-later initiative

Long-term plans for scaling alternative data applications

## Project Structure
text
credit-risk-model/
├── .github/workflows/ci.yml   # For CI/CD
├── data/                      # add this folder to .gitignore
│   ├── raw/                  # Raw data goes here 
│   └── processed/            # Processed data for training
├── notebooks/
│   └── eda.ipynb          # Exploratory, one-off analysis
├── src/
│   ├── __init__.py
│   ├── data_processing.py     # Script for feature engineering
│   ├── train.py               # Script for model training
│   ├── predict.py             # Script for inference
│   └── api/
│       ├── main.py            # FastAPI application
│       └── pydantic_models.py # Pydantic models for API
├── tests/
│   └── test_data_processing.py # Unit tests
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
├── .gitignore
└── README.md

## Setup Instructions
**Clone the repository**

 * Install dependencies: pip install -r requirements.txt

 * Download the dataset from Kaggle and place in data/raw/

 * Run EDA notebook: jupyter notebook notebooks/eda.ipynb

## Key Features
 * RFM-based proxy variable creation for credit risk

 * Weight of Evidence (WoE) and Information Value (IV)    transformations

 * Multiple model comparison with hyperparameter tuning

 * MLflow experiment tracking and model registry

 * FastAPI deployment with Docker containerization

 * CI/CD pipeline with automated testing

## Next Steps
 * Complete exploratory data analysis (Task 2)

 * Implement feature engineering pipeline (Task 3) 

 * Create RFM-based proxy target variable (Task 4)

 * Train and compare models (Task 5)

 * Deploy model as API with CI/CD (Task 6)