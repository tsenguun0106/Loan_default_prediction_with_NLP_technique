# Loan_default_prediction_with_NLP_technique

In this analysis, we predict the loan application default probability based on numerical information such as income, etc., and the loan application description (text data). 

## First we conduct some EDA and simple ML model analysis. 

(Notebook used for this analysis: Loan_application_data_analysis_Dec_9.ipynb)

<img src="https://github.com/tsenguun0106/Loan_default_prediction_with_NLP_technique/assets/60633314/14598488-f545-4ca3-9da9-cfb51a89b3c3" width="600px">

When the loan was not fully paid or defaulted, the target variable is set as 1. And when the loan was fully paid out, the target variable value is set as 0. 

<img src="https://github.com/tsenguun0106/Loan_default_prediction_with_NLP_technique/assets/60633314/033f8105-7f4d-4287-bc39-88ef21dc5f0e" width="350px">

Numerical variables: 
- Loan amount
- Term (loan term/duration)
- interest rate
- Length of employment of borrower
- Annual income
- Income source verification status

<img src="https://github.com/tsenguun0106/Loan_default_prediction_with_NLP_technique/assets/60633314/46355cfa-351d-4c6e-84d0-8d54ac11f8e7" width="400px">

Employment length and loan term values are transformed into dummy variables to capture more complex impacts from these factors on the loan default problem. 

I have fit the random forest model with 200 trees for this loan default classification problem. 
Feature importance from Random Forest model: 

<img src="https://github.com/tsenguun0106/Loan_default_prediction_with_NLP_technique/assets/60633314/f8875bd2-9517-41c5-a492-9d233ea4e6e1" width="350px">

Also, I have fit the XGBoost model with 150 trees for this problem. 
Feature importance from XGBoost model: 

<img src="https://github.com/tsenguun0106/Loan_default_prediction_with_NLP_technique/assets/60633314/4969872e-29b4-4b07-95fc-ea2b3c2ee53b" width="350px">

Finally, I have run the logistic regression for this problem and used the SHAP library to get the SHAP feature importance values.

<img src="https://github.com/tsenguun0106/Loan_default_prediction_with_NLP_technique/assets/60633314/3dde5c3d-7fda-40e5-b052-155b458891c3" width="450px">

Annual income and loan amount relationship for 60 months term loans: 

<img src="https://github.com/tsenguun0106/Loan_default_prediction_with_NLP_technique/assets/60633314/462c981a-cab3-40d9-adad-338bc3abf756" width="400px">

Annual income and loan amount relationship for 36 months term loans: 

<img src="https://github.com/tsenguun0106/Loan_default_prediction_with_NLP_technique/assets/60633314/2f833a9f-11e7-4e75-a9fa-08e5046a8c3f" width="400px">





## NLP modeling using the pre-trained embedding vectors from the open-source.




   
