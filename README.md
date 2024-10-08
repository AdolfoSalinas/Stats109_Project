Sales Forecasting with Walmart Sales Data 

Adolfo Salinas
Harvard University, Extension School  



Introduction

The goal of this project is to go into the field of sales forecasting with a particular emphasis on Walmart, one of the biggest names in retail. We aim to investigate how various factors, such as the time of year, economic conditions, and holiday seasons, affect sales by examining Walmart's vast network of stores.The question being tackling is: How can Walmart's sales be predicted across its various stores, taking into account the complex interplay of holiday seasons, economic indicators like unemployment rates and the consumer price index, and, of course, the sales history itself?

This study's driving hypothesis is simple to understand: We think a variety of factors affect Walmart's sales, with certain seasons of the year—like the holidays—having a major impact on the company's earnings because of increased consumer spending. Our objective is to sort through sales data from 45 Walmart locations that Kaggle has provided. This data includes not just sales numbers but also other details like regional weather, gas prices, and economic indicators. This detailed dataset is our foundation for unraveling the patterns that inform Walmart's sales dynamics.

The approach is to to identify patterns, understand the impact of various drivers on sales, and use this knowledge to make accurate future sales forecasts. We plan to develop predictive models that consider everything from the timing of sales to special events and beyond. A critical component of our strategy involves validating these models and establishing their reliability using metrics like Mean Absolute Error (MAE), Mean Squared Error (MSE), and Root Mean Squared Error (RMSE).

In essence, this project explores the complex world of sales forecasting by focusing on Walmart. Our objective is to discover methods that accurately forecast sales, considering a wide range of influencing factors. With this project,  I seek to shed light on the dynamics of retail sales forecasting and offer insightful information that could support strategic planning and decision-making within the retail industry.






Dataset Details

To provide an in-depth understanding of the dataset utilized in our sales forecasting project, let's delve into the specifics of the data. This Kaggle-sourced dataset, which includes information from 45 Walmart locations, provides a rich canvas for sales dynamics analysis and forecasting. The variables included in the dataset and their structure are broken down as follows:

Store: Identifies each of the 45 Walmart stores, enabling analysis that accounts for regional differences and store-specific characteristics.
Date: Records the week's ending date, a key factor for analyzing sales trends, seasonal effects, and holiday impacts over the specified period.
Weekly_Sales: The target variable, representing total sales in a given week for a store, provides the basis for our forecasting efforts.
Holiday_Flag: Indicates weeks that contain major holidays, essential for understanding holiday-related sales spikes.
Temperature: Averages the weekly temperature for each store's location, offering insights into how weather conditions affect shopping patterns.
Fuel_Price: Averages the weekly fuel price in the stores region, which can influence consumer spending habits and travel decisions to and from the store.
CPI (Consumer Price Index): Reflects the inflation rate and economic environment, impacting consumer purchasing power.
Unemployment: Indicates the unemployment rate in the store's region, a significant factor in consumer spending and overall economic health.

The dataset spans three years, from 2010 to 2012, a period that allows for the observation of post-recession recovery patterns, annual seasonal trends, and the effects of economic stimuli on consumer behavior. Each record in the dataset represents weekly sales data from one of the 45 Walmart stores, making for a detailed and comprehensive analysis of sales trends over time.

Hypothesis Test

We conducted a Welch Two Sample t-test to assess whether a significant difference exists between weekly sales during holiday periods compared to non-holiday periods at Walmart stores.

T-Statistic: -2.6801
Degrees of Freedom: 504
P-value: 0.007602

The test indicates a p-value of 0.007602, which is below the alpha level of 0.05. This indicates a statistically significant difference in the mean weekly sales between holiday and non-holiday weeks.

The 95% confidence interval for the mean difference between holiday and non-holiday weekly sales ranges from -141,473.17 to -21,789.85. This interval does not encompass zero, further supporting the existence of a true difference in sales performance between the two groups.
Furthermore, the negative sign on the confidence interval suggests that sales are higher during holiday weeks compared to non-holiday weeks. This aligns with expected consumer behavior, where purchasing typically increases during holiday seasons due to promotions and seasonal shopping trends.

Given the statistical evidence from the t-test and the derived confidence interval, we reject the null hypothesis that there is no difference in mean sales between holiday and non-holiday periods. The analysis confirms that holiday periods significantly impact sales figures, likely reflecting increased consumer activity during these times. 

Regression Models

Next I created a series of multiple regressions to compare to the Time Series autoregression (ARIMA). Regression models are predicated upon certain assumptions regarding the underlying data set. We assessed and addressed outliers, skew, normality and correlation to ensure solid performance of the regression.

Correlation Analysis

Negative Correlations:
Weekly Sales and Store: A moderate negative correlation (-0.34) might indicate that certain stores have lower sales. This could be due to a variety of factors like location, size, or customer base.

Weekly Sales and Unemployment: A weak negative correlation (-0.11) suggests that higher unemployment in the store's area might be associated with slightly lower sales. This could be an indicator of the economic health of the area affecting purchasing power.

CPI and Unemployment: A moderate negative correlation (-0.30) implies that higher unemployment is associated with lower CPI values, which could suggest economic downturns in areas with higher unemployment.

Positive Correlations:
Fuel Price and Temperature: A weak positive correlation (0.14) suggests that as temperatures rise, fuel prices might also increase slightly, which could be related to seasonal variations.

