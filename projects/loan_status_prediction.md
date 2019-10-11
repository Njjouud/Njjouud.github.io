---
layout: page
title: Loan Status Prediction
---


### Purpose

Predict loan status if it is fully paid or charged off using a bank loan dataset. And what I mean by charged off status is the amount of credit that is unlikely to be collected.

### Dataset Description
##### Dataset Source
[Kaggle](https://www.kaggle.com/omkar5/dataset-for-bank-loan-prediction/)

##### Dataset Dimensions
(19x101k).

##### Features
<ul>
  <li>Numeric Features</li>
  <ul>
  <li>Credit Score(risk a lender takes when you borrow money).</li>
  <li>Annual Income.</li>
  <li>Current Loan Amount.</li>
  <li>Monthly Debt.</li>
  <li>Years of Credit History.</li>
  <li>Number of Open Accounts</li>
  <li>Number of Credit Problems.</li>
  <li>Current Credit Balance.</li>
  <li>Maximum Open Credit and Tax Liens.</li>
<li>Months since last delinquent.</li>
  <li>Bankruptcies</li>
  </ul>
  <li>Categorical Features</li>
<ul>
  <li>Loan Status.</li>
  <li>Term.</li>
  <li>Home Ownership.</li>
  <li>Purpose.</li>
  </ul>
</ul> 

### Work Stages

##### Data Cleaning

I started cleaning data by:

- Dropping null observations.
- Replacing null numerical cells with the mean.  
- Null categorical cells with mode.
- Grouped the columns that have lots of categories by grouping them. For example, Purpose data field had these categories and number of datapoints:
  * Debt Consolidation 78552 
  * other 6037
  * Home improvments 5839
  * Other 3250
  * Business Loan 1569
  * Buy a Car 1265
  * Medical Bills 1127
  * Buy House 678
  * Take a Trip 573
  * Major_purchase 352
  * Small_business 283
  * Moving 150
  * Wedding  115
  * Vacation 101
  * Educational Expenses  99
  * Renewable_energy 10

I categorized them into 6 different categories:
<ul>
  <li>Other:</li>
<ul>
  <li>other            </li>      
  <li>Other            </li>       
  <li>Major_purchase   </li>       
  <li>Renewable_energy  </li>
  </ul>   
  <li>Home:</li>
<ul>
  <li>Home Improvements  </li>    
  <li>Buy House   </li>
  </ul>
  <li>Essentials: </li>
<ul>
  <li>Buy a Car       </li>         
  <li>Medical Bills    </li>       
  <li>Educational Expenses </li>      
  </ul>
  <li>Leisure:</li>
<ul>
  <li>Wedding    </li>               
  <li>Take a Trip  </li>            
  <li>Vacation    </li>              
  <li>Moving      </li>             
  </ul>
  <li>Business:</li>
<ul>
  <li>Small_business  </li>          
  <li>Business Loan </li>           
  </ul>
  <li>Debt Consolidation  </li>
</ul> 
Thirdly, I converted categorical field to 1,0 columns.
Lastly, I removed duplicates. 



##### Baseline Models
After cleaning data I tried building several models with 3-cross validation folds to find the best model that fits my data.
K-Nearest Neighbor Result:<br/>
Accuracy:          0.7359<br/>
Precision:          0.3246<br/>
Recall:               0.1504<br/>

Decision Tree Result:<br/>
fit_time:              0.5292<br/>
score_time:        0.0637<br/>
test_accuracy:   0.7080<br/>
train_accuracy:  1.0000<br/>
test_precision:   0.8021<br/>
train_precision:  1.0000<br/>
test_recall:          0.7921<br/>
train_recall:        1.0000<br/>
test_f1:              0.7971<br/>
train_f1:             1.0000<br/>

Random Forest Result:<br/>
fit_time:             0.8488<br/>
score_time:       0.1717<br/>
test_accuracy:  0.7590<br/>
train_accuracy: 0.9920<br/>
test_precision:   0.8052<br/>
train_precision:  0.9928<br/>
test_recall:        0.8801<br/>
train_recall:        0.9961<br/>

Logistic Regression Result:<br/>
fit_time:              0.3618<br/>
score_time:        0.0227<br/>
test_accuracy:   0.7756<br/>
train_accuracy:  0.7754<br/>
test_precision:   0.7650<br/>
train_precision:  0.7649<br/>
test_recall:         0.9960<br/>
train_recall:        0.9959<br/>

Naive Bayes Classifier Result: <br/>
fit_time:              0.0336<br/>
score_time:        0.0423<br/>
test_accuracy:    0.4018<br/>
train_accuracy:   0.4021<br/>
test_precision:    0.9632<br/>
train_precision:   0.9637<br/>
test_recall:          0.1808<br/>
train_recall:         0.1811<br/>

After trying all of these models I wasn't satisfied enough with the results so I decided to do some feature engineering!

##### Feature Engineering 
For The feature engineering part I created dummy variables for the categorical fields. And since the target classes weren't balanced(72% of the fully paid class and 28% of the charged off class)  I decided to oversample the charged-off class using SMOTE function.
Before balancing Loan Status Class:<br/>
![before]({{ site.url }}/images/loan_imbalanced_classes.png)

After balancing the classes:
![After]({{ site.url }}/images/loan_balanced_classes.png)

##### Final Model
After doing the feature engineering part I decided to try pipelining my data to get the best model that fits my data with the right hyperparameters and that was the result.<br/>
![pipeline]({{ site.url }}/images/loan_pipeline.png)
So I fitted my data into Random Forest Classifier and the result was amazing!<br/>
Accuracy:  0.7952<br/>
Precision:  0.7884<br/>
Recall:  0.9826<br/>
f1:  0.8749<br/>

Since the results satisfy me enough I tested the model and compared the model result along with the actual data(1=Fully Paid Loan, 2=Charged-off Loan).<br/>
![random_forest]({{ site.url }}/images/actual_predicted_loan.png)

And bar plot is comparing the result of the confusion matrix:<br/>
![cm]({{ site.url }}/images/loan_cm_before_threshhold.png)<br/>
As you can see the True Negative value is to low comparing it to the True Positive value, and thats why I build a function that finds the best threshold value.
![cm]({{ site.url }}/images/loan_cm_after_threshhold.png)<br/>

### Business Insight
Since my data didn't help me finding the average profit for each loan. I did my research to find the average and plotted the optimized threshold along with the profit  and the result was reasonable.
![profit]({{ site.url }}/images/loan_profit.png)<br/>

Have questions or suggestions? Feel free to [email me](mailto:njoud.algifari@gmail.com).

Thanks for reading!
