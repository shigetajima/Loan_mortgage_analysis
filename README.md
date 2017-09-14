# Loan mortgage analysis
As my Capstone project I worked with a mortgage lender to analyze their mortgage data.
Analysis includes the prediction of loan processing time.
Regression models are used to predict the # of days it takes
from the mortgage rate "locked" until the money gets "funded"
(it's called "Locked to Funded" time).
Classification models are used to predict the Locked to Funded "period"
after the data were divided into several bins (Lock periods).
Top features were found and interpretations were made.

## Presentation slides
* My presentation slides are posted on this repo (Mortgage_Analysis_slides_Shige_Tajima.pdf). These slides were presented at the Capstone showcase event at Galvanize on Sep 7, 2017. Please note that I cannot share the code and data for this project since the data is from a real company.

## Packages used
The packages used in my python code (not posted on github) include:
* sklearn
* statsmodels
* psycopg2
* pandas
* numpy
* matplotlib

## Data Cleaning and Preprocessing
Data has 500 features and about 200 of them are categorical ones. To preprocess data, the following steps are performed.

* In order to extract "locked to funded" data, checked the stage name to see if it is equal to closed and won. If not, discard such rows from data.
* columns with too many missing values (>95%) are removed.
* The remaining "missing" values were replaced with 0.
* There are features in the data which cause "leakage" that will result in high accuracy value or high R2 score. Such features were identified and removed from the data.
* dummify the categorical features.
* If two columns are identical, remove one of them.

## Add Features
Even though there exist many features in the data, an important part of the analysis is to find new features. They are calculated using the values from the other features. The following features are added to Pandas data frame:
  * cohort value
  * the number of staff
  * The number of active Loans
  * loan weight
  * locked to funded "period"

See the presentation slides for details about those features.

## The code structure
1. Data are cleaned and preprocessed (see above)
2. New features are calculated and added (see above)
3. Linear regression
  * reduce the number of features (by checking the correlation with locked_to_funded, VIF, and p_value)
  * cross validation of R2 score
4. Run Lasso regression to identify the main features.
5. Run other regression models (Random Forest, AdaBoost, GDB)
6. Run classification model (Random forest)
  * select top 50 features
  * grid search for optimizing parameters
  * cross validation of scores
