# 📈 Stock Price Prediction Application

A comprehensive machine learning application that predicts stock prices using deep learning (LSTM neural networks) and provides interactive visualization with data persistence. Built with modern web technologies for real-time financial data analysis.

---

## 🎯 Overview

This full-stack application leverages LSTM (Long Short-Term Memory) neural networks to forecast stock prices based on historical market data. The system fetches live stock data, processes it with advanced machine learning techniques, visualizes trends with moving averages, and stores prediction results in a NoSQL database.

**Perfect for:** Financial analysts, traders, investors, and machine learning enthusiasts looking to explore AI-driven stock market predictions.

---

## ✨ Key Features

### 📊 Prediction Engine
- **LSTM-Based Predictions**: Advanced deep learning model trained on historical stock data
- **Real-Time Data Fetching**: Integrates with Yahoo Finance API (yfinance) to get live market data
- **Flexible Timeframes**: Supports 20-year historical data analysis
- **Accuracy Metrics**: Displays RMSE (Root Mean Squared Error) for model validation

### 📈 Technical Analysis
- **Moving Averages**: 100-day, 200-day, and 250-day moving average calculations
- **Interactive Visualizations**: Matplotlib-based charts for trend analysis
- **Comparative Analysis**: Side-by-side comparison of predicted vs. actual prices
- **Data Normalization**: MinMax scaling for optimal model performance

### 💾 Data Management
- **MongoDB Integration**: Persistent storage of prediction summaries
- **Historical Tracking**: View all past predictions with timestamps
- **Aggregate Metrics**: Average predictions and actual prices per stock

### 🎨 User Interface
- **Streamlit Framework**: Responsive, interactive web interface
- **Real-Time Updates**: Instant stock data and predictions
- **Easy Navigation**: Intuitive controls for different stock tickers
- **Visual Dashboards**: Comprehensive charts and data tables

---

## 🛠️ Technology Stack

| Component | Technology |
|-----------|-----------|
| **Backend** | Python 3.x |
| **Web Framework** | Streamlit |
| **ML/DL** | TensorFlow 2.x, Keras |
| **Data Processing** | Pandas, NumPy, Scikit-Learn |
| **Database** | MongoDB |
| **Data Source** | yfinance (Yahoo Finance API) |
| **Visualization** | Matplotlib |
| **Model Format** | Keras (.keras) |

---

## 📋 Requirements

Python 3.8+ TensorFlow 2.13.0 Keras 2.13.1 Streamlit 1.45.1 Pandas 2.3.0 NumPy 1.24.3 Matplotlib 3.10.3 Scikit-Learn 1.7.0 yfinance 0.2.62 MongoDB 4.x or higher PyMongo 4.13.0

Code

---

## 🚀 Installation & Setup

