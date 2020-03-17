# Hotel Cancellation Analysis





Abstract 

We are a data science consultancy that has been hired by a large hotel chain to investigate viable methods of mitigating the impact of short-notice customer cancellations. The approach taken in this analysis was to look at what characteristics of an individual may indicate that they are of a high probability to cancel. If an individual is deemed likely to cancel, they are charged a higher deposit at the point of purchase. This means that some of the lost revenue due to cancellation is recovered, thus reducing the overall cost to our client. We take ethics very seriously so for obvious reasons race, religion, gender and biological sex have not been considered. All customers data:image/png;base64,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%0Awill pay the same overall price (if they are purchasing the same product), it is only the initial deposit (as a % of the total price) that will change on a customer to customer basis.



Context

This dataset describes hotel(city) demand data, with 31 variables describing the 79,330 observations( observation represents a hotel booking. )
Also, datasets comprehend bookings due to arrive between the 1st of July of 2015 and the 31st of August 2017, including bookings that effectively arrived and bookings that were canceled. 

The dataset now made available were collected aiming at the development of prediction models to classify a hotel booking׳s likelihood to be canceled. Nevertheless, due to the characteristics of the variables included in thIs dataset, their use goes beyond this cancellation prediction problem.

we chose this dataset, because of the following reasons below:

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
   
   
   


