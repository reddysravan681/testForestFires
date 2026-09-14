# Fire Weather Index (FWI) Prediction - End-to-End ML Deployment

A complete end-to-end machine learning project that predicts the **Fire Weather Index (FWI)** using environmental parameters from the Algerian Forest Fires dataset. The project includes data cleaning, exploratory data analysis, feature engineering, model training, and deployment as a Flask web application on AWS Elastic Beanstalk.

---

## Project Overview

The Fire Weather Index (FWI) is a critical indicator used in wildfire management and prevention. This project builds a regression model to predict FWI based on meteorological conditions such as temperature, humidity, wind speed, rainfall, and various forest fire weather indices (FFMC, DMC, ISI).

### Key Highlights

- **Dataset**: Algerian Forest Fires Dataset (243 records, 2 regions)
- **Model**: Ridge Regression (R² = 0.9847 on test data)
- **Web App**: Flask-based web interface with a responsive UI
- **Deployment**: AWS Elastic Beanstalk ready

---

## Project Structure

```
.
├── application.py              # Flask application (main entry point)
├── models/
│   ├── ridge.pkl               # Trained Ridge Regression model
│   └── scaler.pkl              # StandardScaler for feature normalization
├── notebooks/
│   ├── Algerian_forest_fires_dataset.csv   # Raw dataset
│   ├── EDA&FE.ipynb            # Data cleaning, EDA, and Feature Engineering
│   └── model.ipynb             # Model training and evaluation
├── templates/
│   ├── index.html              # Landing page
│   └── home.html               # Prediction form UI
├── .ebextensions/
│   └── python.config           # AWS Elastic Beanstalk configuration
├── requirements.txt            # Python dependencies
└── README.md                   # Project documentation
```

---

## Features Used for Prediction

| Feature  | Description                        |
|----------|------------------------------------|
| Temperature | Temperature in °C               |
| RH       | Relative Humidity (%)             |
| Ws       | Wind Speed (km/h)                 |
| Rain     | Rainfall (mm)                     |
| FFMC     | Fine Fuel Moisture Code           |
| DMC      | Duff Moisture Code                |
| ISI      | Initial Spread Index              |
| Classes  | Fire (1) or Not Fire (0)          |
| Region   | Bejaia (0) or Sidi-Bel Abbes (1) |

**Target Variable**: `FWI` (Fire Weather Index)

---

## Data Processing Pipeline

1. **Data Cleaning**:
   - Removed null rows and duplicate header rows
   - Stripped whitespace from column names
   - Converted data types to appropriate numeric types

2. **Feature Engineering**:
   - Encoded `Classes` column: `fire` → 1, `not fire` → 0
   - Added `region` column based on dataset split (Bejaia = 0, Sidi-Bel Abbes = 1)
   - Dropped highly correlated features (`BUI`, `DC`) with correlation > 0.85 to reduce multicollinearity

3. **Feature Scaling**:
   - Applied `StandardScaler` to normalize features for better model performance

4. **Train-Test Split**:
   - 75% training, 25% test split with `random_state=42`

---

## Model Performance

| Model              | MSE    | MAE    | R² Score |
|--------------------|--------|--------|----------|
| Linear Regression  | 0.6743 | 0.5468 | 0.9848   |
| Lasso Regression   | 2.2483 | 1.1332 | 0.9492   |
| **Ridge Regression** | —    | —      | **0.9847** |

> Ridge Regression was selected for deployment due to its strong generalization with regularization.

---

## Installation & Setup

### Prerequisites

- Python 3.8+
- pip

### Steps

1. **Clone the repository**:
   ```bash
   git clone https://github.com/<your-username>/fwi-prediction.git
   cd fwi-prediction
   ```

2. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

3. **Run the Flask application**:
   ```bash
   python application.py
   ```

4. **Access the app**:
   Open your browser and navigate to:
   ```
   http://localhost:5000
   ```

---

## AWS Elastic Beanstalk Deployment

This project is configured for deployment on AWS Elastic Beanstalk.

1. Install the EB CLI:
   ```bash
   pip install awsebcli
   ```

2. Initialize EB:
   ```bash
   eb init
   ```

3. Create an environment and deploy:
   ```bash
   eb create
   ```

4. Open the deployed app:
   ```bash
   eb open
   ```

---

## Web Application

### Landing Page
- URL: `/`
- Displays a welcome page

### Prediction Page
- URL: `/predictdata`
- Input form with 9 environmental parameters
- Returns the predicted Fire Weather Index (FWI) value

---

## Dependencies

| Package       | Purpose                              |
|---------------|--------------------------------------|
| Flask         | Web framework                        |
| NumPy         | Numerical computations               |
| Pandas        | Data manipulation                    |
| scikit-learn  | Machine learning (Ridge, Scaler)     |

---

## License

This project is open source and available for educational purposes.
