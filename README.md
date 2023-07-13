# Marketing-Campaign-Analysis

Analysis and Prediction of Marketing Campaign Effectiveness.

The data in this project contains information on a telemarketing campaign by a Portuguese banking institution.

The dataset used is bank-full.csv (sourced from https://archive.ics.uci.edu/dataset/222/bank+marketing).

The dataset has 45,211 observations and 17 variables.

The dataset contains info about various client attributes like "Age of customer", "Type of Job of customer", "Marital status of the customer", "Education level of the customer", and "If the customer has credit in default?", "Balance of the customer", "If the customer has a housing loan?", "If the customer has a personal loan?"

The campaign attributes consist of data that contains info like "contact communication type", "last contact day of the week", "last contact month of the year", "last contact duration, in seconds", "number of contacts performed during this campaign and for this client", "number of days that passed by after the client was last contacted from a previous campaign", "number of contacts performed before this campaign and for this client", "the outcome of the previous marketing campaign".

The outcome variable would be "Y" meaning "Has the client subscribed to a term deposit?" and the variable type is Categorical (Yes / No)

Initial Analysis

Most of the variables are categorical variables, so they were converted into factors using as.factor().

29% of the data for the Contact variable falls under ‘unknown’ category.

Most of the data for poutcome variable falls under ‘unknown’ category.

The "balance" variable contains negative values and most of the clients have a balance of less than 12500.

Between all numeric variables, only "pdays" and previous variables have some level of relationship but not so strong to exclude anyone of these variables

Partitioned the data into Training data (60% - 27,127 rows) and Validation data (40% - 18,084 rows)

Initial Observations

Most of the clients Below the age of 25 years and over the age of 60 years tend to accept Term Deposit offers.

The duration of the call seems to highly influence the outcome variable. Longer duration call result in successful subscription of Term deposit. So it is not a good variable to be included in the Model.

The variable "outcome" seems to have a good influence on the outcome variable. If the client subscribed to the bank’s product in the last campaign, there is high chance they will subscribe to the Term Deposit.

Clients that have credit in default do not tend to choose the Term Deposit.


Final Analysis and Results

-> kNN:

    Excluded contact (due to large values being ‘Unknown’), day (Due to no influence on the Outcome variable), and duration (as duration will not be known for any new call) variables.
    Identified k=13 as the best k based on accuracy (89.19%). 
    With K=13, Accuracy = 89.19%, Sensitivity = 98.73%, Specificity = 16.33% was achieved
-> Classification Tree:

    Identified the best CP value (0.0018) and developed pruned tree based on that.
    Achieved 89.48% accuracy with 98.89% sensitivity and 17.57% specificity with the best-pruned tree.
    To further increase the accuracy, we applied the Random Forest technique and identified important variables to predict the outcome.
    Achieved 89.39% accuracy with 98.15% sensitivity and 22.49% specificity with the random forest.
->  Logistic Regression:

    Employed logistic regression model and achieved 89.36% accuracy with 98.71% sensitivity and 17.96% specificity.

Comparison of the 3 models

   -> KNN
   
     From 1-14, k= 13 gave us the best accuracy when running k-NN at 89.18%, and the lowest accuracy was 83.55% at k= 1. Very close in accuracy to our pruned tree but still less.
   -> Classification Tree- 
    
    Having higher values of accuracy than k-NN and Logit, our best pruned tree seems to be the best method in predicting whether a customer will subscribe to a bank’s Term deposit. 
    "poutcome", "housing", "pdays", "month", "age" and "balance" are the predictors used in our classification tree. 
    Even with a lower accuracy given by random forest, it is still a higher accuracy than k-NN and Logit.
   -> Logistic Regression- 
   
       When running Logit, the Decile Chart bars did have a consistent decline but with a slight increase of 0.1 at the 80th percentile.

Accuracy for both Logit and k-NN were very close to our pruned tree but still less; specificity for all 3 methods were relatively the same, with only a difference in range of about 2%
                    
Final Takeaways

-> The classification tree method provided the best accuracy among kNN, Classification Tree and Logistic regression.

-> Month, Age, Housing and pOutcome variables has most influence in determining the outcome variable.

-> March month being the financial year-end turned out to be the best time to conduct Marketing campaign.

-> Clients with the last successful campaign, having housing loans contacted outside the months of (Apr, Jan, May, and Nov) and last contacted more than 84 days ago, are a good targeted audience for Term Deposit.



