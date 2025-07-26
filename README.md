Demand Forecasting with Time Series Models
1. Overview
This project performs demand forecasting on a retail dataset (demand.csv). It analyzes historical sales data to predict future units sold. The script follows a complete data science workflow: data loading and cleaning, exploratory data analysis (EDA), feature engineering, model training, and evaluation.

Three different time series forecasting models are implemented and compared to determine the most accurate one for this dataset:

Holt-Winters Exponential Smoothing (a classical univariate model)

Auto-ARIMAX (a sophisticated model that includes external factors)

Facebook Prophet (a modern forecasting library designed for business time series)

The final output is a performance comparison of the models based on Root Mean Squared Error (RMSE) and a visualization comparing their forecasts against the actual sales data.

2. Project Workflow
The script is structured into a clear, step-by-step process:

Step 1: Setup and Installation
Installs the pmdarima library required for the Auto-ARIMA model.

Imports all necessary Python libraries for data manipulation (pandas, numpy), visualization (matplotlib, seaborn), and time series modeling (statsmodels, pmdarima, prophet).

Step 2: Data Loading and Cleaning
Loads the demand.csv dataset.

Handles missing values in the total_price column by imputing them with the median price for that specific product SKU. This is a robust method that avoids skewing the data.

Converts the week column into a proper datetime format, which is essential for time series analysis.

Step 3: Exploratory Data Analysis (EDA)
Feature Distributions: Visualizes the distributions of key features like store_id, sku_id, total_price, and units_sold to understand their characteristics.

Correlation Analysis: Creates a heatmap to analyze the correlation between numerical features. This step reveals that promotional activities (is_featured_sku, is_display_sku) are positively correlated with units_sold, making them valuable predictors.

Time Series Analysis:

Aggregates total sales by week to get a high-level view of sales over time.

Decomposes the time series into its trend, seasonal, and residual components, clearly identifying a yearly seasonal pattern.

Plots the autocorrelation function, which confirms the strong yearly seasonality observed in the decomposition.

Step 4: Feature Engineering
Aggregates the data on a weekly basis to prepare it for the forecasting models.

Creates new features (regressors) from the raw data, such as the weekly sum of promotional flags (is_featured_sku, is_display_sku) and the weekly average prices (total_price, base_price). These engineered features allow the advanced models (ARIMAX and Prophet) to leverage more information than just the sales data alone.

Step 5: Train-Test Split
Splits the weekly aggregated data into a training set (the first 80% of the data) and a test set (the final 20%).

The models are trained on the training data and evaluated on how well they predict the sales in the test data period.

Step 6: Model Training and Evaluation
Holt-Winters: A baseline model is trained using only the historical sales data (units_sold). It is configured with an additive seasonal component and a period of 52 weeks to match the yearly seasonality.

Auto-ARIMAX: The pmdarima library automatically finds the best ARIMA model parameters. This model is trained on the sales data (y) and the engineered features (exogenous regressors) to improve its predictive power.

Prophet: A Prophet model is trained with yearly seasonality enabled. The same engineered features are added as extra regressors to the model.

Step 7: Final Results and Visualization
Compares the Root Mean Squared Error (RMSE) of all three models to identify the best-performing one.

Generates a comprehensive plot that visualizes the historical training data, the actual test data, and the forecasts from all three models. This makes it easy to visually compare the accuracy of each model.

3. How to Run the Script
Prerequisites
You need to have Python installed along with the following libraries. You can install them using pip:

pip install pandas numpy matplotlib seaborn statsmodels pmdarima prophet

Data File
Ensure you have the demand.csv file in the same directory as the script. The script will not run without it.

Execution
You can run the script from your terminal:

python your_script_name.py

Alternatively, you can run the code in a Jupyter Notebook or Google Colab environment by executing the cells in order.

4. Results
The script will print the RMSE for each model and declare the best-performing one based on the lowest RMSE. The final plot provides a clear visual comparison, showing how closely each model's forecast aligns with the actual units sold during the test period. The inclusion of external regressors in the Auto-ARIMAX and Prophet models is expected to provide more accurate forecasts than the univariate Holt-Winters model.
