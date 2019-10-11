---
layout: page
title: Loan Status Prediction
---


### Purpose

Predict loan status if it is fully paid or charged off(amount of credit that is unlikely to be collected) using a bank loan dataset. And what I mean by charged off status is the amount of credit that is unlikely to be collected.

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

### Data Cleaning

Firstly I started by cleaning data by removing null rows and replacing null numerical cells with the mean and null categorical cells with mode.
Secondly I dealt with the columns that have lots of categories by grouping them. So for example Purpose data field had these categories:

<ul>
  <li>Debt Consolidation      78552</li>
<li>other                    6037</li>
<li>Home Improvements        5839</li>
<li>Other                    3250</li>
<li>Business Loan            1569</li>
<li>Buy a Car                1265</li>
<li>Medical Bills            1127</li>
<li>Buy House                 678</li>
<li>Take a Trip               573</li>
<li>Major_purchase            352</li>
<li>Small_business            283</li>
<li>Moving                    150</li>
<li>Wedding                   115</li>
<li>Vacation                  101</li>
<li>Educational Expenses       99</li>
<li>Renewable_energy           10</li>
</ul>

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



### Baseline Models
After cleaning data I tried building several models with 3-cross validation folds  to find the best model that fits my data.
K-Nearest Neighbor Result:<br/>
Accuracy:          0.7359100631746506<br/>
Precision:          0.32466918714555765<br/>
Recall:               0.15042697613312897<br/>

Decision Tree Result:<br/>
fit_time:              0.529221<br/>
score_time:        0.063719<br/>
test_accuracy:   0.708044<br/>
train_accuracy:  1.000000<br/>
test_precision:   0.802186<br/>
train_precision:  1.000000<br/>
test_recall:          0.792122<br/>
train_recall:        1.000000<br/>
test_f1:              0.797120<br/>
train_f1:             1.000000<br/>

Random Forest Result:<br/>
fit_time:             0.848813<br/>
score_time:       0.171709<br/>
test_accuracy:  0.759097<br/>
train_accuracy: 0.992004<br/>
test_precision:   0.805275<br/>
train_precision:  0.992866<br/>
test_recall:        0.880124<br/>
train_recall:        0.996116<br/>

Logistic Regression Result:<br/>
fit_time:              0.361881<br/>
score_time:        0.022789<br/>
test_accuracy:   0.775652<br/>
train_accuracy:  0.775408<br/>
test_precision:   0.765078<br/>
train_precision:  0.764909<br/>
test_recall:         0.996021<br/>
train_recall:        0.995937<br/>

Naive Bayes Classifier Result: <br/>
fit_time:              0.033692<br/>
score_time:        0.042347<br/>
test_accuracy:    0.401805<br/>
train_accuracy:   0.402171<br/>
test_precision:    0.963284<br/>
train_precision:   0.963789<br/>
test_recall:          0.180804<br/>
train_recall:         0.181183<br/>

After trying all of these models I wasn't satisfied enough with the results so I decided to do some feature engineering!

### Feature Engineering 
For The feature engineering part I created dummy variables for the categorical fields. And since the target classes weren't balanced(72% of the fully paid class and 28% of the charged off class)  I decided to oversample the charged-off class using SMOTE function.
Before balancing Loan Status Class:<br/>
![before]({{ site.url }}/images/loan_imbalanced_classes.png)

After balancing the classes:
![After]({{ site.url }}/images/loan_balanced_classes.png)

### Final Model
After doing the feature engineering part I decided to try pipelining my data to get the best model that fits my data with the right hyperparameters and that was the result.<br/>
![pipeline]({{ site.url }}/images/loan_pipeline.png)
So I fitted my data into Random Forest Classifier and the result was amazing!<br/>
Accuracy:  0.7952439024390244<br/>
Precision:  0.7884382973009265<br/>
Recall:  0.9826778242677824<br/>
f1:  0.8749068693190283<br/>

Since the result satisfies me enough I tested the model and compared the model result along with the actual data(1=Fully Paid Loan, 2=Charged-off Loan).<br/>
![random_forest]({{ site.url }}/images/actual_predicted_loan.png)

And bar plot is comparing the result of the confusion matrix:<br/>
![cm]({{ site.url }}/images/cm_before_threshhold.png)<br/>
As you can see the True Negative value is to low comparing it to the True Positive value, and thats why I build a function that finds the best threshold value.
![cm]({{ site.url }}/images/cm_after_threshhold.png)<br/>

### Business Insight
Since my data didn't help me finding the average profit for each loan. I did my research to find the average and plotted the optimized threshold along with the profit  and the result was reasonable.
![profit]({{ site.url }}/images/loan_profit.png)<br/>

Have questions or suggestions? Feel free to [email me](mailto:njoud.algifari@gmail.com).

Thanks for reading!