CPI and Temperature: A weak positive correlation (0.18) indicates that CPI might be higher when temperatures are higher, though the reason for this correlation would require further investigation.

Store and Unemployment: A weak positive correlation (0.22) suggests that stores with higher numbers might be located in areas with slightly higher unemployment rates.

Very Weak/No Correlations:
There is virtually no correlation between the store number and the holiday flag (0.00), which is expected as they are unrelated variables. Similarly, the holiday flag shows very weak or no correlation with most variables like weekly sales (0.04) and fuel price (-0.08), suggesting that the occurrence of holidays does not significantly impact these factors in a linear way.

Check for Skew

Numerous data analysis techniques rely on the premise that data conform to a normal distribution, while complete adherence to normality is improbable, significant deviations from this distribution pattern warrant attention and in analysis. It's particularly crucial to scrutinize datasets exhibiting skewness, as such deviations can impact the validity of analyses. (Maindonald & Braun, 2010). In the data I can observe less than normal distributions in each of our variables. Weekly sales, our response variable, is positively skewed. The CPI variable is multimodal. Unemployment is slightly skewed positively, and temp appears to be skewed negatively. This would warrant further investigation.

Outlier Detection 

Outliers denote data points that seem disconnected from the main cluster of data. These points, whether stemming from errors or genuine values, possess the potential to skew any model I construct. The identification of an outlier is inherently influenced by the perspective from which the data is examined. At a basic level, this perspective is shaped by whether or not and how the data undergo transformation (Maindonald & Braun, 2010). Boxplots prove valuable in pinpointing outliers along a single dimension The presence of outliers often signals a departure from the assumptions underlying the model (Maindonald & Braun, 2010).



Three of our variables have potential outliers. The first is our response variable Weekly Sales. It is difficult to determine if the high-end points are truly outliers because the sales data is proprietary to Walmart. We do know that retail sales volume is highly seasonal with many days being high above the mean during Thanksgiving and Christmas. Also, different store formats (Walmart vs Walmart Supercenters) could have drastically different sales. For these reasons I do not feel it is necessary to remove any of the observations on account of weekly sales.

The second variable is Temperature with a few low outliers in the low end of the distribution. The lowest of the points is just below zero. We do not find it surprising to have a few average temps below zero as the data is dispersed through the entire year. Although I am not given the geographic area of the store, I can assume that with an average in the 60s that most of the stores are likely in temperate climate areas of the US. We do not feel that removing the observation used to this data feature is necessary.

The third variable is Unemployment. There are outliers on the higher side of this distribution with the average just under 8% and the outliers ranging from 11% to 14%. The years that the dataset spans are 2011-2012 only a few years after the 2008 housing crash. It would be understandable that unemployment rates would still be in the low double digits during this time as a result. Again, the geographic locations of the sores are unknown. Thus, further analysis and comparison to Bureau of Labor Statistics data to our dataset is not practical. We are confident that these ranges are within reason and not due to error. So I will not remove observations due to outliers in this variable.
Check for Normality 

Histograms lack effectiveness in determining whether a distribution conforms reasonably to normality; a more reliable tool for evaluating normality is the normal probability plot, also known as a quantile-quantile plot. (Maindonald & Braun, 2010). This method involves sorting the data values and plotting them against the expected ordered values under the assumption of a normal distribution. If the dataset adheres to a normal distribution, the plot should approximate a straight line, however if some points at the ends stray off the data should still be assumed to be normal (Maindonald & Braun, 2010).




Most of our variables show signs of non-normality. Fuel looks to appx normal. CPI shows bimodal data with a break in the line. Temp, weekly sales, CPI show signs of non-normality with the plot as well. We will address can in two ways. The first is to transform the variables using a log function. After I have transformed, I can use a standard linear model to see results. The second is to use regression methods that are resistant to non-normal data using the original non-log dataset. We can compare the results to find the best fit.

Basic (Vallina) model

The first regression model that was built had no treatments committed to the data. A standard linear model with a step AIC function was used to measure a baseline performance. 


Call:
lm(formula = Weekly_Sales ~ ., data = training)

Residuals:
    Min      1Q  Median      3Q     Max 
-624054  -63704   -3850   46547 1611702 

Coefficients: (1 not defined because of singularities)
               Estimate Std. Error t value Pr(>|t|)    
