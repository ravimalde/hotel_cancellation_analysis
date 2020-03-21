# Hotel Cancellation Analysis

This project was a collaborative effort between Ravi Malde and Seung Won Lee.

# Executive Summary

A large hotel chain has approached us to investigate viable methods of mitigating the impact of short-notice customer cancellations. The aim of this analysis was to identify which characteristics of customers indicate that they are of a high probability to cancel, and to provide actionable insights on how to mitigate any revenue loss due to cancellations.

We take ethics very seriously so for obvious reasons race, religion, gender and biological sex have not been considered. All customers pay the same overall price (if they are purchasing the same product), it is only the initial deposit (as a % of the total price) that will change on a customer to customer basis. It is important to note that despite our model not considering these characteritics directly, it must be monitored post implementation to determine whether or not it is discriminating against any goups indirectly throught the variables that have been considered.

## The Problem

Our dataset contained 79,330 bookings made between 1st July 2015 and 31st August 2017. Of these, 33,076 were cancelled prior to check-in. As one can imagine this causes a huge loss of revenue for our client as not all of the cancellations can be replaced with new customers in time for the check-in date.

![Hotel Reservation Count](https://github.com/ravimalde/hotel_cancellation_analysis/blob/master/images/cancellation_count.png)

## Our Solution

Our primary goal was to be able to accurately identify a customer that had a high likelihood of cancelling prior to check-in at the point of purchase. We ran a total of 15 different models, the best of which was a Random Forest Classifier. It was able to identify 99.0% of individuals that do cancel and 98.7% of individuals that do not cancel (on our test dataset). With the accuracy of this model there are many feasible ways of curbing the revenue loss from cancellations.

[image goes here]

Prior to engaging with us, the hotelier had already decided that going forward all customers will be charged a base deposit of 25%. This was the standard rate before, however some customers were able to book deposit free through various packages avialable via travel agents. Our proposal was that individals that are flagged as having a high chance of cancelling should be charged a higher deposit at 50% of the total booking price, resulting in lower losses if they do cancel.

1) This could be a good excerise to tackle the real-world dataset.
2) Evenly distributed ( roughly half of the data is cancelled and the other half is not cancelled)



Objectives 

1) how to mitigate the problem of cancellation and 
2) how to maximise the profits (Minimise the loss) from this context.
3) Provide insights about the users who is likely to cancel the hotel booking 
4) Select the best model and predict the conversion probabilities of the users 

Methodology

1) Data ingestion

EDA

2-1) Balanced Classes:

An assumption of classification models is that all the classes are of equal occurrence in the data set. 
In our case of a binary classification problem, the split is 50/50.
We have nearly even number of the dataset.

2-2) Data Encoding 

We initially tried the method of "One Hot Coding" and it caused the Sklearn version problem. 
Thus we used "dummies" instead.

3) Modeling

3-1) Data Scaling

In order to apply Logistic Regression, the data must be scaled in advance, 
because its accuracy might be influenced.

3-2) Data splitting (X,y split)

3-3) Class Modelling

We have made " pre-made coding" to apply later.

4) Models

we tested numbers of models 

I) Logistic Regression

( L.Regression is very easy to use and it generally gived a good prediction)  

we evaluated with following number of evaluation techniques:

1) Accuracy, 
2) Precision 
3) Recall 
4) F1_Score
5) Roc_Auc Score
6) Confusion Matrix

and we found two meaningful ones ( ROC and Confusion Matrix)

1) ROC

Train AUC (0.903361)
Validation AUC (0.898656)

2) Confusion Matrix

(7541, 1170),(1584, 4574)



II) Decision Trees 

1) Iteration 1

Train AUC (0.927799)
Validation AUC (0.919023)

2) Iteration 2

Train AUC (0.933974)
Validation AUC (0.921681)

3) Iteration 3

Train AUC (0.936956)
Validation AUC (0.923146)

4) Iteration 4

Train AUC (0.9372820)
Validation AUC (0.923006)

Confusion Matrix

(7812, 899),(1432, 4726)

We can clearly see that we have improved the accuracy from iterations (0.919023-> 0.923006)


*****************
Conclusion:

Decision Tree shows better accuracy over Logistics regression 

Logistic regression (0.898656) < Decision Tree (0.923006)

In addition, confusion matrix is also better than Logistics Regression.

Logistic regression (7541, 1170),(1584, 4574)  <  Decision Tree (7812, 899),(1432, 4726) 

we have better True Positive 7541 < 7812.
*****************


III) Random Forest

1) Iteration 1

Train AUC (0.999411)
Validation AUC (0.946462)

2) Iteration 2

Train AUC (0.998293)
Validation AUC (0.947042)

3) Iteration 3

Train AUC (0.998293)
Validation AUC (0.947042)


*****************
Conclusion:

ROC: Decision Tree (0.923006) < Random Forest (0.947042)

Matrix: Decision Tree (7812, 899),(1432, 4726) < Random Forest (8057, 654),(1185, 4973)  
*****************




IV) Ensemble Methods ( Train AUC, Validation AUC)

1) Voting Classifier (0.97889,0.942302)

2) AdaBoost - Random Boost ( 0.999942, 0.932234)

3) XGBoost (0.920237, 0.920104)

4) Stacking (0.996112, 0.948935)

*****************
Stacking has the highest accuracy of 0.948935
*****************


V) Model Selection 

We found that Stacking has the highest accuracy of 0.948935.

However, we decided to go for Random Forest, since it is faster and simpler method than Stacking.
Moreover, its different is only 0.001893.

VI) Importance Feature

We found the list of important features below

	Importance	Feature
	0.101343	LeadTime
	0.081141	Country_PRT
	0.074694	TotalOfSpecialRequests
	0.060365	ADR
	0.046779	PreviousCancellations
	0.029017	CustomerType_Transient
	0.027794	StaysInWeekNights
	0.020519	CustomerType_Transient-Party
	0.019357	StaysInWeekendNights
	0.017951	MarketSegment_Online TA
	0.016006	MarketSegment_Groups
	0.015982	Agent_ 9
	0.015354	Adults
	0.014579	DistributionChannel_TA/TO
	0.014467	Country_FRA
	0.013896	Agent_ 7
	0.012924	Country_DEU
	0.011856	AssignedRoomType_D
	0.009492	RequiredCarParkingSpaces
	0.009331	DistributionChannel_Direct

VII) Threshold Selection



VIII) Recommendation

1) Rather than apply the high - deposit models. 
   Future work might be good to find out the descount model( no need for deposit Early cancellation)
   or sell more services (cheaper rate of room upgrade , free internet wifi or 10% discount on the hotel restaurant etc)
   at the time of booking with discounted rate and charge them normal rate of cancellation of fee for all services 
   (room charge and services)
   
   
   


