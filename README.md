Problem Statement:


Part 1:  Predict and Identify the Customers who have a very high delay in Invoice to Cash Collection.
Part2: Predict and Identify the weekly Collection Insight from a Date, i.eThe Customers who are likely to pay within the next week of a date given as input.
Part 3: Predict the sales of Cash based Customers for the next 5 days from the current date.

Analytics

•	The First Problem:The Dataset provided was the past record of 9 Months of the BPR Only, B2B Customers of Tata Steel
•	The Dataset contained Cross Sectional and Time Series Features and was basically a Panel Dataset. So, I could neither use basic approaches of Machine Learning nor pure ARIMA Model.
•	The main challenge was to predict the minority class, i.e, in the entire dataset contained over 110 thousand data points out of which the Class of No Delay, i.e. The Customer transactions which did not incur delay in Invoice to Cash Collection was more than 90 thousand. The Customer Transactions which suffered the significant delay of more than 30 days were very few in number, 224. 
o	The technique used to tackle this problem was to generate Synthetic data points using the ADASYN algorithm 
o	PAPER :ADASYN: Adaptive Synthetic Sampling Approach for Imbalanced Learning .
o	AUTHORS :  Haibo He, Yang Bai, Edwardo A. Garcia, and Shutao Li
o	Source : IEEE JOURNAL 2008
o	The picture of the algorithm is attached.


 

•	The Next task was based on Feature Engineering where two Columns were generatedmanually, one being the number of Pending Invoices prior to a Posting Date of an Invoice for every customer and the last was the Amount of Pending Invoices prior to a Posting Date for every Customer.
•	After Feature Engineering choice of Model was very important, being a Supervised Learning Type Classification Problem. After checking accuracy for 3 of the Models, a weighted Voting Classifier was used to predict the Final Output. 
•	The 3 Models being used are – Random Forest, Adaaboot with base learner as Decision Tree, Bagging Classifier with base estimator as KNN. The Random Forest algorithm performs the best. Though no correct set of reasons are known yet with a few searches I got a few probable reasons:
	Random Forests can handle thousands of input variables without variable deletion.
	It generates an internal unbiased estimate of the generalization error as the forest
building progresses.
•	Prototypes are computed that give information about the relation between the
variables and the classification. 

•	The Final Output contained 3 classes – No Delay (Customers with no Invoice to Cash Delay) ; Low Delay (Customers who pay within 7 days from Due Date) ; High Delay (Customers who don’t pay within the 1st week.)
•	The Dataset was split into 3 segments : Training – 70%
     Testing and Validation – 15% and 15% each

•	Accuracy:
o	Training Accuracy : 99.35
o	Testing Accuracy : 97.28

-------------------------------------------------------------------------------------------------------------------------------
•	The Second problem : This was a very interesting problem where we needed to predict the estimated Clearing Date.
•	We used two models in order to predict the Estimated Date of Clearing.
	First: Model predicting estimated date of clearing from Net Due Date.
	Second : Model predicting estimated date of clearing from Posting.
o	We use the agreement of both the models in a range of 5 days to predict the final number of Invoices that will be cleared.
•	In Second Problem too Random Forest outshone the Other Classifiers.
•	The training and Testing data was all data before the Input Posting Date and the Validation Data was all the data points whose invoices were raised before the Posting Date but was not cleared.
o	The Training Accuracy for Model 1 : 99.98
o	The Testing Accuracy for Model 1 : 94.04
o	The Training Accuracy for Model 2 : 99.36
o	The Testing Accuracy for Model 2 : 97.67
-------------------------------------------------------------------------------------------------------------------------------
•	The Third problem: This problem was not as difficult as the rest of the problems. We used Arima to forecast the sales of the Individual Customers for the next 5 days from a specified date.
o	ARIMA is an Ideology that captures autocorrelation in the series by modelling it directly.
o	Lags of the stationarized series are called “autoregressive” that refers to (AR) terms & Lags of the forecast errors are called “moving average” which refers to (MA) terms.
o	The autocorrelation function (ACF). Intuitively, a stationary time series is defined by its mean, variance and ACF. A useful result is that any function of a stationary time series is also a stationary time series.
o	We plotted the PACF and the ACF and used those as q and p, respectively in ARIMA(p,d,q). The differential
o	In time series analysis, the partial autocorrelation function (PACF) gives the partial correlation of a time series with its own lagged values, controlling for the values of the time series at all shorter lags. It contrasts with the autocorrelation function, which does not control for other lags.
o	The Terminologies involved:
	p = No. of Auto-Regressive Terms
	d = No. of Non-Seasonal Differences
	q = No. of Moving Average Terms
•	These 3 are used to model ARIMA(p,d,q)
o	Advantages :It is a strong underlined mathematical theory which makes it easy to predict “PREICTIVE INTERVALS” which is it is flexible in capturing a lot of different parameters.
o	Disadvantages :No explicit seasonal indices, hard to interpret coefficients or explain “how the model works”, there is danger of overfitting or mis-identification if not used with care.

<img src="https://github.com/SOUMYABROTOBANERJEE/CashInvoicePredictor/raw/master/Required_GIF.gif" width="400" height="400" />