(Intercept)  26367882.9  4281640.3   6.158 8.29e-10 ***
Store2         414411.3    24001.3  17.266  < 2e-16 ***
Store3       -1190827.8    25952.5 -45.885  < 2e-16 ***
Store4        1061830.0   189268.4   5.610 2.20e-08 ***
Store5       -1268851.8    24895.0 -50.968  < 2e-16 ***
Store6           2640.4    25130.7   0.105 0.916331    
Store7        -769613.0    56833.5 -13.542  < 2e-16 ***
Store8        -705268.8    27094.5 -26.030  < 2e-16 ***
Store9       -1072027.2    27147.8 -39.489  < 2e-16 ***
Store10        941462.4   190801.8   4.934 8.47e-07 ***
Store11       -212540.2    25092.7  -8.470  < 2e-16 ***
Store12        176146.7   199094.9   0.885 0.376367    
Store13        984491.0   189613.2   5.192 2.21e-07 ***
Store14        736081.6    70290.8  10.472  < 2e-16 ***
Store15       -376791.6   176643.2  -2.133 0.032997 *  
Store16       -897820.8    54385.0 -16.509  < 2e-16 ***
Store17       -110211.2   189302.3  -0.582 0.560476    
Store18        110432.2   177857.4   0.621 0.534709    
Store19        457463.7   176623.0   2.590 0.009641 ** 
Store20        584593.7    28267.1  20.681  < 2e-16 ***
Store21       -779850.5    24040.9 -32.438  < 2e-16 ***
Store22         -1514.8   168430.9  -0.009 0.992825    
Store23        297536.0   173853.7   1.711 0.087104 .  
Store24        361620.6   177223.0   2.040 0.041386 *  
Store25       -791328.5    28904.3 -27.378  < 2e-16 ***
Store26         20724.1   176571.3   0.117 0.906575    
Store27        740212.4   168284.4   4.399 1.13e-05 ***
Store28        486708.7   198664.2   2.450 0.014344 *  
Store29       -418808.0   179218.0  -2.337 0.019509 *  
Store30      -1095984.3    24566.7 -44.613  < 2e-16 ***
Store31       -151817.2    23572.3  -6.440 1.37e-10 ***
Store32       -184962.2    55993.7  -3.303 0.000966 ***
Store33       -708952.5   190721.0  -3.717 0.000205 ***
Store34         44106.3   193268.6   0.228 0.819496    
Store35        -83615.1   169470.2  -0.493 0.621771    
Store36      -1163063.9    23691.2 -49.093  < 2e-16 ***
Store37      -1015034.5    24979.5 -40.635  < 2e-16 ***
Store38       -450735.0   198567.6  -2.270 0.023280 *  
Store39        -98057.7    23793.0  -4.121 3.87e-05 ***
Store40       -142823.8   174157.8  -0.820 0.412232    
Store41       -131932.2    54258.6  -2.432 0.015091 *  
Store42       -418124.2   190851.4  -2.191 0.028538 *  
Store43       -780544.0    34571.4 -22.578  < 2e-16 ***
Store44       -706371.7   188796.0  -3.741 0.000186 ***
Store45       -521312.0    69936.5  -7.454 1.17e-13 ***
Date            -1781.7      293.4  -6.072 1.41e-09 ***
Holiday_Flag    -5791.3    10948.3  -0.529 0.596863    
Temperature       978.6      483.7   2.023 0.043116 *  
Fuel_Price     -11329.9    17625.3  -0.643 0.520388    
CPI              6331.7     2161.8   2.929 0.003426 ** 
Unemployment   -29583.9     6169.8  -4.795 1.70e-06 ***
Year2011       622222.7   106778.6   5.827 6.21e-09 ***
Year2012      1246399.2   213591.2   5.835 5.92e-09 ***
Month02        179962.4    16288.8  11.048  < 2e-16 ***
Month03        175419.5    22863.9   7.672 2.24e-14 ***
Month04        245804.6    31130.8   7.896 3.96e-15 ***
Month05        286608.8    39720.4   7.216 6.71e-13 ***
Month06        355974.6    47524.7   7.490 8.90e-14 ***
Month07        379113.9    56441.5   6.717 2.20e-11 ***
Month08        443185.0    64592.5   6.861 8.20e-12 ***
Month09        445100.9    72315.4   6.155 8.47e-10 ***
Month10        516932.9    80284.0   6.439 1.39e-10 ***
Month11        737955.2    89399.1   8.255 2.22e-16 ***
Month12        937597.3    98430.6   9.525  < 2e-16 ***
Week                 NA         NA      NA       NA    
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 141100 on 3114 degrees of freedom
Multiple R-squared:  0.9393,	Adjusted R-squared:  0.9381 
F-statistic: 765.4 on 63 and 3114 DF,  p-value: < 2.2e-16



The coefficients in the model are distributed across both positive and negative ranges. When it comes to the P value of variables, it’s observed that Store 6, 12, 17, 18, 22, 26, 34, 35, and 40 do not hold statistical significance. The same applies to the Holiday Flag and Fuel price. However, the rest of the variables are significant, except for the Week variable which likely has an error due to a high correlation with another variable such as the date of the year. 

Looking at the P value of the model, the results indicate that the model is statistically significant as it has a very low P value. The multiple R square of the model is .9394, which means that our model explains 94% of the variability.We anticipate that the Multiple R2 will increase after additional treatments are applied to the model.
The Step AIC method, which tests all possible subsets of data starting from one regressor and proceeding to all regressors, was used with the goal of minimizing the AIC. This allows for comparison of the AIC to other models. After applying the StepAIC function the variables Holiday Flag and Fuel_price were removed from the model. The coefficients in the model are a mix of positive and negative values. A fair number of variables were found to be statistically significant. Interestingly, despite many of the store number variables not being significant, they were not dropped by the Step function. This is likely due to these variables originating from a single source variable.


Call:
lm(formula = Weekly_Sales ~ Store + Date + Temperature + CPI + 
    Unemployment + Year + Month, data = training)

Residuals:
    Min      1Q  Median      3Q     Max 
-631860  -63723   -4018   46271 1610082 

Coefficients:
               Estimate Std. Error t value Pr(>|t|)    
