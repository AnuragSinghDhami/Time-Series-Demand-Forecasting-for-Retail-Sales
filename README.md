# 📈 Time-Series-Demand-Forecasting-for-Retail-Sales

## 1. Overview 🔍
This project performs demand forecasting on a retail dataset (**demand.csv**). It analyzes historical sales data to predict future units sold, following a complete data science workflow:

- 📂 Data loading and cleaning  
- 📊 Exploratory data analysis (EDA)  
- 🛠 Feature engineering  
- 🤖 Model training and evaluation  

Three time series forecasting models are implemented and compared:

1. **Holt-Winters Exponential Smoothing** – Classical univariate model.  
2. **Auto-ARIMAX** – Advanced model including external factors.  
3. **Facebook Prophet** – Modern forecasting library designed for business time series.  

The final output compares model performance using **Root Mean Squared Error (RMSE)** and visualizes forecasts vs. actual sales data.

---

## 2. Project Workflow 🧭

### **Step 1: Setup and Installation ⚙️**
- Installs the `pmdarima` library for Auto-ARIMA.
- Imports essential libraries:  
  `pandas`, `numpy` (data manipulation), `matplotlib`, `seaborn` (visualization), `statsmodels`, `pmdarima`, `prophet` (time series modeling).

### **Step 2: Data Loading and Cleaning 🧹**
- Loads **demand.csv**.
- Handles missing values in `total_price` by imputing with the **median SKU price**.
- Converts `week` column to datetime format (essential for time series analysis).

### **Step 3: Exploratory Data Analysis (EDA) 📊**
- **Feature Distributions:** Visualizes `store_id`, `sku_id`, `total_price`, `units_sold`.  
- **Correlation Analysis:** Heatmap reveals positive correlation between promotional activities (`is_featured_sku`, `is_display_sku`) and `units_sold`.  
- **Time Series Analysis:**  
  - Aggregates total weekly sales.  
  - Decomposes series into trend, seasonality, and residual components.  
  - ACF plot confirms **yearly seasonality**.

### **Step 4: Feature Engineering 🛠**
- Aggregates data on a **weekly** basis.  
- Creates engineered features:  
  - Weekly promotional flags (`is_featured_sku`, `is_display_sku`).  
  - Weekly average prices (`total_price`, `base_price`).  
- These features improve ARIMAX & Prophet models.

### **Step 5: Train-Test Split ✂️**
- 80% training data, 20% test data.  
- Models trained on the training set and evaluated on test predictions.

### **Step 6: Model Training and Evaluation 🤖**
- **Holt-Winters:** Baseline model with additive seasonality (52 weeks).  
- **Auto-ARIMAX:** Finds optimal ARIMA parameters and uses exogenous features.  
- **Prophet:** Configured with yearly seasonality + engineered regressors.

### **Step 7: Final Results and Visualization 📉**
- Compares RMSE for all three models.  
- Plots historical data, test data, and model forecasts for easy visual comparison.

---

## 3. How to Run the Script 🚀

### **Prerequisites 📦**
Install Python libraries:
```bash
pip install pandas numpy matplotlib seaborn statsmodels pmdarima prophet
```
### **Data File 📁**
Place demand.csv in the same directory as the script.

### **Execution**
Run the script:
```
python your_script_name.py
```
Or execute the cells in a Jupyter Notebook/Google Colab.

## 4. Results 💻
The script prints RMSE for each model and identifies the best-performing one.

The forecast visualization compares predicted vs. actual sales.

Models with external regressors (Auto-ARIMAX & Prophet) are expected to outperform Holt-Winters due to additional features.

