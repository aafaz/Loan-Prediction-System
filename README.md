# Loan-Prediction-System
![](Images/document-classifier-photo.png)


# Problem Statement:
Loans are the core business of banks. The main profit comes directly from the loan’s interest. The loan companies grant a loan after an intensive process of verification and validation. However, they still do not have assurance if the applicant is able to repay the loan with no difficulties.
The two most critical questions in the lending industry are: 
1) How risky is the borrower? 
2) Given the borrower’s risk, should we lend him/her?
In the modern era, the data science teams in the banks build predictive models using machine learning to predict how likely a client is going to default the loan when they only have a handful of information.
Loan Prediction is a very common real-life problem that each retail bank faces at least once in its lifetime. If done correctly, it can save a lot of man hours at the end of a retail bank.

# Goal of this Project:
Dream Housing Finance company deals in all home loans. They have presence across all urban, semi urban, and rural areas. Customer first apply for home loan after that company validates the customer eligibility for loan. Company wants to automate the loan eligibility process (real time) based on customer detail provided while filling online application form. 

To automate this process, they have given a problem to identify the customers’ segments, those are eligible for loan amount so that they can specifically target these customers. The goal of this project is to predict whether a loan would be approved or not.

# Hypothesis Generation:
Below are the factors which I think can affect the Loan Approval (dependent variable for this loan prediction problem):
•	Salary: Applicant with high income should have more chances of loan approval.
•	Previous History: Applicant who have repaid their previous debts should have higher chances of loan approval.
•	Loan Amount: Loan Approval should also depend on the loan amount. If the loan amount is less, chances of loan approval should be high.
•	Loan Term: Loan for less time and less amount should have higher chances of approval.
•	EMI: Lesser the amount to be paid monthly to repay the loan, higher the chances of loan approval.

# Data Source:
For this problem, we have two CSV files: train and test.
Train file will be used for training the model, i.e., our model will learn from this file. It contains all the independent variables and the target variable.
Test file contains all the independent variables, but not the target variable. We will apply the model to predict the target variable for the test data.
Given below is the description for each variable with its data type.

![](Images/document-classifier-photo.png)
We have 614 rows and 13 columns in the train dataset and 367 rows and 12 columns in the test dataset.