(Intercept)  26748795.8  4255597.3   6.286 3.72e-10 ***
Store2         414677.5    23993.6  17.283  < 2e-16 ***
Store3       -1191318.2    25930.6 -45.943  < 2e-16 ***
Store4        1074642.8   187907.1   5.719 1.17e-08 ***
Store5       -1269378.1    24869.2 -51.042  < 2e-16 ***
Store6           2250.6    25120.5   0.090 0.928616    
Store7        -765978.4    56579.7 -13.538  < 2e-16 ***
Store8        -706113.5    27051.8 -26.102  < 2e-16 ***
Store9       -1072895.6    27087.9 -39.608  < 2e-16 ***
Store10        951071.6   190000.7   5.006 5.88e-07 ***
Store11       -213259.4    25062.9  -8.509  < 2e-16 ***
Store12        186296.5   198260.3   0.940 0.347467    
Store13        996819.3   188410.5   5.291 1.30e-07 ***
Store14        738665.2    70143.3  10.531  < 2e-16 ***
Store15       -368365.9   176000.1  -2.093 0.036431 *  
Store16       -894794.4    54168.1 -16.519  < 2e-16 ***
Store17        -97742.3   188100.3  -0.520 0.603359    
Store18        120072.9   177004.7   0.678 0.497594    
Store19        466095.9   175967.8   2.649 0.008120 ** 
Store20        583542.2    28172.9  20.713  < 2e-16 ***
Store21       -779591.8    24030.6 -32.442  < 2e-16 ***
Store22          7496.8   167652.7   0.045 0.964336    
Store23        306680.7   173097.9   1.772 0.076539 .  
Store24        370151.3   176572.5   2.096 0.036135 *  
Store25       -792563.1    28798.1 -27.521  < 2e-16 ***
Store26         30344.2   175767.5   0.173 0.862947    
Store27        747666.0   167712.5   4.458 8.56e-06 ***
Store28        496445.4   197867.6   2.509 0.012158 *  
Store29       -408799.5   178329.1  -2.292 0.021950 *  
Store30      -1095833.6    24560.9 -44.617  < 2e-16 ***
Store31       -151785.2    23566.1  -6.441 1.37e-10 ***
Store32       -181489.9    55712.7  -3.258 0.001136 ** 
Store33       -699491.5   189912.5  -3.683 0.000234 ***
Store34         57829.6   191797.0   0.302 0.763042    
Store35        -73827.2   168624.5  -0.438 0.661547    
Store36      -1162438.8    23671.0 -49.108  < 2e-16 ***
Store37      -1014947.5    24972.0 -40.643  < 2e-16 ***
Store38       -440755.8   197763.3  -2.229 0.025905 *  
Store39        -97728.7    23783.1  -4.109 4.07e-05 ***
Store40       -133580.0   173382.9  -0.770 0.441101    
Store41       -129042.4    54033.2  -2.388 0.016990 *  
Store42       -408914.4   190060.7  -2.151 0.031514 *  
Store43       -778844.3    34450.4 -22.608  < 2e-16 ***
Store44       -694214.6   187611.7  -3.700 0.000219 ***
Store45       -518755.2    69786.9  -7.433 1.36e-13 ***
Date            -1811.5      291.1  -6.222 5.55e-10 ***
Temperature       984.2      482.4   2.040 0.041419 *  
CPI              6482.1     2145.5   3.021 0.002538 ** 
Unemployment   -29820.3     6159.7  -4.841 1.35e-06 ***
Year2011       623772.8   106331.9   5.866 4.92e-09 ***
Year2012      1256316.5   212883.9   5.901 3.99e-09 ***
Month02        177507.2    16011.4  11.086  < 2e-16 ***
Month03        172034.4    22014.4   7.815 7.48e-15 ***
Month04        241601.7    30107.0   8.025 1.43e-15 ***
Month05        282666.8    38908.0   7.265 4.69e-13 ***
Month06        354748.9    47307.9   7.499 8.35e-14 ***
Month07        379559.1    56330.1   6.738 1.90e-11 ***
Month08        444016.3    64457.0   6.889 6.79e-12 ***
Month09        445204.3    72255.4   6.162 8.13e-10 ***
Month10        519423.8    80075.9   6.487 1.02e-10 ***
Month11        740099.9    89311.4   8.287  < 2e-16 ***
Month12        941345.8    98264.8   9.580  < 2e-16 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 141100 on 3116 degrees of freedom
Multiple R-squared:  0.9393,	Adjusted R-squared:  0.9381 
F-statistic: 790.8 on 61 and 3116 DF,  p-value: < 2.2e-16

The overall significance of the model is high, as indicated by a P value that is much lower than .05. The multiple R square of the model is a respectable .9394, which means that the model can explain 94% of the variance. However, there was no improvement in the R2 value between our two baselines.
MODEL 2 LOG Transformed Linear Model

This model uses logarithm transformations to address the normality issues that were found earlier. We also include custom multiplicative features to discover any combined effects of variables.

When examining proportional changes, logarithms of measurements become useful. Statisticians employ transformations to make data distributions more symmetrical and closer to normal, and to streamline the analysis if a single transformation can resolve several issues. A log transformation might normalize data and remove or introduce interactions. It can also reduce skewness but may increase variability. (Maindonald & Braun, 2010).

