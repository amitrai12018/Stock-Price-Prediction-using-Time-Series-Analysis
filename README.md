
# Stock-Price-Prediction-using-Time-Series-Analysis
Used Historical data of stock prices of 3 companies listed in National Stock Exchange (NSE), predicted the future stock price for the companies.
![image](https://user-images.githubusercontent.com/45662797/132518806-30b74642-5d31-4c98-844a-74e1ce1b0f7e.png)
![image](https://user-images.githubusercontent.com/45662797/132519038-63827e22-1d52-4c4a-af21-1e12c3273cff.png)
![image](https://user-images.githubusercontent.com/45662797/132519148-8a6e8944-6fbf-4a0d-a653-7d19f9c6c268.png)

# Problem Statement
 Using Historical stock Price data given for a company can we predict the future stock price for future?
## Review:
   There are number of statistical models like Arima forecasting, Linear Regression, but none of them take place long term dependencies into consideration. In this regard, Deep learning techniques use be saviour as they are good in capturing long term dependencies. 
   
   **"Hence standard RNNs fail to learn in the presence of time lags greater than 5 – 10 discrete time steps between relevant input events and target signals. The vanishing error problem casts doubt on whether standard RNNs can indeed exhibit significant practical advantages over time window-based feedforward networks. A recent model, “Long Short-Term Memory” (LSTM), is not affected by this problem. LSTM can learn to bridge minimal time lags in excess of 1000 discrete time steps by enforcing constant error flow through “constant error carrousels” (CECs) within special units, called cells"**
   𝙍𝙚𝙛𝙚𝙧 𝙩𝙤 𝙩𝙝𝙞𝙨 𝙥𝙖𝙥𝙚𝙧 : https://ieeexplore.ieee.org/document/9005997

— Felix A. Gers, et al., *Learning to Forget: Continual Prediction with LSTM, 2000*
## Data Set:
The We used stock Price for about 12 years for dataset, we got out dataset from National Stock Exchange(NSE) for three companies: SBI, YesBank and HDFC Bank stock price.
Daily High, Low, Open, Close values were taken collected from credible website.
The dataset can be assessed from the dataset folder.
## Data Preprocessing:
First of all We created a windowed dataset where each data point comprising of 5 time-steps at the gap of 1 day, so 5 days 1 data point, the stock price for next day is given as the output for that data point. Then we split dataset in training to validation/test ratio 80 % to 20 %.
## Approach
Enough emphasis has been laid on using LSTM Layers. So, furthur we discuss what makes our approach different from others :
### Model Summary
![Screenshot (834)](https://user-images.githubusercontent.com/45662797/132556133-66f2bb3c-fb25-4acb-b408-e89125177328.png)
### Training 
During the training process, we simply fit each training input using 'Adam Optimizer' with default learning rate, 0.001 and loss function mse on 500 epochs
### Testing 
Let us define what is Feedback loop:

** Feedback loop: 

** say you are on day 1 of the test data, you already have learned weights from the model fitting on training data. For prediction on test data we assume that we want is model to give more weight to what was the market condition in last 20 days. So we want to customise our model to learn this 20 days time window so we train our trained model again on the data window of last 20 days which consists of last 17 data points because last in training set data point already contains the data for last 5 days we need 16 days more, then after fit model on these 17 data points for  10 epoches we predict on last day, and repeat the same for future timesteps.
This testing method ensures more weight to recent happenings in the market.
### Interesting Results,
  Do You remember Yes Bank Market Crash in 2020 ? Let me remind you through the graph of closing, opening, high price prediction vs actual graphs.![Screenshot (263)](https://user-images.githubusercontent.com/45662797/132560102-c7235a8e-6236-449d-b53a-3dc51ac01d3c.png)
![Screenshot (262)](https://user-images.githubusercontent.com/45662797/132560306-114ef438-e817-4de9-9c9d-38ff6d88e5c3.png)
![Screenshot (261)](https://user-images.githubusercontent.com/45662797/132560507-20449db6-68ba-4eb9-bb35-885d9db3ce7c.png)

Total MSE: 2.58 

>> Between day 700 to day 500 you can see there has been a crash in Yes Bank stock price. And we could have predicted it! (see the predicted(blue) and (actual) orange lines ) 
>> But could we have made people profitable as by claiming that Yes bank stock is going to crash? 
      may be may be not! model fidelity is a big question that is still unanswered, since we are predicting the price of next day, intutively model will take time to capture it once the sudden crash takes place, it will quickly learn about the crash. 
## End Note:
  I think Model can give a good prediction for stock price to a good extent if some sudden crashes donot happen as happened in case of Yes Bank, it can be used.
  Model Can be improved by adding tweet/news sentiment analysis so that we can have some prior idea of market crash! 
## Final Note:
![image](https://user-images.githubusercontent.com/45662797/132523863-519bc202-fff4-4de9-bfef-d0f1c370bc02.png)

 Yeah so here we learnt more about Bi LSTM's I am attaching the poster that we presented in Techevinche 2020 IIT Guwahati to the community in the folder, in the poster we have said as two lstms which is nothing but bilstms