### 1. **Clone the Repository**
```bash
git clone https://github.com/Ruthu543/StockPrice_Prediction.git
cd StockPrice_Prediction
2. Create Virtual Environment (Recommended)
bash
python -m venv venv
# On Windows
venv\Scripts\activate
# On macOS/Linux
source venv/bin/activate
3. Install Dependencies
bash
pip install -r requirements.txt
4. Setup MongoDB
Option A: Local MongoDB

bash
# Install MongoDB from https://www.mongodb.com/try/download/community
# Start MongoDB service
mongod
Option B: MongoDB Atlas (Cloud)

Create an account at MongoDB Atlas
Create a cluster and get your connection string
Update the connection string in app.py line 12:
Python
client = MongoClient("your_connection_string_here")
5. Run the Application
bash
streamlit run app.py
The app will be available at http://localhost:8501

📖 Usage Guide
Getting Started
Launch the Application

Run streamlit run app.py
Open your browser to the local Streamlit URL
Enter Stock Ticker

Input any valid stock symbol (e.g., GOOG, AAPL, MSFT, AMZN)
The app fetches 20 years of historical data
Analyze the Output

Stock Data: Full historical dataset table
Moving Averages: Visualization of 100, 200, and 250-day trends
Predictions vs Actual: Comparison of model predictions with real prices
Performance Data: Table showing predicted vs. original test values
Save Results

Click "Save Summary to MongoDB" button
Stores average prediction, actual price, and timestamp
Access historical records later
Example Stocks to Try
Tech: GOOG, AAPL, MSFT, NVDA, TSLA
Finance: JPM, BAC, GS, WFC
Energy: XOM, CVX, MPC
Healthcare: JNJ, UNH, PFE, MRK
🧠 Model Architecture
LSTM Model Details
Input Shape: 100 time steps of historical closing prices
Architecture:
LSTM layers with dropout for regularization
Dense layers for feature extraction
Output: Single next-day price prediction
Training: Historical data with MinMax normalization (0-1 scale)
File: Latest_stock_price_model.keras
Data Pipeline
Code
Raw Stock Data → Data Cleaning → Normalization (MinMax) 
→ Sequence Creation (100-day windows) → LSTM Model 
→ Inverse Transform → Price Prediction
📊 Project Structure
Code
StockPrice_Prediction/
├── app.py                              # Main Streamlit application
├── Stock_Prediction.ipynb              # Jupyter notebook with model training
├── Latest_stock_price_model.keras      # Pre-trained LSTM model
├── requirements.txt                    # Python dependencies
├── .gitignore                          # Git ignore file
└── README.md                           # This file
File Descriptions
File	Purpose
app.py	Main web application with Streamlit UI and prediction logic
Stock_Prediction.ipynb	Model training notebook with EDA and model development
Latest_stock_price_model.keras	Pre-trained LSTM neural network (~1.4 MB)
requirements.txt	All Python package dependencies with versions
💡 How It Works
1. Data Fetching
Python
# Retrieves last 20 years of stock data from Yahoo Finance
google_data = yf.download(stock, start, end, auto_adjust=False)
2. Data Preprocessing
Python
# Train-test split (70-30)
splitting_len = int(len(google_data) * 0.7)

# Calculate moving averages
google_data['MA_for_250_days'] = google_data.Close.rolling(250).mean()
google_data['MA_for_200_days'] = google_data.Close.rolling(200).mean()
google_data['MA_for_100_days'] = google_data.Close.rolling(100).mean()
3. Price Normalization
Python
# Scale prices to 0-1 range for better neural network performance
scaler = MinMaxScaler(feature_range=(0, 1))
scaled_data = scaler.fit_transform(x_test[['Close']])
4. Prediction
Python
# Use LSTM to predict test set prices
predictions = model.predict(x_data)
# Convert back to original price range
inv_pre = scaler.inverse_transform(predictions)
5. Visualization & Storage
Python
# Display prediction results
# Store summary to MongoDB for future reference
📈 Performance Metrics
The application tracks several key metrics:

RMSE (Root Mean Squared Error): Measures prediction accuracy
Average Predicted Price: Mean of all predictions
Average Actual Price: Mean of test data
Timestamp: When prediction was made
Lower RMSE values indicate better model accuracy.

⚙️ Configuration
MongoDB Configuration
Edit app.py line 12 to change the database connection:

Python
client = MongoClient("mongodb://localhost:27017/")
db = client["stockApp"]
collection = db["predictions"]
Model Configuration
To use a different trained model, replace Latest_stock_price_model.keras:

Python
model = load_model("your_model_name.keras")
Data Range
To modify historical data range (currently 20 years):

Python
start = datetime(end.year - 20, end.month, end.day)  # Change 20 to desired years
🔍 Troubleshooting
Issue: "Model file not found"
Solution: Ensure Latest_stock_price_model.keras is in the same directory as app.py

Issue: MongoDB connection error
Solution:

Verify MongoDB is running: mongod
Check connection string in app.py
For Atlas: Ensure IP whitelist includes your machine
Issue: Stock ticker not found
Solution: Verify the ticker is valid on Yahoo Finance (use uppercase)

Issue: "No module named 'streamlit'"
Solution: Run pip install -r requirements.txt in your virtual environment

Issue: Slow predictions
Solution: Consider reducing data range or using smaller batches

🎓 Learning Resources
TensorFlow/Keras Documentation
Streamlit Official Guide
yfinance Documentation
LSTM Neural Networks
MongoDB Python Driver
📝 Model Training
The notebook Stock_Prediction.ipynb contains the complete model training pipeline:

Exploratory Data Analysis (EDA)

Price trends over time
Volatility analysis
Correlation analysis
Feature Engineering

Moving averages
Price momentum
Volume analysis
Model Development

LSTM architecture design
Hyperparameter tuning
Model training and validation
Performance evaluation
Model Evaluation

Train/test loss visualization
Prediction accuracy metrics
Error analysis
🚨 Disclaimer
Important: This model is for educational and research purposes only. Stock market predictions are inherently uncertain and involve substantial risk. Never make investment decisions solely based on this or any algorithmic prediction. Always:

Consult with financial advisors
Conduct thorough due diligence
Understand market risks
Use multiple data sources
Keep up with market news and trends
Past performance does not guarantee future results.

🤝 Contributing
Contributions are welcome! To contribute:

Fork the repository
Create a feature branch (git checkout -b feature/AmazingFeature)
Commit your changes (git commit -m 'Add AmazingFeature')
Push to the branch (git push origin feature/AmazingFeature)
Open a Pull Request
Suggested Improvements
 Add more technical indicators (RSI, MACD, Bollinger Bands)
 Implement ensemble models
 Add portfolio analysis features
 Real-time prediction updates
 Email alerts for price predictions
 API endpoint development
 Enhanced error handling
 Unit tests
📄 License
This project is licensed under the MIT License - see the LICENSE file for details.

👤 Author
Ruthu543

GitHub: @Ruthu543
Repository: StockPrice_Prediction


📞 Support & Contact
If you encounter any issues or have suggestions:

Open an Issue
Check existing Discussions
Review the Troubleshooting section

🙏 Acknowledgments
Yahoo Finance for providing historical stock data
TensorFlow/Keras community for excellent deep learning tools
Streamlit for making web app development accessible
MongoDB for robust data storage solutions
Financial data enthusiasts and contributors




