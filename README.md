# StockTrainer: Stocks Made Easy

StockTrainer is high level API data generator for training python machine learning models on stock and cryptocurrency data. 
It is capable of running with Keras, Tensorflow, sklearn, and many other machine learning APIs

Capabilities:

- Predict day to day stock prices
- Use multiple days to predict next stock price
- Predict succeeding stock prices over multiple days
- Train a reinforcement learning agent to simulate stock trades


Documentation available soon ;)

StockTrainer is compatible with: Python 3.6+

## Getting Started
The core of algorithm is the model, here is a simple LSTM model to based on 5 days of stock data to predict next day stock price

	import keras
	import numpy as np
	from keras.models import Sequential
	from keras.layers import Dropout ,BatchNormalization, LSTM, Dense 

  
	model = Sequential()
	#input shape 5 days of data 
	#each day has 6 data points (open, close, high , low volums, adj CLose)
	model.add(BatchNormalization(input_shape=(5, 6)))#batchnorm bc high values
    model.add(LSTM(512, return_sequences=True, activation='relu'))
    model.add(Dropout(0.2))
    model.add(Dense(512, activation='relu'))
	model.add(Dense(128, activation='relu'))	
    model.add(Dense(1, activation='relu'))

    model.compile(loss='mse', optimizer='adam')

Next import StockTrainer and create your environment
 
    from StockTrainer import Env
    enviorment = Env("Standard", "AAPL")

Time to collect your data to train!!!

	test_percent =.30
	shuffle =True
	start_date ='2003-01-01'
	end_date='now'
	agent_memory = 5
	seed = 42
	trainx,testx,trainy, testy = environment.train_test(
	test_percent= test_percent, shuffle = shuffle, 
	start_date=start_date, end_date=end_date,
	agent_memory=agent_memory, seed=seed)

Futher information on parameters in Documentation 


That's it now train and test your model
	
	#fit model
    model.fit(trainx, trainy, epochs=10, batch_size=128, verbose=2)
    model.save('model.h5')

    #evaluate model
    model.evaluate(testx,testy )
    #use model to predict
    model.predict(testx)

More examples in samples folder in github

## Installation

Using pip
	
	pip install StockEnv

or download directly: [https://pypi.org/project/StockEnv/](https://pypi.org/project/StockEnv/ "install") 
