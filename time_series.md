#### Class 16 Time Series
do starter code Exercises in starter-code-15.ipynb
do check out the solution code and see some of the syntactical things your are missing like double square brackets 
do cement understanding of "cross-validation"
* wellness project
1. AutoRegressive (AR) Model
2. Moving average (MA) Model
3. ARMA (combines AR and MA)
L16-Demo has Time Series modeling L16-Demo.ipynb and with Walmart starter-code-16.ipynb
*do resample autocorr on wellness data to see if there is a trend; "predict for the individual or the population"

online time series arma exercise:

https://machinelearningmastery.com/arima-for-time-series-forecasting-with-python/

"comprehensive mapping of failure is a finding"

ABC liquor sales based on tod, toy
crime in summer/winter

data['Sales'].resample('D').mean().autocorr(lag=364) 

autocorrolation - compares with itself

show the mean to nail down where the right skew is coming from?

bring in supps? look at monthly intake of x against hr? against strava? sleep?

for what to fix, look at next time: subjective evaluation of effort? 

####Time Series Modeling

like other predictive modeling we predict the future

unlike previous models - we are using historical outcomes to predict the future outcomes as opposed to features
