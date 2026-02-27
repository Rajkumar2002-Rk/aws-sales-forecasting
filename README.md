# 🛒 End-to-End Retail Sales Forecasting on AWS SageMaker

## 📌 Project Overview
This project demonstrates a complete end-to-end Machine Learning pipeline built in the cloud using **AWS SageMaker**. The goal of this project was to ingest raw, transactional retail data, clean and aggregate it, and train an **XGBoost** model to forecast total daily revenue for the crucial holiday shopping season.

## 🛠️ Tech Stack & Tools
* **Cloud Platform:** Amazon Web Services (AWS)
* **Compute:** SageMaker Notebooks (`ml.t2.medium`), SageMaker Training Jobs (`ml.m5.large`), SageMaker Real-Time Endpoints
* **Storage:** Amazon S3
* **Languages & Libraries:** Python, Pandas, NumPy, Scikit-Learn, Matplotlib, Boto3

## 🏗️ Project Architecture & Workflow
1. **Data Engineering & Cleaning (Pandas):** * Ingested over 500,000 rows of raw transactional data.
   * Handled missing values and removed negative quantities (canceled orders/returns) using Boolean masking.
   * Aggregated transactional data into a daily time-series format (`groupby`).
   * Reindexed the timeline to handle missing days (zero-sales days) to ensure a continuous time-series.
2. **Feature Engineering:**
   * Engineered time-based features (Month, Day, DayOfWeek, Year) from the `Datetime` index to prepare the data for the XGBoost algorithm.
3. **Cloud Model Training (XGBoost):**
   * Staged the cleaned, split data (Train/Test) into Amazon S3.
   * Configured and launched a SageMaker Training Job using the built-in XGBoost container.
4. **Deployment & Inference:**
   * Deployed the trained model artifact to a SageMaker Real-Time Endpoint.
   * Formatted the holdout test data (Nov-Dec holiday season) and invoked the endpoint for predictions.
5. **Evaluation & Visualization:**
   * Visualized Actual vs. Predicted revenue using Matplotlib.
   * Evaluated model accuracy using Mean Absolute Error (MAE) and Root Mean Squared Error (RMSE).
   * Safely deleted the endpoint post-evaluation to optimize cloud costs.

## 📊 Results
The model successfully captured the weekly seasonality and the general upward trend of the holiday shopping season. 

<img width="1503" height="609" alt="Screenshot 2026-02-27 at 2 58 16 PM" src="https://github.com/user-attachments/assets/9f373dc6-128e-41b7-bac0-fc644340b698" />
