# Loan_default_prediction_with_NLP_technique

In this analysis, we predict the loan application default probability based on numerical information such as income, etc., and the loan application description (text data). 

**Problem:** Lending companies need to decide whether to grant the loan to a borrower using the borrower's numerical data such as income, employment length, age, etc., and the borrower's loan application description (text data). 

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

**Feature importance result:**
1. Both the RF and XGboost models capture that the interest rate, annual income, and loan length are important factors for predicting the loan default rate.
2. XGboost also indicates that the employment length of a borrower can be informative. However, the RF model does not suggest the same.
3. Also, both models explain that the loan amount is not very informative about the loan default rate which is quite different from the expectation.
4. The SHAP method demonstrates a similar feature importance result. However, the SHAP method is pushing that the loan amount is very informative about the loan default rate, which is quite a different result from the previous two models. 


Annual income and loan amount relationship for 60 months term loans (x-axis is the annual income and y-axis is the loan amount): 

<img src="https://github.com/tsenguun0106/Loan_default_prediction_with_NLP_technique/assets/60633314/462c981a-cab3-40d9-adad-338bc3abf756" width="400px">

Annual income and loan amount relationship for 36 months term loans (x-axis is the annual income and y-axis is the loan amount): 

<img src="https://github.com/tsenguun0106/Loan_default_prediction_with_NLP_technique/assets/60633314/2f833a9f-11e7-4e75-a9fa-08e5046a8c3f" width="400px">

The above two graphs illustrate that the maximum loan amount and the annual income level have a linear upward relationship for the annual income values up to 70K USD. In other words, borrowers with up to 70K USD annual income were able to borrow up to around half of their annual earnings. 



# NLP modeling using the pre-trained embedding vectors.
(Notebook used for this analysis: Loan_app_NLP_PyTorch_RNN_pretrained_embeddings_with_other_features_ver3.ipynb)

## Conducting the text data cleaning: 

<img src="https://github.com/tsenguun0106/Loan_default_prediction_with_NLP_technique/assets/60633314/0647e1c7-7f08-43b0-8bb1-fb00ded45a16" width="350px">

1. Sorting the words using their frequencies
2. Adding padding and unknown to the tokens list
3. Creating word-to-index and index-to-word mapping dictionaries

<img src="https://github.com/tsenguun0106/Loan_default_prediction_with_NLP_technique/assets/60633314/4060cdf2-b9fa-4430-b73a-7c3ae4c56f0a" width="350px">

## Using the pre-trained embedding vectors for words from the GLOVE oper-source NLP model: 

<img src="https://github.com/tsenguun0106/Loan_default_prediction_with_NLP_technique/assets/60633314/ae9b8fbb-0e51-4323-923a-a111aad828d3" width="350px">

I used the PyTorch to conduct the NLP model training: 

<img src="https://github.com/tsenguun0106/Loan_default_prediction_with_NLP_technique/assets/60633314/c7b04adc-496c-4ab5-9453-52da966601f8" width="350px">

I use the numerical features and the text feature to train the model:  
The list of numerical features: 

<img src="https://github.com/tsenguun0106/Loan_default_prediction_with_NLP_technique/assets/60633314/6bbd984f-4531-4dac-b302-533f840ffc88" width="300px">

The example for the text loan request description from one borrower: 

<img src="https://github.com/tsenguun0106/Loan_default_prediction_with_NLP_technique/assets/60633314/c53b16de-08f0-4e63-b142-31b0df3e93aa" width="650px">

**Model architecture:** 
1. 32 hidden units and 2 hidden layers for the GRU model (RNN)
2. Initial embedding vectors for words are extracted from the GLOVE open-source NLP model and the embedding vector dimension is 100 (for each word in vocabulary).
3. The dropout probability for the GRU model is 0.2.
4. Text data is trained through the GRU model and the GRU model output is combined by the linear layer at the end. 
5. Numerical features are trained through the logistic regression model.
6. The Sigmoid function is applied after concatenating the outputs from the GRU model for text data and the logistic regression model for the numerical data.
7. This sigmoid function will predict the final output regarding the loan defaulting or not.
8. Learning parameters are the GRU model parameters for text data, logistic regression parameters for numerical data, and parameters for the final sigmoid layer to efficiently combine the GRU and logistic regression models for the final prediction process. 

<img src="https://github.com/tsenguun0106/Loan_default_prediction_with_NLP_technique/assets/60633314/f8f57d01-67a1-40a2-9c3f-1cd761888623" width="650px">

Model architecture displayed: 

<img src="https://github.com/tsenguun0106/Loan_default_prediction_with_NLP_technique/assets/60633314/2fa9b04e-bee7-4513-9c75-c67ff30380ad" width="350px">

**Model training process:**
1. Batch size is 32.
2. 15% of data is used for the validation.
3. Adam optimizer is used and the model is trained for 10 epochs.
4. The Binary Cross Entropy function is used as the loss function.

# Summary: 
The model accuracy based on the validation data is 82.24%. The sample size is only 28124. The model still can learn some insights from the numerical features and text data. However, my conclusion is that more data is needed to train the deep learning model for this loan defaulting prediction problem. In this demo, I demonstrated how numerical features such as income and age data can be combined with text data for predicting the loan default probability of a borrower. This use case is especially useful for lending companies to automate their loan decision-making process. 
