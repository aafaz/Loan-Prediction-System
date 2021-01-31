# Loan Prediction System for Banks
![](Images/1.%20Loan%20Prediction%20System.png)


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

![](Images/2.%20Data%20Dictionary.png)

We have 614 rows and 13 columns in the train dataset and 367 rows and 12 columns in the test dataset.


# Exploratory Data Analysis:
The exploratory data analysis is divided into two categories:

# 1.	Univariate Analysis: 
Examining each variable individually. 
For categorical features, we use frequency table or bar plots which will calculate the number of each category in a particular variable.

![](Images/3.%20Univariate%20Analysis_1.png)

It can be inferred from the above bar plots that:
•	80% applicant in the dataset are male.
•	Around 65% of the applicants in the dataset are married.
•	Around 15% of the applicants in the dataset are self-employed.
•	Around 85% applicants have repaid their debts.

![](Images/4.%20Univariate%20Analysis_2.png)

Following inferences can be made from the above bar plots:
•	Most of the applicant do not have any dependents.
•	Around 80% of the applicants are graduates.
•	Most of the applicant are from Semiurban area.

For numerical variables, probability density plots can be used to look at the distribution of the variable.

![](Images/5.%20Univariate%20Analysis_3.png)

It can be inferred that most of the data in the distribution of applicant income is towards left which is not normally distributed, and the boxplot confirms the presence of a lot of extreme values/outliers. This can be attributed to the income disparity in the society. 


# 2.	Bivariate Analysis: 
Examining each variable with respect to target variable

![](Images/6.%20Bivariate%20Analysis.jpg)

Following inferences can be made from the above bar plots:
•	It seems people with credit history as 1 are more likely to get the loans approved.
•	Proportion of loans getting approved in semi-urban area is higher than as compared to that in rural and urban areas.
•	Proportion of married applicants is higher for the approved loans.
•	Ratio of male and female applicants is more or less same for both approved and unapproved loans.

# 3.	Correlation Plot:
The following heatmap shows the correlation between all the numerical variables. The variable with darker color means their correlation is more.

![](Images/7.%20Correlation%20Plot.png)

We see that the most correlated variables are (Applicant Income – Loan Amount) and (Credit_History – Loan Status). 
LoanAmount is also correlated with CoapplicantIncome.


# Data Preprocessing:
The quality of the inputs in the model will decide the quality of your output. The following steps were taken to pre-process the data to feed into the prediction model.

1.	Missing Value Imputation

After understanding all the variable in the data, we can now impute the missing values and treat the outliers because missing data and outliers can have adverse effect on the model performance. 

We consider the following values in all the features one by one.

For categorical variables: impute using mode.

For numerical variable: imputation using mean or median. Here, I have used median to impute the missing values as evident from Exploratory Data Analysis that loan amount has outliers, so the mean will not be the proper approach as it is highly affected by the presence of outliers.

2.	Outlier Treatment:

As LoanAmount contains outliers, it is rightly skewed. One way to remove this skewness is by doing the log transformation. As a result, we get a distribution like the normal distribution and does no affect the smaller values much but reduces the larger values.

![](Images/8.%20Outlier%20Treatment.png)

Now the distribution for LoanAmount looks much closer to normal and effect of extreme values has been significantly subsided. 

# Building the Baseline Model:
For the baseline model, I have chosen a simple logistic regression model to predict the loan status. The training data is divided into training and validation set. In this way we can validate our predictions as we have the true predictions for the validation part.
The baseline logistic regression model has given an accuracy of 84%. From the classification report, the F-1 score obtained is 82%.

# Feature Engineering:
Based on the domain knowledge, we can come up with new features that might affect the target variable. We can come up with following new three features:

1.	Total Income: 
As evident from Exploratory Data Analysis, we will combine the Applicant Income and Coapplicant Income. If the total income is high, chances of loan approval might also be high.

2.	EMI:
EMI is the monthly amount to be paid by the applicant to repay the loan. Idea behind making this variable is that people who have high EMI’s might find it difficult to pay back the loan. We can calculate EMI by taking the ratio of loan amount with respect to loan amount term.

3.	Balance Income: 
This is the income left after the EMI has been paid. Idea behind creating this variable is that if the value is high, the chances are high that a person will repay the loan and hence increasing the chances of loan approval. 

Let us now drop the columns which we used to create these new features. Reason for doing this is, the correlation between those old features and these new features will be very high and logistic regression assumes that the variables are not highly correlated. We also want to remove the noise from the dataset, so removing correlated features will help in reducing the noise too.

# Model Building:
StratifiedShuffleSplit is used as a cross validation technique in this problem. 

The advantage of using this cross-validation technique is that it is a merge of StratifiedKFold and ShuffleSplit, which returns stratified randomized folds. The folds are made by preserving the percentage of samples for each class.

After creating new features, we can continue the model building process. So, we will start with logistic regression model and then move over to more complex models like Decision Tree, Random Forest and XGBoost.
The model building code can be found here: <a> https://github.com/aafaz/Loan-Prediction-System/blob/master/Code/Exploratory%20Data%20Analysis.ipynb </a>

# Model Comparision:
![](Images/9.%20Model%20Comparision.png)


After trying and testing 4 different algorithms, the best predictions are given by Logistic Regression Model, with an F-1 Score of 82%.

The following actions were taken to achieve this result:

•	Explored the dataset to understand the data.

•	Perform different tests of statistical significance to uncover hidden data relationships that our predictive model could learn from and leverage when predicting unseen instances.

•	Employed statistical analysis using various python libraries to identify the number and names of features that could more likely help in identifying the potential customers.


# Future Improvements:
•	In upcoming years, as the new data keeps coming in, it will be important for data science team to deal with missing values, imbalanced data sets and additional features. 

•	It is important to notice this fact that the default loans are only about 10% of the total loans, thus during the training process, the model will favor predicting more negatives than positive results.

•	The models can also be improved further by fine tunings on hyperparameters or using ensemble methods such as bagging, boosting, and stacking.
