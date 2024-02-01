# Bike-Rental-Prediction
Bike Rental Prediction


# Step 1: Load the  Relevant Libraries

First, we'll load the necessary R libraries and the dataset. For this analysis, we'll need readxl to read the Excel file, dplyr for data manipulation, ggplot2 for data visualization, and randomForest for building the predictive model.

    

# Load necessary libraries
library(readxl)

library(dplyr)

library(ggplot2)

library(randomForest)


# Load the dataset
data <- read_excel("/path/to/your/file/1657875746_day.xlsx")

Make sure to replace "/path/to/your/file/1657875746_day.xlsx" with the actual path where you've saved the dataset.

# Step 2: Exploratory Data Analysis (EDA)
# Data Type Conversion

Check the structure of the dataset using str(data) and convert the data types if needed. For instance, converting dteday to a Date type and categorical variables to factors.


data$dteday <- as.Date(data$dteday)

data$season <- as.factor(data$season)

data$yr <- as.factor(data$yr)

data$mnth <- as.factor(data$mnth)

data$holiday <- as.factor(data$holiday)

data$weekday <- as.factor(data$weekday)

data$workingday <- as.factor(data$workingday)

data$weathersit <- as.factor(data$weathersit)


# Missing Value Analysis

Check for missing values in the dataset.


sum(is.na(data))

#Step 3: Attributes Distribution and Trends

# Monthly Distribution of Total Bikes Rented

ggplot(data, aes(x = mnth, y = cnt)) +

  geom_bar(stat = "identity", fill = "steelblue") +
	
  labs(x = "Month", y = "Total Bikes Rented", title = "Monthly Distribution of Total Bikes Rented")

  ![image](https://github.com/Shruchika17/Bike-Rental-Prediction/assets/88970372/976eb1d3-bbfe-479f-aa26-03052bd57a43)



# Yearly Distribution of Total Bikes Rented

ggplot(data, aes(x = yr, y = cnt)) +

  geom_bar(stat = "identity", fill = "coral") +
	
  labs(x = "Year", y = "Total Bikes Rented", title = "Yearly Distribution of Total Bikes Rented")
	
![image](https://github.com/Shruchika17/Bike-Rental-Prediction/assets/88970372/8a8f4012-43e4-4d32-b191-7bc62362528a)


# Boxplot for Outliers Analysis

ggplot(data, aes(y = temp)) + geom_boxplot() + ggtitle("Boxplot for Temperature")

 Repeat for other continuous variables like atemp, hum, and windspeed

![image](https://github.com/Shruchika17/Bike-Rental-Prediction/assets/88970372/a6af8404-1fb8-428a-b70f-a5f3179f5de3)

 
# Step 4: Split the Dataset into Train and Test Dataset

set.seed(123) # Ensure reproducibility

trainIndex <- sample(1:nrow(data), 0.8 * nrow(data))

trainData <- data[trainIndex, ]

testData <- data[-trainIndex, ]


![image](https://github.com/Shruchika17/Bike-Rental-Prediction/assets/88970372/ddc60c85-4b48-42e0-a01b-c4f44058f9ad)


# Step 5: Create a Model Using the Random Forest Algorithm


model <- randomForest(cnt ~ . -instant -dteday, data = trainData)

# Step 6: Predict the Performance of the Model on the Test Dataset

predictions <- predict(model, testData)

predictions <- predict(model, testData)

performance <- postResample(predictions, testData$cnt)

print(performance)

![image](https://github.com/Shruchika17/Bike-Rental-Prediction/assets/88970372/d82d25d7-ced7-45c6-a756-9e6cda0cab0d)

To evaluate the model, you could calculate metrics such as Mean Squared Error (MSE), Root Mean Squared Error (RMSE), or Mean Absolute Error (MAE). These metrics provide insight into the model's accuracy.

actual <- testData$cnt

mse <- mean((predictions - actual)^2)

rmse <- sqrt(mse)

![image](https://github.com/Shruchika17/Bike-Rental-Prediction/assets/88970372/e3963063-1b55-4ef8-a4fe-2d68101b5b29)


#Project Outcome
By following these steps, you will load the dataset, perform EDA to understand the data's characteristics, visualize the distribution of bike rentals, prepare the data, build a random forest model, and evaluate its performance. This process will equip you with insights into factors affecting bike rentals and allow you to predict future rentals accurately.

Remember, the effectiveness of your model might depend on various factors, including the quality of the data, the selection of variables included in the model, and how well the model's assumptions fit the data. Continuous refinement and validation against new data are key to maintaining the model's accuracy over time.
