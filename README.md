# Hotel Cancellation Analysis

The aim of this project was to mitigate the loss of revenue to a hotel due to the cancellation of bookings. The dataset used contained customer booking information for 80,000 bookings over a two year period, from which we were trying to predict the likelihood of that booking being cancelled prior to the check-in date. This project was a collaborative effort between Ravi Malde and Seung Won Lee.

Ravi Malde Contact Info:
- Email: ravidmalde@gmail.com
- LinkedIn: www.linkedin.com/in/ravi-malde
- Medium: www.medium.com/@ravimalde

Seung Won Lee Contact Info:
- Email: jesuslsw21@gmail.com
- LinkedIn: www.linkedin.com/in/james-seungwon-lee-a681b855

## Table of Contents

1. [ File Descriptions ](#file_description)
2. [ Methods Used ](#methods_used)
3. [ Technologies Used ](#technologies_used)
4. [ Executive Summary ](#executive_summary)

<a name="file_description"></a>
## File Descriptions

- index.ipynb: notebook conatining all of the code.
- H2.csv: the dataset obtained from [ScienceDirect](https://www.sciencedirect.com/science/article/pii/S2352340918315191).
- images: contains images used in the readme file.
- superseded: contains superseded notebooks.
- Column_Description_1.png: Outlines the definitions of dataset features.
- Column_Description_2.png: Outlines the definitions of dataset features.

<a name="methods_used"></a>
## Methods Used

- Data exploration
- Data visualisation
- Data cleaning
- Feature engineering
- Machine learning

<a name="technologies_used"></a>
## Technologies

- Python
- Pandas
- Numpy
- Matplotlib
- Seaborn
- Scikit-learn

<a name="executive_summary"></a>
## Executive Summary

Our dataset contained 79,330 bookings made between 1st July 2015 and 31st August 2017. Of these, 42% were cancelled prior to check-in (as can be seen in the plot given below). As one can imagine, this causes a huge loss of revenue for our client as not all of the cancellations can be replaced with new customers in time for the check-in date. The aim of this analysis was to identify which characteristics of customers indicate that they are of a high probability to cancel, and to provide actionable insights on how to mitigate any losses.

<h5 align="center">Hotel Reservation Count</h5>
<p align="center">
  <img src="https://github.com/ravimalde/hotel_cancellation_analysis/blob/master/images/cancellation_count.png" width=750>
</p>

We take ethics very seriously so for obvious reasons race, religion, gender and biological sex have not been considered in the model. This is not to say that the model isn't indirectly discriminating against certain groups via the other features, therefore this is something that will require close monitoring after its implementation. More will be covered on the topic of ethics towards the end of this document.

### Preprocessing

Fortunately, the dataset was already in good shape, presumably because it was created knowing that it would be used in an official study as seen on [ScienceDirect](https://www.sciencedirect.com/science/article/pii/S2352340918315191). However there were still 28 null values present. Due to the relative size of the total dataset and the nulls, these were omitted from the analysis. After this, columns that were not going to be used were also removed. For example, 'BookingChanges' was removed because the purpose of the model is to identify individuals that are likely to cancel at the point of purchase, therefore at that time it is unknown how many booking changes they will make prior to check-in.

The features contained in the dataset at this point were as follows (the definitions of these can be found in the Column_Description_1.png and Column_Description_2.png files):

- LeadTime
- ArrivalDateMonth
- ArrivalDateWeekNumber
- ArrivalDateDayOfmonth
- StaysInWeekendNights
- StaysInWeekNights
- Adults
- Children
- Babies
- Meal
- Country
- MarketSegment
- DistributionChannel
- IsRepeatedGuest
- PreviousCancellations
- PreviousBookingsNotCanceled
- ReservedRoomTpye
- AssignedRoomType
- Agent
- DaysInWaitingList
- CustomerType
- ADR
- RequiredCarParkingSpaces
- TotalOfSpecialRequests

The data set had 12 numerical and 12 categorical features. The categorical features were then one hot encoded, reusulting in a dataframe with 524 columns. After this, the dataset was then split into a training set (44,607 instances), a validation set (14,869 instances) and a test set (19,826). A StandardScaler object was then fit to the numerical features in the training dataset and used to tranform the instances in that same set. The same scaling object was then used to transform the numerical features in the validation and test datasets.

### Modelling

Seven different model types were created and their hyperparameters were tuned using GridSearchCV. the metric by which the models were compared was their validation AUC ROC (the table below gives all of the model performances sorted by this metric). The final model chosen was the 4th iteration of random forest classifier as it was one of the best performers and was relatively low in complexity compared the the best performer (stacking classifier). As can be seen from the table, there were some reproducibility issues with the random forest classifier as the first iteration was actually the best performer despite the grid search narrowing down the parameters to the optimum range. This is currently thought to be due to floating point rounding errors or a multiprocessing issue. The differences in performance are very small and considered negligible. 

<h5 align="center">Model Performances</h5>
<p align="center">
  <img src="https://github.com/ravimalde/hotel_cancellation_analysis/blob/master/images/moedl_performances.png" width=450>
</p>

Some interesting insights from the model were the relative importances of the features. These indicate how important a given feature is in determining whether or not a booking is going to be cancelled. The graph below shows the relative importance of the top 20 most important features in the dataset.

<h5 align="center">Feature Importances</h5>
<p align="center">
  <img src="https://github.com/ravimalde/hotel_cancellation_analysis/blob/master/images/feature_importance.png" width=850>
</p>

1. LeadTime: the time between the booking being made and the check-in date.
2. Country_PRT: if the booking was made from Portugal. The identity of the hotel was kept anonymous in the dataset, however Portugal had the highest number of bookings, so it is assued that the hotel is based somewhere within the country.
3. TotalOfSpecialRequests: the number of special requests made in the booking. A special request is when a customer asks for anything that does not come standard in the booking (i.e. a certain number of beds in the room or special linen).
4. ADR: the Average Daily Rate. This could be considered a proxy for whether or not the hotel is in a busy period at the check-in date.
5. PreviousCancellations: the number of times the customer has cancelled previous bookings.

The model was able to correctly identify 99.6% of individuals that do cancel and 99.7% of individuals that do not cancel (on our test dataset). With the accuracy of this model there are many feasible ways of curbing the revenue loss from cancellations. Our recommendations to the client are theat they increase the base level of deposit from 25% to 50% for individuals that are classified as people that are going to cancel. From our calculations we estimate that this will increase their revenue by 20,000€ per 1000 bookings, equating to 790,000€ per year.