We devised two bespoke features for our analysis, each presented in both additive and multiplicative formulations. The initial feature amalgamates Consumer Price Index (CPI) and unemployment rate, both of which serve as pivotal economic indicators signifying the economic prosperity of a nation, thus constituting an inherently correlated pair. The subsequent feature pairs fuel prices with temperature, a relationship rooted in the phenomenon where escalating temperatures tend to correspond with heightened fuel prices owing to amplified demand.



Upon checking the effects of the log transformation I did not  visually find a significant impact on the normality of the data from the Q-Q plots. As a result the performance of the model may suffer.


The model has strong coefficients similar to the base model, with some store coefficients influencing weekly sales by over $1 million. The Holiday flag and Week variables don’t show statistical significance. Interestingly, none of the LOG transformed features, including the two custom ones, show any significance. The Log of CPI shows slight statistical significance at the 0.01 level. The Log model, like the baseline model, holds a high degree of significance. The R square value remains the same as the baseline model, approximately 94%. The AIC is 84436.9. The next step is to optimize the AIC with step AIC to see if performance can be improved.
In this case, the Step AIC function eliminated `Holiday_Flag`, `Week`, `preholiday`, and `fuel` from the data, but retained a majority of the features. The `Multiple R squared` value remained virtually unchanged. Interestingly, the AIC of the optimized model is **92487.32**, which is virtually identical to the AIC of the non-AIC optimized Log model. This suggests that the optimization did not significantly change the model's performance. The next steps could involve exploring other optimization techniques or reconsidering the feature selection.


Call:
lm(formula = Weekly_Sales ~ Store + Date + Temperature + Year + 
    Month + Log_CPI + Log_CPI_Unemployment_Mult, data = training_LOG)

Residuals:
    Min      1Q  Median      3Q     Max 
-633336  -63436   -4643   47209 1613154 

Coefficients:
                            Estimate Std. Error t value Pr(>|t|)    
(Intercept)               20636236.8  5182689.6   3.982 7.00e-05 ***
Store2                      414835.7    23967.4  17.308  < 2e-16 ***
Store3                    -1196574.8    26650.2 -44.899  < 2e-16 ***
Store4                     1211886.8   330115.8   3.671 0.000246 ***
Store5                    -1288478.6    25321.5 -50.885  < 2e-16 ***
Store6                      -12319.6    25484.1  -0.483 0.628830    
Store7                     -748592.0    75121.1  -9.965  < 2e-16 ***
Store8                     -729730.8    28380.4 -25.712  < 2e-16 ***
Store9                    -1096766.2    28479.9 -38.510  < 2e-16 ***
Store10                    1121192.1   330869.5   3.389 0.000711 ***
Store11                    -219421.1    25830.8  -8.495  < 2e-16 ***
Store12                     340716.0   333512.7   1.022 0.307050    
Store13                    1157496.0   329969.5   3.508 0.000458 ***
Store14                     762765.4    98410.2   7.751 1.23e-14 ***
Store15                    -225073.1   299765.0  -0.751 0.452811    
Store16                    -899214.4    73963.8 -12.157  < 2e-16 ***
Store17                      59866.5   329791.1   0.182 0.855964    
Store18                     265563.4   299877.5   0.886 0.375916    
Store19                     609449.4   299663.5   2.034 0.042058 *  
Store20                     582880.0    31608.6  18.441  < 2e-16 ***
Store21                    -780163.5    24001.6 -32.505  < 2e-16 ***
Store22                     135895.6   281605.7   0.483 0.629432    
Store23                     400047.4   298399.9   1.341 0.180135    
Store24                     515299.0   299940.6   1.718 0.085895 .  
Store25                    -792161.9    32165.0 -24.628  < 2e-16 ***
Store26                     172706.4   299297.3   0.577 0.563954    
Store27                     875918.1   281711.4   3.109 0.001892 ** 
Store28                     650192.8   332914.6   1.953 0.050905 .  
Store29                    -262805.3   300382.2  -0.875 0.381694    
Store30                   -1095898.1    24531.7 -44.673  < 2e-16 ***
Store31                    -151778.4    23536.5  -6.449 1.30e-10 ***
Store32                    -164078.4    74485.2  -2.203 0.027679 *  
Store33                    -529011.3   330701.1  -1.600 0.109774    
Store34                     230476.3   331363.2   0.696 0.486769    
Store35                      57145.7   281862.7   0.203 0.839349    
Store36                   -1160685.7    23758.5 -48.853  < 2e-16 ***
Store37                   -1012446.1    25083.3 -40.363  < 2e-16 ***
Store38                    -288121.7   332817.8  -0.866 0.386719    
Store39                     -96068.7    23864.4  -4.026 5.82e-05 ***
Store40                     -39411.6   298693.2  -0.132 0.895035    
Store41                    -126229.7    73823.0  -1.710 0.087384 .  
Store42                    -238673.8   331017.5  -0.721 0.470945    
Store43                    -764889.7    37656.5 -20.312  < 2e-16 ***
Store44                    -534173.9   329231.2  -1.622 0.104800    
Store45                    -493465.4    97825.0  -5.044 4.81e-07 ***
Date                         -1832.7      291.5  -6.287 3.70e-10 ***
Temperature                   1004.8      481.8   2.085 0.037124 *  
Year2011                    621414.4   106142.4   5.855 5.28e-09 ***
Year2012                   1249102.6   212508.3   5.878 4.59e-09 ***
Month02                     176847.9    16144.2  10.954  < 2e-16 ***
Month03                     170225.5    22142.4   7.688 1.99e-14 ***
Month04                     238470.4    30172.2   7.904 3.73e-15 ***
Month05                     280443.8    38895.3   7.210 6.98e-13 ***
Month06                     352369.2    47239.0   7.459 1.12e-13 ***
Month07                     375940.2    56239.4   6.685 2.73e-11 ***
Month08                     441525.9    64334.4   6.863 8.10e-12 ***
Month09                     442657.4    72125.2   6.137 9.45e-10 ***
Month10                     516168.3    79928.8   6.458 1.23e-10 ***
Month11                     737988.6    89156.0   8.277  < 2e-16 ***
Month12                     939856.2    98085.6   9.582  < 2e-16 ***
Log_CPI                    1531818.4   637537.1   2.403 0.016332 *  
Log_CPI_Unemployment_Mult   -57183.9     9349.2  -6.116 1.08e-09 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 140800 on 3116 degrees of freedom
Multiple R-squared:  0.9396,	Adjusted R-squared:  0.9384 
F-statistic: 794.1 on 61 and 3116 DF,  p-value: < 2.2e-16



