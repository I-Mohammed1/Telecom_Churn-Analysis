# Telecom_Churn- EDA, Model Building, Model Tuning


#### Intro
This project analyzes a telecom company’s dataset, with respect to customer churn.
The target variable is Churn Flag, True/False

#### Libraries
*Pandas
*Numpy, Matplotlib, Seaborn, Sklearn, MLextend(Scaling) LightGBM, Optuna

#### High-Level Description/How I went about the project
The data was in an excel sheet, I converted it to a CSV format to read it into the Jupiter Notebook.

After loading the data, I ran a few checks on the data and found that there were whitespaces in the observations and the column names of  the dataset.
I eliminated those using the strip command, stripping off the whitespaces before and after any column names.

One issue I wasn’t able to resolve was the presence of whitespaces in the observations where they were “True ” and “False ”. I ran the strip command which transformed those into “True” and “False” respectively, but when I ran the code to test presence of whitespaces, it still showed that whitespaces were present. However, as this was no longer affecting my work, I decided to move on with it.

#### EDA
I then proceeded with the usual EDA
As part of EDA, I first generated a Pandas Profiling report
I then proceeded to seperately plot a few graphs for Univariate and Bivariate Analysis of the numerical and categorical data.

#### Statistical Modeling
Here, I discuss the model evaluation criterion

#### Model evaluation criterion
Possible errors:
1. Model predicts that the customer will churn, but in reality, the customer stays: A False Positive.
2. Model predicts that the customer will not churn, but in reality, the customer leaves: A False Negative.

Which case is more important?
* For us, it is important to prevent the second error
* If a customer is incorrectly predicted to churn, the company might extend an offer to him/her although it may not have been necessary. This wouldn't put significant pressure on the resources, and hence impact is negligible.
* But if the opposite happens, an unsatisfied customer may be left unattended and will churn, and a valuable customer will have been lost

How to reduce False Negatives?
* Recall can be used a the metric for evaluation of the model, greater the Recall score, higher are the chances of minimizing False Negatives.

#### Data Preparation for Modeling
I proceeded to prepare the data for modeling
Here, I created another copy of the data,
Encoded the target variable (Churn Flag), and a couple of other variables into binary format.
I encoded the (“State”) variable using Label Encoding as it contains 52 unique values.

##### Dropping Variables
I then plot a heat map of correlation between the variables
Here, I found Total day, evening, night and international minutes to be having a corr coefficient of 1 with their charges counterparts. 
Here, I dropped the minutes columns and chose to keep the charges columns

##### Dividing the data into X and y
X contains all variables except the target variable, and y contains only the target variable

##### Scaling
I then observe that the data in columns was on different scales, so I
scaled the data using RobsutScaler

##### Train_test split
Next, I split the data into train and test sets, with test size 30%

#### Model

Now that our data is ready, I define a few functions to evaluate the performances of the models, and a scorecard that presents the Train and Test accuracies, Recall, and F1- Weighted average scores,
And define a function to plot a confusion matrix

Finally, I start building the models, and tuning a few of them, as shown in the scorecard below:

<img width="728" alt="image" src="https://user-images.githubusercontent.com/103328085/168894001-d931e55c-ff46-4b36-a386-0b804faaae4e.png">

Of the above models built and tuned, Tuned Light Gradient Boosting Model gives the best Train and closest Test Recall scores, with the highest F1 score

##### Feature Importances
I plot a figure showing the relative importances of features with respect to the target variable

#### Business Insights
- The average account length is 100 days, which is just 37% of the 9-month period of the dataset
- Customers that made 4 or more calls to customer service were much likely to churn than those who made 3 calls or less.
- The most calls made to customer care by a customer was 9, and such customers had a 100% churn rate.
- The churn rate is significant among customers with account lengths falling between 50 and 150 days, and peaks between 100 and 120.
 - This means that customers are likely to switch between 2 months of usage and 5 months
 - This could be because the first set of customers were unsatisfied after one month of the service, and just waited to leave before their next billing cycle.
 - Highest churn is in customers of between 3 and 4 months. This needs to be investigated, as to what factors are causing this.
- Total charge:
  - The churn rate is significant among customers that spent between \\$45 and \\$60, and between \\$70 and \\$80, after which it declines.
 - The churn rate is highest among customers spending around \\$73.
  - This insight needs to be investigated further, it could be that these customers are holding a particular plan which costs around $70,  and this particular plan might be causing some issues that most unsatisfied customers are facing.

#### Business Recommendations
- Customers making 3 calls or more to Customer Service should be flagged as important and these cases should be tracked for immediate resolution of their issues.
- As customers are most likely to switch between 2-5 months of usage, this signifies that the first 5 months is the important stage where the brand loyalty needs to be established
- Highest churn rate is found in customers of between 3 and 4 months. This needs to be investigated, as to what factors are causing this.
- The churn rate is highest among customers spending around \\$73.
- This insight needs to be investigated further, as it could be that these customers are holding a particular plan which costs \\$73,  and this particular plan might be having some issues that most unsatisfied customers are facing.
- A system needs to be brought in place to record the customer satisfaction after each call made to customer care. - This will not only help improve resolution efficacy, but also help better predict churn probability of any account
