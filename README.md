# ✈️ Ryanair Takeoff Weight Prediction: Machine Learning Approach

## 🎯 Introduction
This project focuses on predicting an aircraft's **Actual Takeoff Weight (ActualTOW)** using historical flight data from Ryanair. Takeoff weight is a critical operational parameter, influencing factors like fuel consumption estimation and flight pricing.

The dataset, which is based on real historical Ryanair flight logs, contains **29,731 rows** and **14 initial columns**. While the data is somewhat dated, it provides valuable insights for developing and comparing machine learning models.

The complete dataset, along with all necessary libraries and dependencies, is available within this repository.

---

## 🔬 Data Exploration and Cleaning

The initial dataset was thoroughly explored using standard `pandas` methods (`info()`, `describe()`) and through various visualizations to understand feature distributions and patterns.

### Data Cleaning and Feature Engineering Highlights

* **Handling Missing/Irrelevant Data:**
    * Irrelevant date and flight identifier columns (`DepartureDate`, `DepartureYear`, `DepartureMonth`, `FlightNumber`) were excluded.
    * Rows with missing **FLownPassengers** were removed to ensure data reliability.
    * Redundant airport columns were dropped to simplify the feature set.
* **Target Variable Imputation (ActualTOW):**
    * The target column, **ActualTOW**, was converted to a numeric type, with non-numeric entries replaced by `NaN`.
    * Missing values were imputed using the **mean** of the available values. This was deemed reasonable as the **ActualTOW** distribution is tightly clustered.
    * The histogram of **ActualTOW** showed a slightly **right-skewed distribution**, indicating fewer flights with lower takeoff weights ($\sim45,000–55,000$).
* **Creating Day-of-Week Features:**
    * New binary features were engineered from the departure day:
        * **`Weekend`**: $1$ if the departure day is Friday, Saturday, or Sunday; $0$ otherwise.
        * **`WeekDay`**: $1$ if the departure day is Monday, Tuesday, Wednesday, or Thursday; $0$ otherwise.

---

## 🛠️ Modeling and Prediction

### Final Features

After cleaning and engineering, the following seven features were used for modeling the target variable, **ActualTOW**:

1.  **ActualFlightTime**: The real flight duration in minutes.
2.  **ActualTotalFuel**: Total fuel consumed during the flight.
3.  **ActualTOW**: Aircraft’s actual takeoff weight (target variable).
4.  **FLownPassengers**: Number of passengers on the flight.
5.  **FlightBagsWeight**: Total weight of passenger baggage.
6.  **Weekend**: Binary indicator ($1$ for Friday–Sunday).
7.  **WeekDay**: Binary indicator ($1$ for Monday–Thursday).

### Model Training

The dataset was split into training and testing sets. Both the features and the target variable were **scaled** prior to training. Four different regression models were implemented and evaluated:

1.  **Linear Regression**
2.  **Neural Network**
3.  **Decision Tree Regressor**
4.  **Random Forest Regressor**

---

## 📊 Model Performance Summary

The models were evaluated using Root Mean Squared Error (RMSE), Mean Absolute Error (MAE), and R-squared ($R^2$).

| Model | RMSE | MAE | $R^2$ |
| :--- | :--- | :--- | :--- |
| **Neural Network** | **936.49** | **665.39** | N/A |
| Random Forest Regressor | 988.22 | 726.98 | N/A |
| Linear Regression | 1030.97 | 763.15 | 1.5883 |
| Decision Tree Regressor | 1348.40 | 977.49 | N/A |

---

## ✅ Conclusion and Validation

### Conclusion

The **Neural Network** model demonstrated the best performance, achieving the **lowest RMSE (936.49)** and making it the most accurate model for predicting the **ActualTOW**.

* The **Random Forest** was the second-best performer.
* The **Decision Tree** model had the weakest performance, likely due to a tendency to **overfit** the training data.

### Validation

The final, best-performing model (the **Neural Network**) was used to generate predictions for **ActualTOW** on a separate, cleaned, and prepared validation dataset, confirming its generalization ability.

---

## 💻 How to Run This Project

1.  Clone this repository: `git clone [Your-Repo-Link]`
2.  Navigate to the project directory: `cd [Your-Repo-Name]`
3.  Install the required dependencies: `pip install -r requirements.txt` (Update this command if you don't use a requirements file).
4.  Run the main analysis notebook or script: `jupyter notebook prediction_notebook.ipynb` (Replace with your actual file name).