LOG Transformed Model Assessment 

The visualizations show the original log sales without treatment and the predictions based on log treated variables. Further evidence that the Log treatment did successfully normalize the data but at a cost of struggling to predict more extreme values.

When an outlier appears to be a legitimate data point, conducting the analysis with and without this outlier is considered best practice. Should the inclusion of a suspected outlier not significantly alter the practical application and interpretation of the results, it's generally advisable to keep it in the primary analysis (Maindonald & Braun, 2010). We know that the sales data is valid for the data points that are skewing the distribution (1906, 1334, 1958). We will explore the model without these data points.


The Variance Inflation Factor (VIF) assesses multicollinearity in linear regression models by detecting correlations among independent variables. Multicollinearity, where these variables are interrelated, can lead to unreliable estimates of regression coefficients, complicating the assessment of each variable's individual impact.

                            GVIF       Df      GVIF^(1/(2*Df))
Store                     223062.34128 44        1.150211
Date                        1142.36463  1       33.798885
Temperature                   12.73987  1        3.569296
Year                        1266.27787  2        5.965300
Month                       1414.70330 11        1.390631
Log_CPI                     3547.20291  1       59.558399
Log_CPI_Unemployment_Mult     17.15713  1        4.142117


Raw GVIF is high in the Store variable, but adjusting for its 44 levels yields a GVIF^(1/(2*Df)) of 1.150211, indicating no significant multicollinearity. Date, however, shows a persistently high GVIF even after adjusting for degrees of freedom, at 33.798885, suggesting it's a likely cause of multicollinearity. 

Temperature's GVIF^(1/(2*Df)) of 3.569296 is below the threshold of concern, indicating no significant issue. Similarly, 

Year's adjusted VIF of 5.965300 falls below the 10 threshold. Month's GVIF^(1/(2*Df)) of 1.390631 also suggests no significant multicollinearity. 

Conversely, Log_CPI displays a very high GVIF^(1/(2*Df)) of 59.558399, indicating severe multicollinearity. Finally, the Log_CPI_Unemployment_Mult product term has a GVIF^(1/(2*Df)) of 4.142117, below the 10 threshold, indicating no significant multicollinearity problem.

Plotting the residuals predicted values against actuals can show if the model adhered to the normality assumptions required for linear models. The red line shows what would be the perfect relationship between the predictions and actuals. The further the two disperse from the line the less predictive power the model shows. Here I can observe a great deal of dispersion toward the high end of weekly sales where the model had a difficult time making predictions. For the most part however the model points are close to linear and performance appears solid. 


MODEL 3- Log Transformed with No Outliers

In our final regression model, I will exclude data points identified with the highest leverage on Cook's distance, specifically the three outliers numbered 1906, 1334, and 1958. Additionally, I will omit features with VIF scores exceeding 10, such as LOG_CPI and Date. 


Call:
lm(formula = Weekly_Sales ~ Store + Holiday_Flag + Month + Week + 
    LOG_Temperature + LOG_CPI_Unemployment_Mult + LOG_Fuel_Price_Temp_Mult, 
    data = training_LOG_NO_OUTLIERS)

Residuals:
    Min      1Q  Median      3Q     Max 
-633177  -61827   -4272   44201 1415726 

Coefficients:
                          Estimate   Std. Error  t value  Pr(>|t|)    
