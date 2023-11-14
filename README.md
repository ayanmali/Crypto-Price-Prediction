# Predicting the future price of ETH

A support vector regression (SVR) model and LSTM recurrent neural network (RNN) are implemented to predict future prices of the ETH cryptocurrency based on daily historical data.

The SVR model was implemented using scikit-learn, and also involves the standard data science stack -- NumPy, Pandas, and Matplotlib.

Moreover, the Optuna library is used to automate the model's hyperparameter tuning before it trains to maximize accuracy.

# Support Vector Regression

Preprocessing the data was an important part of the process to take into consideration. Here it involves scaling the data down so that every value ranges from 0 to 1. This way the models can train faster. Generally, scaling the input data down seems to boost performance in ML models as well. Also, the 'Date' column isn't very useful as it is, so I had to convert those values into integers by first converting them into datetime objects, then converting those values into integers via `dates` from Matplotlib. Moreover, the data was split into training and testing sets as typical when building any ML model.

The model seemed to be prone to overfitting. I found that with a test size of 0.2, the model was getting an accuracy of near zero. But as I experimented with larger test sizes, results got slightly better up until a test size of around 0.4. Beyond this point, the model began to perform worse, likely because it didn't have enough training data. 

I noticed that the SVR model was not very effective when given just one input variable. I initially provided it just the 'Date' column, and accuracy was only about 25-40% at best depending on hyperparameters. I instead provided it the Date, Open, and Close columns as input to predict the price (3 days into the future in this case).

Results were much better, with the model obtaining an accuracy of around 98% on the test set.

However, I wanted to take this one step further to see if there was a better way. I had heard of LSTM and recurrent neural networks being used for time series analysis which got me curious to see how well that would perform compared to a typical regression model.

# LSTM Neural Network

I realized pretty quickly that for an LSTM deep learning model, it needs to take in a 3D array as its input; one dimension for the number of rows/samples, another dimension for the number of columns (features), and another dimension for the number of time steps to look back on to make predictions. This makes sense since LSTM is used for time series analysis, so it needs a certain amount of data from the past to forecast.

I chose to set the timesteps value to 15, so the model looks at 15 day intervals to determine what the price of ETH will be in 3 days.

Preprocessing the data was the most important component here. I took the cleaned data from the last section and preprocessed it again similarly to how it was done before, except the data was split in a different way. First the dataset is split into one set for training and validation for the model, and another set for testing. Once the datasets were ready, it was time to build the model.

Once again, Optuna was used to automatically tune the hyperparameters. In this case the only HPs to optimize were the number of units in each LSTM layer as well as the Dropout percentage, which is important to prevent the model from overfitting. It does this by switching off some neurons when the weights update, so that other neurons can learn better.

Once I had the optimal HP values it was time to actually create the model and train it. This is where the validation set comes into play to determine the model's performance during training so it can improve over the training period, which was 50 epochs in this case.

Now that the model was trained, I provided the test set to it and plotted its performance along with some metrics. It turned out that the SVR model seemed to be more accurate at around 98% compared to the ~89% from the LSTM model.

Here are my thoughts going forward:
Something I want to experiment with more is to see how the model's performance changes (if it all) depending on the timesteps value. If I gave the model a smaller or larger interval of days of price data, will it predict the future price more or less accurately?

I used two LSTM layers when building the model, but I do want to know how the model's performance changes if I add an extra layer or two.

It might simply need to train longer, or perhaps more refined hyperparameter tuning to improve its accuracy.

# To do
Adjust the x-axis and y-axis scale for the NN accuracy raph
