Intro:

The dataset contains 29,731 rows and 14 columns of real historical data from Ryanair. The goal is to predict the aircraft's takeoff weight, which is an important factor for estimating operational parameters such as fuel consumption and pricing. Note that the data is somewhat dated, which may impact certain estimations, but it still provides valuable insights for modeling and analysis.

The dataset has been uploaded to this repository along with all the necessary libraries and dependencies required to run the analysis and modeling.

Data Exploration
The dataset was explored using pandas methods info() and describe() to understand its structure, data types, and basic statistics.

Visualizations were created to examine the distributions of key features, providing deeper insights and aiding in understanding patterns within the dataset.

Data Cleaning
Handling Missing and Irrelevant Data:
Some columns in the dataset contained missing values, while others were deemed irrelevant for this level of analysis. Specifically, columns such as 'DepartureDate', 'DepartureYear', 'DepartureMonth', and 'FlightNumber' were excluded, as they do not add significant value for the current modeling task. Instead, the 'DepartureDay' column is complete and can be used to reconstruct the relevant date information.

The ActualTOW column contains the aircraft’s actual takeoff weight, but some entries may be missing or incorrectly formatted.
All values in ActualTOW are converted to numeric types, with non-numeric entries replaced by NaN.
The mean takeoff weight is calculated from the available numeric values.
Missing values are then replaced with this mean, ensuring the column is complete and ready for modeling.

Most ActualTOW values are tightly clustered, so using the mean for imputation is reasonable. For added robustness, the median could also be used, as it would be slightly more resistant to the few lower-value points.

Distribution of Actual Takeoff Weight (ActualTOW)
The histogram for ActualTOW shows a slightly right-skewed distribution, indicating that a small number of flights have lower takeoff weights (~45,000–55,000), which occur less frequently.

The BagsCount and FlightBagsWeight columns are related, as the total baggage weight naturally depends on the number of bags. Instead of treating these as independent features, the information from one can help reconstruct the other if needed. This simplifies feature handling and reduces redundancy while preserving the underlying data patterns.

The dataset only provides the day of departure in the DepartureDay column, without month or year.
Each day value is converted to a string in DD.MM.YYYY format.
Single-digit days are padded with a leading zero (e.g., 1 → 01).
The month and year are fixed as October 2016.

Creating Day-of-Week Features

The dataset initially contains only the day of departure.
DepartureDay is converted to a datetime object, making it easier to extract date-related information.

DayOfWeek is created using .dt.day_name(), giving the name of the day (e.g., Monday, Tuesday).

Two binary features are derived:

Weekend: True if the day is Friday, Saturday, or Sunday.

WeekDay: True if the day is Monday through Thursday.

The original DepartureDay and DayOfWeek columns are dropped to avoid redundancy.

Both Weekend and WeekDay are converted to numeric 0/1 values, which are easier to use in modeling.

Handling Missing Passenger Data
Removes rows where FLownPassengers is missing, ensuring only complete and reliable data is used.

Visualizing Actual Takeoff Weight vs. Baggage Weight
This visualization helps identify trends or correlations between takeoff weight and baggage load, and whether weekend flights behave differently. and the answer is yes.

Dropping Redundant Airport Columns: Dropping them reduces redundancy and keeps the dataset clean for modeling.

After data cleaning and feature engineering, the following features are used for modeling:

ActualFlightTime	The real duration of the flight in minutes.
ActualTotalFuel	The total fuel consumed during the flight.
ActualTOW	Aircraft’s actual takeoff weight (imputed for missing values).
FLownPassengers	Number of passengers on the flight (rows with missing values dropped).
FlightBagsWeight	Total weight of passenger baggage.
Weekend	Binary indicator (1 if flight is on Friday–Sunday, 0 otherwise).
WeekDay	Binary indicator (1 if flight is on Monday–Thursday, 0 otherwise).

Before training the models, the dataset is split into training and testing sets, and both features and target
Scaling ensures that models sensitive to feature magnitudes (e.g., regression, gradient-based models) perform optimally.

Model Performance Summary

1. Linear Regression

Prediction Sample: 64,908.11

RMSE: 1030.97

MAE: 763.15

R²: 1.5883

2. Neural Network

RMSE: 936.49

MAE: 665.39

3. Decision Tree Regressor

RMSE: 1348.40

MAE: 977.49

4. Random Forest Regressor

RMSE: 988.22

MAE: 726.98

Conclusion

The Neural Network achieved the lowest RMSE overall (936.49), making it the most accurate model for predicting ActualTOW.

The Random Forest performed better than the Decision Tree and Linear Regression, but worse than the Neural Network.

Linear Regression performed reasonably but was outperformed by both the Neural Network and Random Forest.

Decision Tree had the weakest performance due to overfitting and lack of generalization.

Validation

After cleaning and preparing the validation dataset, the final model was used to generate predictions for ActualTOW.