(Intercept)                1857443.6   100833.8  18.421  < 2e-16 ***
Store2                      411691.5    24276.2  16.959  < 2e-16 ***
Store3                    -1171073.0    25069.4 -46.713  < 2e-16 ***
Store4                      410725.9    30625.4  13.411  < 2e-16 ***
Store5                    -1284091.3    24812.2 -51.752  < 2e-16 ***
Store6                       -1975.3    24941.4  -0.079 0.936880    
Store7                     -924030.3    26189.5 -35.282  < 2e-16 ***
Store8                     -710487.9    25765.6 -27.575  < 2e-16 ***
Store9                    -1072429.8    25637.4 -41.831  < 2e-16 ***
Store10                     330230.8    24990.1  13.214  < 2e-16 ***
Store11                    -225619.9    24271.6  -9.296  < 2e-16 ***
Store12                    -436514.8    27544.9 -15.847  < 2e-16 ***
Store13                     386561.5    26516.7  14.578  < 2e-16 ***
Store14                     499148.7    24936.8  20.017  < 2e-16 ***
Store15                    -958602.6    25077.9 -38.225  < 2e-16 ***
Store16                   -1070713.4    27471.1 -38.976  < 2e-16 ***
Store17                    -735542.3    29103.4 -25.273  < 2e-16 ***
Store18                    -463956.0    24665.7 -18.810  < 2e-16 ***
Store19                    -122379.8    25508.2  -4.798 1.68e-06 ***
Store20                     580563.8    24146.9  24.043  < 2e-16 ***
Store21                    -792113.1    24189.5 -32.746  < 2e-16 ***
Store22                    -557804.1    24658.3 -22.621  < 2e-16 ***
Store23                    -324088.1    35053.3  -9.246  < 2e-16 ***
Store24                    -203975.3    24502.8  -8.325  < 2e-16 ***
Store25                    -836094.0    24949.5 -33.511  < 2e-16 ***
Store26                    -577652.6    26304.9 -21.960  < 2e-16 ***
Store27                     189085.8    24943.4   7.581 4.51e-14 ***
Store28                    -102231.8    27550.8  -3.711 0.000210 ***
Store29                    -975787.7    24027.6 -40.611  < 2e-16 ***
Store30                   -1099607.8    25080.6 -43.843  < 2e-16 ***
Store31                    -142572.5    23710.5  -6.013 2.03e-09 ***
Store32                    -341503.2    25758.6 -13.258  < 2e-16 ***
Store33                   -1308668.7    23962.2 -54.614  < 2e-16 ***
Store34                    -568896.6    24309.1 -23.403  < 2e-16 ***
Store35                    -638761.9    24779.7 -25.778  < 2e-16 ***
Store36                   -1169808.6    23620.5 -49.525  < 2e-16 ***
Store37                   -1026600.5    24992.7 -41.076  < 2e-16 ***
Store38                   -1085000.6    28032.4 -38.705  < 2e-16 ***
Store39                     -90924.2    23781.4  -3.823 0.000134 ***
Store40                    -758435.9    35380.5 -21.437  < 2e-16 ***
Store41                    -313263.1    26098.6 -12.003  < 2e-16 ***
Store42                   -1027199.4    24219.8 -42.412  < 2e-16 ***
Store43                    -819837.1    26195.0 -31.297  < 2e-16 ***
Store44                   -1335068.7    27558.8 -48.444  < 2e-16 ***
Store45                    -734483.8    24986.9 -29.395  < 2e-16 ***
Holiday_Flag                 22420.7    10770.8   2.082 0.037458 *  
Month02                     178862.0    15922.2  11.234  < 2e-16 ***
Month03                     172617.6    22023.5   7.838 6.24e-15 ***
Month04                     222570.8    29710.8   7.491 8.84e-14 ***
Month05                     263748.6    38189.4   6.906 6.00e-12 ***
Month06                     328304.6    46495.4   7.061 2.03e-12 ***
Month07                     339403.6    54878.9   6.185 7.04e-10 ***
Month08                     393245.9    63864.2   6.158 8.33e-10 ***
Month09                     376314.3    72093.5   5.220 1.91e-07 ***
Month10                     427970.8    80647.4   5.307 1.19e-07 ***
Month11                     631791.0    89618.5   7.050 2.20e-12 ***
Month12                     821612.2    99258.5   8.278  < 2e-16 ***
Week                         -9337.1     2068.5  -4.514 6.60e-06 ***
LOG_Temperature              63887.6    21755.4   2.937 0.003342 ** 
LOG_CPI_Unemployment_Mult   -58035.3     7461.0  -7.778 9.91e-15 ***
LOG_Fuel_Price_Temp_Mult      -588.8      308.9  -1.906 0.056680 .  
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 142900 on 3114 degrees of freedom
Multiple R-squared:  0.9384,	Adjusted R-squared:  0.9372 
F-statistic: 790.6 on 60 and 3114 DF,  p-value: < 2.2e-16



LOG Transformed No Outlier Assessment 

The removal of outliers does not seem to significantly impact the outcome. The "No Outlier Log" model achieved an R2 of 0.9384, similar to the R2 of 0.9385 obtained with the full LOG model.  Among our LOG features, LOG_CPI, LOG_TEMPERATURE, and our custom feature, LOG_CPI_Unemployment_Mult, were found to be statistically significant. This represents a notable shift from the previous log model.

                           GVIF      Df      GVIF^(1/(2*Df))
Store                      34.254124 44        1.040974
Holiday_Flag                1.255415  1        1.120453
Month                     899.946840 11        1.362331
Week                      132.834950  1       11.525405
LOG_Temperature             9.999781  1        3.162243
LOG_CPI_Unemployment_Mult  10.541188  1        3.246720
LOG_Fuel_Price_Temp_Mult    9.135712  1        3.022534

The VIF scores have notably improved, with only the Week feature slightly exceeding a VIF of 10. Some variables have relatively low levels of multicollinearity Store and Holiday_Flag. Month, LOG_Temperature, LOG_CPI_Unemployment_Mul, LOG_Fuel_Price_Temp_Mult  have moderate levels of multicollinearity, while Week is the only variable displaying high levels.


