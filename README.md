# Loan_default_prediction_with_NLP_technique

In this analysis, we predict the loan application default probability based on numerical information such as income, etc., and the loan application description (text data). 

1. First we conduct some EDA and simple ML model analysis. 

![image](https://github.com/tsenguun0106/Loan_default_prediction_with_NLP_technique/assets/60633314/14598488-f545-4ca3-9da9-cfb51a89b3c3)
When the loan was not fully paid or defaulted, the target variable is set as 1. And when the loan was fully paid out, the target variable value is set as 0. 

![image](https://github.com/tsenguun0106/Loan_default_prediction_with_NLP_technique/assets/60633314/033f8105-7f4d-4287-bc39-88ef21dc5f0e)

Numerical variables: 
- Loan amount
- Term (loan term/duration)
- interest rate
- Length of employment of borrower
- Annual income
- Income source verification status

![image](https://github.com/tsenguun0106/Loan_default_prediction_with_NLP_technique/assets/60633314/46355cfa-351d-4c6e-84d0-8d54ac11f8e7)

Employment length and loan term values are transformed into dummy variables to capture more complex impacts from these factors on the loan default problem. 


2. NLP modeling using the pre-trained embedding vectors from the open-source.


   
