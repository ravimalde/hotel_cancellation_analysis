# Hotel Cancellation Analysis

This project was a collaborative effort between Ravi Malde and Seung Won Lee.

# Executive Summary

A large hotel chain has approached us to investigate viable methods of mitigating the impact of short-notice customer cancellations. The aim of this analysis was to identify which characteristics of customers indicate that they are of a high probability to cancel, and to provide actionable insights on how to mitigate any revenue loss due to cancellations.

We take ethics very seriously so for obvious reasons race, religion, gender and biological sex have not been considered. All customers pay the same overall price (if they are purchasing the same product), it is only the initial deposit (as a % of the total price) that will change on a customer to customer basis. It is important to note that despite our model not considering these characteritics directly, it must be monitored post implementation to determine whether or not it is discriminating against any goups indirectly throught the variables that have been considered.

## The Problem

Our dataset contained 79,330 bookings made between 1st July 2015 and 31st August 2017. Of these, 33,076 were cancelled prior to check-in. As one can imagine this causes a huge loss of revenue for our client as not all of the cancellations can be replaced with new customers in time for the check-in date.

![Hotel Reservation Count](https://github.com/ravimalde/hotel_cancellation_analysis/blob/master/images/cancellation_count.png)

## Our Solution

Our primary goal was to be able to accurately identify a customer that had a high likelihood of cancelling at the point of purchase. We ran a total of 15 different models, the final model chosen was a Random Forest Classifier as it was one of the best performers and was relatively low in complexity compared the the best performer (stacking classifier). The graph below shows the relative importance of the top 20 most important features in the dataset.

![Feature Importances](https://github.com/ravimalde/hotel_cancellation_analysis/blob/master/images/feature_importance.png)

1. LeadTime: the time between the booking being made and the check-in date.
2. Country_PRT: if the booking was made from Portugal. The identity of the hotel was kept anonymous in the dataset, however Portugal had the highest number of bookings, so it is assued that the hotel is based somewhere within the country.
3. TotalOfSpecialRequests: the number of special requests made in the booking. A special request is when a customer asks for anything that does not come standard in the booking (i.e. a certain number of beds in the room or special linen).
4. ADR: the Average Daily Rate. This could be considered a proxy for whether or not the hotel is in a busy period at the check-in date.
5. PreviousCancellations: the number of times the customer has cancelled previous bookings.

It was able to correctly identify 99.6% of individuals that do cancel and 99.7% of individuals that do not cancel (on our test dataset). With the accuracy of this model there are many feasible ways of curbing the revenue loss from cancellations.

