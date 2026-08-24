# 📈 Stock Price Prediction App

A Streamlit web app to predict stock prices using deep learning (LSTM), visualize moving averages, and save predictions to MongoDB.

## 🚀 Features
- Predict future stock prices using a trained Keras model
- Show 100, 200, and 250-day moving averages
- Interactive plots with Streamlit
- Save predictions to MongoDB
- View historical predictions with RMSE

## 🛠️ Tech Stack
- Python, Streamlit, TensorFlow/Keras
- MongoDB for data storage
- yfinance for fetching stock data
- matplotlib, pandas, scikit-learn

## 📦 How to Run Locally
```bash
git clone https://github.com/Ruthu543/StockPrice_Prediction.git
cd StockPrice_Prediction
pip install -r requirements.txt
streamlit run app.py
