# Project Idea/Goal

The idea I have for my project involves analyzing and creating a model regarding behavior and usage of electric vehicle charging stations. The business problem I intend to solve is being able to predict the best characteristics and locations for charging stations in order to maximize profit and use of each charging station. A company looking to install electric vehicle charging stations would be able to use this model in order to know what station characteristics like platform (android, iOS, etc.), fee, currency, etc. would be best and where certain characteristics perform better.

The major questions that would need to be answered are how factors like distance from a user’s home to station, fee, station type, platform used, and charge time affect things like total cost and total energy used per transaction. We want to know which of these characteristics and other ones like them result in the highest sale amounts.

# The Data

I pieced together a couple of different datasets. One is a dataset that takes activity of several electric vehicle drivers across over one hundred charging stations of different types. The other is a dataset that observes user behavior on a single college campus. The goal of using the different datasets is to gauge if there is a difference in behavior when distance isn’t a factor (students are already on campus with charging stations in one scenario), as well as piece together variables that aren’t in both datasets. By comparing models from both I can conclude which model best meets the target of predicting max sales.

<img width="485" alt="Screenshot 2024-09-22 at 12 57 42 PM" src="https://github.com/user-attachments/assets/a15c8e6e-8e7f-4756-8775-7763e9b7fd49">

What we can gather from this graph is that there a loose linear correlation between that gasoline savings provided by the charging session and the fee charged to the user. This means including the savings amount for for the user would be important to explore and include in any model wanting to figure out how to maximize profits through sales/fees.

<img width="508" alt="Screenshot 2024-09-22 at 12 57 48 PM" src="https://github.com/user-attachments/assets/a5e4bb2e-a5d3-4b92-9f49-05414ec4a8a4">

The histogram shows us that the distribution of the energy used is roughly bell-shaped meaning most of the transactions that took place are in the 0 - 20 kWh range. However, the data is right-skewed meaning the long tail is on the right side of the distribution. This occurs because there can be no transactions that are less than zero, but there are a few large numbers that skew the data to the right which will cause an overestimation in the mean. This means I may have to remove some of the extremely large outliers in order to get a more accurate model.

<img width="506" alt="Screenshot 2024-09-22 at 12 57 54 PM" src="https://github.com/user-attachments/assets/c16172dd-4a1e-42e5-b1f0-381ec36beeb3">

The histogram shows us that the distribution of the charge times is also roughly bell-shaped meaning most of the transactions that took place are in the 0 - 6 hour range. This data is also right-skewed. This occurs because there can be no transaction that takes negative time, but there are a few large numbers that skew the data to the right which will cause an overestimation in the mean. However, overall I believe this distribution combined with other factors will help accurately train the model, since the skew is not as far right as the previous histogram.

<img width="490" alt="Screenshot 2024-09-22 at 12 59 45 PM" src="https://github.com/user-attachments/assets/fee051a5-8f82-43a7-a9fc-5548139a9f17">

My initial interpretation of the scatter is that there is little to no correlation between how far the charging station is from the user, and how much the user ends up spending. A few of the largest sales do take place at short distances, but there is still very little correlation. This will be helpful to know later on when considering whether to include distance as a variable in the model or not. If indeed distance plays no role, the company installing these stations will not have to consider placement too much.

# Thought process on model selection
The goal of my model is to determine what factors of electric vehicle charging stations lead to to the highest amount of energy usage (most use from station). Given this approach, the kwhTotal is my target variable, and the others are the determining.

Since the kWh is the target and it is numerical, not categorical I am going to use regression algorithms for my model. As identified earlier in my exploratory data analysis, there is a linear relationship between some variables, but not all. Therefore, I will consider a linear regression model, and a random forest regressor and comparing the results to see which yiedls a better result. I will see which one yields a better result by comparing the values for R2, root mean squared error (RMSE), and mean absolute error (MAE). For each model I will compare these values on the training and test set to make sure there is no major gap that would indicate overfitting.

# Random Forest Regressor Analysis

The R2 for the test and train set are both .99. Given both values are in close range I can assume overfitting isn't a major issue. The RMSE and MAE values are also very small (~.25 & ~.2 for the test set) meaning, when the model did make an incorrect prediction, the magnitude of the error was small. Similarly we do see smaller RMSE and MAE values for the train set which is expected since the model should perform better on the data it was trained with.

# Linear Regression Analysis

The R2 value for the test and train set are both .98. Given both values are in close range I can assume overfitting isn't a major issue for this model either. The RMSE and MAE values are also very small (~.07 & ~.2 for the test set). This is interesting because while the R2 value is slightly smaller, the RMSE and MAE values are smaller as well. This could mean that there is some overfitting in the Random Forest Regressor, because the Linear Regression model, when incorrect, had a smaller magnitude of error. This could mean that the Linear Regression Model may perform better at scale. Given this analysis I think it would be best to use a pipeline with a grid search to find the best model/parameters.

# Analysis After Pipeline and Grid Search

Overall I am satisfied with the results, with the R2 value being .98 for the test set. Given my suspicions that the original Random Forest Regressor was possibly over-fit (.99 R2 value), I feel more confident in the new model at scale. Additionally with the new model the RMSE and MAE values are still relatively small (.29 and .2), meaning there was not much of an increase in error magnitude.


# Feature Performance

<img width="617" alt="Screenshot 2024-09-22 at 1 02 45 PM" src="https://github.com/user-attachments/assets/ca6fb9e3-9321-4245-9152-4d121b80a1e2">

<img width="538" alt="Screenshot 2024-09-22 at 1 02 48 PM" src="https://github.com/user-attachments/assets/b894d72b-2636-47ec-968f-684e1e386d0a">

While there is a positive correlation with charge time and kWh, which would seem obvious given the more time spent charging the more energy used, we do actually see most of the highest energy usage take place below the middle value (4 hours). This would indicate most customers mat prefer to use stations that charge at a faster rate.