The standardized residuals in the scale-location reduced from 3.5 to 3.0 showing a compression of errors when outliers were removed. New outliers arose to take the place of the data points that were removed. Q-Q residuals also show the outliers are below 10 versus above10 with the previous outliers.The highest leverage point also went from .03 to .06 with the no outlier model.   

Model Comparison

Most stores show statistical significance in their coefficients across all models, with the exception of Store6 and Store12. The coefficients for each store vary across the models, indicating different effects on the dependent variable, Weekly_Sales. It’s important to consider these differences when interpreting the results of the models.

In terms of model fit, all models have a high R2 value, indicating that they explain a large proportion of the variance in the dependent variable. The R2 values range from 0.938 to 0.940. The adjusted R2 values, which account for the number of predictors in the model, are also high and range from 0.937 to 0.938. The R2 values for all three models are approximately 0.939 to 0.940, indicating that about 93.9% to 94% of the variance in Weekly_Sales is explained by the models.

F-statistic: Highly significant (p < 0.01) for all models, suggesting the models are statistically significant as a whole.















Arima Vs Regression

Model
RMSE
MAE
R-squared
AIC
Notes
Vanilla Model
144,079.2
85,816.16
0.9342
84,444.68


No Outliers Model
133,481.9
83,740.64
0.9422
84,432.21
Best among regression models
Full Log Model
143,654.2
85,411.53
0.9346
84,444.47


ARIMA Model
131,693.9
113,664.1
N/A
2,589.854
Not directly comparable (AIC)



The No Outliers Model has the lowest RMSE and MAE among the regression models, suggesting it has the best forecasting accuracy for handling data without extreme values which might skew the results.The No Outliers Model also has the highest R-squared value, indicating it explains a higher percentage of the variance in sales compared to other regression models.

The ARIMA model's Avg_RMSE of 131693.9 is competitive with the best regression model (No Outliers Model), but its Avg_MAE is higher. This indicates that while ARIMA might be quite predictive, it may not be as reliable in some error metrics compared to the best regression model. 

Despite the AIC being the lowest in the No Outliers Model among regression approaches, it is crucial to note that AIC values are not directly comparable between ARIMA and regression models due to differences in how these models are built and their underlying assumptions.

If predictive accuracy is paramount, especially in terms of minimizing error metrics like RMSE and MAE, the No Outliers Regression Model appears to be the most effective among the regression models. However, ARIMA performs comparably in RMSE and could be preferable if you're focusing on capturing time-series dynamics that regression models are not addressing.

Conclusion

The project delves into sales forecasting within the retail sector, focusing specifically on Walmart's extensive dataset encompassing sales data from 45 store locations over a three-year span (2010-2012) and incorporating economic indicators like CPI and unemployment rates. Through hypothesis testing using a Welch Two Sample t-test, the study revealed significant sales discrepancies between holiday and non-holiday weeks, emphasizing the seasonal influence on sales performance. Time series analysis employing ARIMA models aimed to discern seasonal patterns and make forward-looking sales predictions, demonstrating varying levels of accuracy across different store locations. Furthermore, our study employed multiple regression models, including standard linear and log-transformed variants, to forecast sales while addressing issues like outliers, multicollinearity and non-normality. 

The most effective regression model, “Log Transformed No Outliers”, exhibited robust accuracy with low RMSE and MAE, outperforming specific metrics of the ARIMA model. This comparison underscores the nuanced trade-offs between time series and regression methodologies in forecasting Walmart's sales dynamics, with regression models proving advantageous in certain predictive aspects. Comparing model performance, the “No Outliers” Regression Model emerged as the most accurate among regression models, showcasing minimal RMSE and MAE alongside a high R-squared value elucidating sales variance. Conversely, the ARIMA model exhibited competitive RMSE but higher MAE, implying potential disparities in error metric reliability compared to regression approaches. Notably, AIC values were highlighted as non-comparable between ARIMA and regression models due to distinct model architectures and assumptions. 

In summary, thestudy navigates the intricate landscape of retail sales forecasting, highlighting Walmart's Kaggle dataset as a lens into the industry's dynamics. Noteworthy findings include the discernible impact of seasonal factors on sales, evidenced by significant variations between holiday and non-holiday weeks. With the culmination underscoring the utility of comparing time series to regression models, particularly the “No Outliers” Regression Model, in achieving superior forecasting precision compared to ARIMA in specific performance metrics, shedding light on strategic considerations for sales forecasting within the retail domain.













Sources

Data:
Mikhail. (2024, February 13). Walmart sales. Kaggle. https://www.kaggle.com/datasets/mikhail1681/walmart-sales 
Arima Model:
Hyndman, R., & Athanasopoulos, G. (n.d.). Forecasting: Principles and practice (2nd ed). 8.7 ARIMA modelling in R. https://otexts.com/fpp2/arima-r.html 
Khan, R. (n.d.). ARIMA model for forecasting– Example in RARIMA model for forecasting– Example in R. RPubs. https://rpubs.com/riazakhan94/arima_with_example 
Regression:
Maindonald, J., & Braun, W. J. (2010). Data Analysis and Graphics Using R: An Example-Based Approach (3rd ed.). Cambridge University Press.

