# Predicting the future price of ETH

A support vector regression (SVR) model and LSTM recurrent neural network (RNN) are implemented to predict future prices of the ETH cryptocurrency based on daily historical data.

The SVR model was implemented using scikit-learn, and also involves the standard data science stack -- NumPy, Pandas, and Matplotlib.

Moreover, the Optuna library is used to automate the model's hyperparameter tuning before it trains to maximize accuracy.

# Support Vector Regression

The model seemed to be prone to overfitting. I found that with a test size of 0.2, the model was getting an accuracy of near zero. But as I experimented with larger test sizes, results got slightly better up until a test size of around 0.4. Beyond this point, the model began to perform worse, likely because it didn't have enough training data. 

I noticed that the SVR model was not very effective when given just one input variable. I initially provided it just the 'Date' column, and accuracy was only about 25-40% at best depending on hyperparameters. I instead provided it the Date, Open, and Close columns as input to predict the price (3 days into the future in this case).

Results were much better, with the model obtaining an accuracy of around 98% on the test set.

However, I wanted to take this one step further to see if there was a better way. I had heard of LSTM and recurrent neural networks being used for time series analysis which got me curious to see how well it performs compared to a typical regression model.

# To do:
Implement LSTM RNN to predict prices and compare results with SVR
