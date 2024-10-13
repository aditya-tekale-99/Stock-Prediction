## [Stock Price Forecasting using Alpha Vantage API and Snowflake ML](https://github.com/aditya-tekale-99/Stock-Prediction/blob/main/stock_prediction_dag.py)

This project is an end-to-end pipeline for extracting stock price data from the Alpha Vantage API, transforming and loading it into Snowflake, and applying Snowflake's Machine Learning (ML) forecasting feature to predict stock prices for the next 7 days. The process is automated using Apache Airflow.

### Project Overview

This repository contains the DAG and associated tasks for performing the following operations:

1. **Extract** stock data for specific symbols (TTWO and GOOGL) from the Alpha Vantage API.
2. **Transform** the data into a format suitable for database storage and future analysis.
3. **Load** the data into Snowflake as the raw stock price data.
4. **Train** a stock price forecasting model using Snowflake's ML forecasting features.
5. **Predict** the next 7 days of stock prices using the trained model.
6. **Store** the forecasted stock prices into a final table that combines actual and forecasted values.

#### Key Features

- **Data Extraction**: The DAG extracts stock price data for the `TTWO` and `GOOGL` stock symbols using Alpha Vantage's "TIME_SERIES_DAILY" function.
- **Data Transformation**: The data is cleaned and transformed to fit a Snowflake schema that includes fields such as `symbol`, `date`, `open`, `high`, `low`, `close`, and `volume`.
- **Data Loading**: The transformed data is loaded into Snowflake's `dev.raw_data.stock_prices` table.
- **Model Training**: Snowflake's ML forecasting feature is used to train a time-series forecasting model based on historical data.
- **Prediction**: The model predicts stock prices for the next 7 days with a confidence interval.
- **Result Storage**: Forecasted and historical stock data are combined into a final table for analysis and reporting.

### Project Structure

- **DAG**: The Airflow DAG `stock_forecast_model` orchestrates the entire pipeline from extraction to loading and prediction.
- **Tasks**:
  - `extract_stock_data`: Extracts raw stock data from the Alpha Vantage API.
  - `transform_stock_data`: Cleans and formats the extracted data.
  - `load_to_snowflake`: Loads the transformed data into Snowflake.
  - `train_forecast_model`: Trains a forecasting model in Snowflake.
  - `predict_stock_prices`: Runs predictions and combines actual and forecasted data into a final table.

### Dependencies

- **Airflow**: Used to orchestrate the DAG and tasks.
- **Alpha Vantage API**: Provides historical stock price data.
- **Snowflake**: The destination for the stock data, used for storage, transformation, and ML predictions.
- **Snowflake ML**: Used to create a forecasting model and predict future stock prices.

### Setup and Usage

1. **Clone this repository**:
   ```bash
   git clone https://github.com/your-username/stock-price-forecasting
   ```

2. **Install dependencies**:
   Ensure you have Airflow set up along with the required providers (Snowflake, HTTP, etc.). You can refer to Airflow's documentation for setup instructions.

3. **Set environment variables**:
   - `alpha_vantage_api_key`: The API key for accessing Alpha Vantage.
   - Configure Snowflake connection in Airflow using the connection ID `snowflake_conn`.

4. **Run the DAG**:
   After starting the Airflow scheduler, activate the DAG by navigating to the Airflow UI and triggering the `stock_forecast_model` DAG.

### Database Structure

- **`raw_data.stock_prices`**: Contains historical stock prices for symbols `TTWO` and `GOOGL`.
  - Columns: `symbol`, `date`, `open`, `high`, `low`, `close`, `volume`
- **`adhoc.stock_prices_forecast`**: Stores forecasted stock prices generated by Snowflake ML.
- **`analytics.stock_prices_with_forecast`**: Combines actual and forecasted data for future analysis.

### Future Improvements

- Support for additional stock symbols.
- Integration with a dashboard tool like Power BI for real-time stock price and forecast visualization.
- Extend the model to include more advanced features or ML algorithms for better accuracy.

### Screenshots

#### Airflow 
![Airflow Web UI](https://github.com/aditya-tekale-99/Stock-Prediction/blob/main/Screenshots/Airflow%20Web%20UI.png)
![Airflow DAG Log](https://github.com/aditya-tekale-99/Stock-Prediction/blob/main/Screenshots/Airflow%20Log.png)
![Airflow DAG Graph](https://github.com/aditya-tekale-99/Stock-Prediction/blob/main/Screenshots/Airflow%20graph.png)

#### Snowflake Tables
![dev.raw_data.stock_prices](https://github.com/aditya-tekale-99/Stock-Prediction/blob/main/Screenshots/Stock_Prices_Table.png)
![dev.adhoc.stock_prices_view](https://github.com/aditya-tekale-99/Stock-Prediction/blob/main/Screenshots/Stock_Prices_View_Table.png)
![dev.adhoc.stock_prices_forecast](https://github.com/aditya-tekale-99/Stock-Prediction/blob/main/Screenshots/Stock_Prices_Forecast_Table.png)
![dev.analytics.stock_prices_with_forecast](https://github.com/aditya-tekale-99/Stock-Prediction/blob/main/Screenshots/Stock_prices_With-Forecast_Table.png)

#### Snowflake SQL Queries
![Ccount of records in raw_data.stock_prices](https://github.com/aditya-tekale-99/Stock-Prediction/blob/main/Screenshots/Count%20of%20records%20for%20each%20stock.png)
![Predicted Stock Data in adhoc.stock_prices_forecast](https://github.com/aditya-tekale-99/Stock-Prediction/blob/main/Screenshots/Predicted_Stock_Data.png)
![Count of Records in analytics.stock_prices_with_forecast](https://github.com/aditya-tekale-99/Stock-Prediction/blob/main/Screenshots/dev.analytics.stock_prices_with_forecast.png)
