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

# Identify Outliers
