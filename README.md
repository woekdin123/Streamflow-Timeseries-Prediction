# “ARIMA and LSTM for Streamflow Time Series Forecasting: A Statistical and Machine Learning Approach’’ 
## Project Overview
This project focuses on time series forecasting of adjusted inflow (in million cubic meters, MCM) in a hydropower reservoir using historical data. Accurate inflow prediction is critical for effective water resource management, given the influence of seasonal variations and long-term trends.

We implemented and compared three models:

ARIMA (Autoregressive Integrated Moving Average)

SARIMA (Seasonal ARIMA)

Bidirectional LSTM (Long Short-Term Memory)

Each model was evaluated based on the R-squared metric to determine its predictive performance. The goal was to identify the most effective model for forecasting, combining traditional statistical methods with modern deep learning approaches to support informed decision-making in hydrology.

## Data understanding
We have month and year data which shows how much streamflow is coming in a month as shown in fig 1.
![image](https://github.com/user-attachments/assets/0cc520fa-d7d9-41c7-b2dc-dccefdf14212)

Fig. 2 illustrates the breakdown of the time series data into four main components: Original, Trend, Seasonality, and Residuals. Here's a simple explanation of each component:
## 1.	Original: 
This is the raw time series data, showing the adjusted inflow (MCM) over time. The graph captures the overall pattern, which includes fluctuations, peaks, and troughs over the years. You can see that the data has repeated spikes, which may correspond to seasonal changes.
## 2.	Trend: 
The trend component shows the long-term movement in the data, revealing periods of increase and decrease, as well as a noticeable rise in the later years.
## 3.	Seasonality:
The seasonality component emphasizes the recurring patterns or cycles within the data. The graph shows a clear seasonal pattern in the adjusted inflow, suggesting higher inflows during specific times of the year due to natural factors like rainfall or snowmelt.
## 4.	Residuals:
The residuals are the remaining variations in the data after removing the trend and seasonality. They represent irregular fluctuations not explained by trend or seasonality, indicating unpredictable variations possibly due to unusual weather events or other factors.
These graphs help us understand the structure of time series data by breaking it down into its fundamental components. This understanding is crucial for accurate forecasting models, allowing us to model trend and seasonality separately and address randomness in the residuals shown in Fig. 2.
![image](https://github.com/user-attachments/assets/2c2cb9c0-4c2a-422e-ad67-b6e608602a54)

## ARIMA Model- Statistical approach
In this study firstly we apply the ARIMA model, ARIMA, short form of Autoregressive Integrated Moving Average, is a forecasting algorithm based on the idea that the information in the past values of the time series can alone be used to predict the future values. ARIMA models are specified by three order parameters: (p, d, q), where,

•	p is the order of the Auto Regressive (AR) term. It refers to the number of lags of Y to be used as predictors.

•	The value of d, therefore, is the minimum number of differencing needed to make the series stationary. If the time series is already stationary, then d = 0.

•	q is the order of the Moving Average (MA) term. It refers to the number of lagged forecast errors that should go into the ARIMA Model.

## LSTM- Machine learning approach
Next we apply LSTM (Long Short Term Memory), a machine learning based approach for prediction of streamflow time series data. 
LSTM (Long Short-Term Memory) is a type of recurrent neural network (RNN) architecture specifically designed to handle sequences of data, which can include time series, natural language, and other sequential tasks. Unlike traditional RNNs, LSTMs are capable of learning long-term dependencies, which is a key advantage in many applications where past information is critical.
Before building any models, it’s crucial to analyze the data for stationarity and seasonality, as these characteristics influence the choice and effectiveness of time series models.
## •	Stationarity:
Stationary data has a constant mean and variance over time, which is essential for many time series models like ARIMA. To test for stationarity, techniques such as the Augmented Dickey-Fuller (ADF) test can be applied. In this case, the data shows non-stationary behaviour, meaning the mean and variance change over time, indicating trends or other non-constant behaviour. If the p-value of the Adfuller test is less than 0.05 implies series is stationary other wise series is non-stationary. If the series is stationary then strong evidence of the null hypothesis(HO), rejects the null hypothesis shown in Fig. 3. Data is stationary. Then we can apply the direct ARIMA model and others.
![image](https://github.com/user-attachments/assets/3995a5fe-d457-45c2-ac3a-2d9673f6575b)

## •	Seasonality: 
Seasonality refers to repeating patterns or cycles in data over a specific period. Through visual inspection and autocorrelation plots, the data reveals seasonal patterns, which means the adjusted inflow varies in a cyclical manner, likely due to seasonal environmental factors.

## Results and Discussion
### ARIMA (Auto Regressive Integrated Moving Average)
In this study our model is Stationary because p-value of Adfuller test is less than 0.05 implies series is stationary.  If the time series is already stationary, then d = 0. According to ARIMA model summary get the value of (p, d, q) = (1, 0, 1) then after fit ARIMA model. After prediction we find the value of R-squared and Root Mean Square Error (RMSE) is 0.29, and 195.193  and plot the actual data, fitted values (predictions), and forecast shown in Fig. 4, and Fig. 5.
 Values of R-squared and RMSE
              R-Squared	                RMSE
              0.29	               195.193

![image](https://github.com/user-attachments/assets/ac13168a-4065-48a5-8f40-2d1a5574da5f)

In this study, the ARIMA model predicts values between 850 and 1000 MCM, as shown in green in Figure 4. The future forecast using ARIMA falls between 140 and 145 shown in Fig. 4. The R-square value is quite far from 1, indicating that it is not the best fit. As a result, we decided to evaluate the SARIMA model for comparison

## SARIMA (Seasonal ARIMA)
SARIMA extends ARIMA by adding seasonal components to capture seasonality in the data. This makes it more suitable for datasets like ours, where seasonality is evident.  Values of R-squared and RMSE
                  R-Squared	                    RMSE
                        0.4955	                   268.6121

This study illustrates the performance of the SARIMA model in predicting adjusted inflow (MCM) over time, compared to actual observed data. The blue line represents historical data used to train the SARIMA model from 1972 to around 2004, extending into the prediction zone from 2004 to 2008. The red line shows the SARIMA model's predicted inflow values for the same period. SARIMA accounts for seasonality more accurately than a standard ARIMA model, resulting in a higher R-squared value of 0.59 compared to 0.29 for the ARIMA model shown in Fig. 5.

![image](https://github.com/user-attachments/assets/f28080fe-ae8c-4b7f-8b8e-3914a3684cf9)

The graph compares the performance of ARIMA and SARIMA models in predicting adjusted inflow (MCM) over time. The blue line represents the historical data, the green line shows fitted values from ARIMA, and the orange line shows fitted values from SARIMA. Both models follow the actual data, but the SARIMA model seems to capture seasonal peaks and troughs more accurately compared to the ARIMA model shown in Fig. 6.

![image](https://github.com/user-attachments/assets/43b3b968-967f-4e6a-9304-2072edcf42b5)

In the forecast period (2004-2009), the SARIMA model's predictions (orange dotted line) are closer to the actual data (blue line) than the ARIMA model's predictions (green dotted line). This indicates that SARIMA is better at capturing future trends and seasonality shown in Fig. 7

![image](https://github.com/user-attachments/assets/3e6da965-565b-4ae3-849e-821b97a9e730)

## LSTM Bidirectional (Long Short-Term Memory Bidirectional 
In this model, Figure 8 shows a comparison between actual data (represented by the blue line) and the predictions made by two different models: ARIMA (red dashed line) and Bidirectional LSTM (green dashed line). The data being analyzed is likely time series data representing inflows over time, measured in MCM, and the timeline spans from 1972 to 2008. The ARIMA model, a traditional time series forecasting method, tries to predict the data. However, as seen in the graph, its predictions do not closely match the actual data. This is reflected in the R-value (a measure of the model's accuracy) of 0.29, suggesting a weak correlation between ARIMA's predictions and the actual data. On the other hand, the Bidirectional LSTM model, a more advanced machine learning approach, performs much better in capturing the patterns in the actual data. Its predictions align more closely with the blue line, and the R-value of 0.90 indicates a strong correlation between the model's predictions and the actual data

R-Square (LSTM)	R-Square (ARIMA)
                        0.8386	                   0.29

![image](https://github.com/user-attachments/assets/6a7ce25b-f751-4886-ba95-c90b28425522)

In this model, Figure 9 shows the forecast of Bidirectional LSTM from February 2008 to March 2010.

![image](https://github.com/user-attachments/assets/cf632d0a-b0aa-4ca1-a9ae-46adca284086)

## Conclusion
The SARIMA model demonstrates a better fit for the streamflow data due to its ability to account for seasonality, resulting in more accurate predictions compared to the standard ARIMA model. This highlights the importance of choosing the appropriate model based on the characteristics of the data, particularly when seasonality is a significant factor.
Given the R-squared values, the LSTM Bidirectional model is the best fit for forecasting the adjusted inflow (MCM) in this dataset. The model's ability to understand and predict complex time series patterns, including trends and seasonality, makes it superior to both ARIMA and SARIMA in this case. For practical purposes, especially when accuracy is paramount, LSTM Bidirectional is recommended for future forecasts.















