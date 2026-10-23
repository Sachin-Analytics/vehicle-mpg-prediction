# Vehicle Combined MPG Prediction

A machine learning regression project that predicts a vehicle's **combined fuel economy (MPG)** from its specifications, using Linear, Ridge, Lasso and ElasticNet Regression.

## Table of Contents

- [Problem Statement](#problem-statement)
- [Dataset](#dataset)
- [Project Workflow](#project-workflow)
- [Data Cleaning](#data-cleaning)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Modeling](#modeling)
- [Results](#results)
- [Sample Prediction](#sample-prediction)
- [Tools and Technologies](#tools-and-technologies)
- [Project Structure](#project-structure)
- [How to Run](#how-to-run)
- [Author](#author)

## Problem Statement

Fuel economy is a key factor for buyers, manufacturers and regulators. The objective of this project is to build a regression model that predicts **combined MPG** from vehicle attributes such as engine size, cylinders, drive type, transmission, fuel type, vehicle class, manufacturer and model year, and to compare multiple regression techniques to find the best performer.

## Dataset

| Item | Details |
|------|---------|
| Source | EPA Fuel Economy dataset (fueleconomy.gov) |
| Original size | 39,181 records, 83 features |
| After cleaning | 33,434 records, 12 features |
| Target variable | `combined_mpg` |
| File used in notebook | `data/vehicles_mpg.csv` |

**Selected features**

| Feature | Description |
|---------|-------------|
| `engine_cylinders` | Number of engine cylinders |
| `engine_displacement` | Engine displacement (liters) |
| `model_year` | Vehicle model year |
| `drive_type` | Drive system (FWD, RWD, AWD, 4WD) |
| `transmission` | Transmission type |
| `fuel_type` | Primary fuel type |
| `vehicle_class` | Vehicle class (compact, SUV, pickup, etc.) |
| `manufacturer` | Vehicle manufacturer |
| `co2_emission` | Tailpipe CO₂ emissions (g/mile) |
| `annual_fuel_cost` | Estimated annual fuel cost ($) |
| `annual_fuel_consumption` | Annual fuel consumption (barrels) |

## Project Workflow

1. Data understanding and quality assessment
2. Data cleaning and standardization
3. Feature selection (83 features reduced to 12)
4. Outlier analysis
5. Exploratory data analysis
6. Preprocessing with `ColumnTransformer`
7. Model training (Linear, Ridge, Lasso, ElasticNet)
8. Model evaluation and comparison
9. Prediction on new vehicle data

## Data Cleaning

- Removed **71 duplicate records** from the raw data, and further duplicates after feature selection
- Treated impossible negative values (cylinders, displacement, fuel cost, fuel consumption) as missing values
- Imputed missing numerical values with the **median** and missing categorical values with the **mode**
- Standardized categorical text (trimmed spaces, consistent title case), which reduced category counts:

| Feature | Before | After |
|---------|--------|-------|
| Drive type | 25 | 8 |
| Transmission | 79 | 37 |
| Fuel type | 16 | 6 |
| Vehicle class | 90 | 34 |
| Manufacturer | 214 | 134 |

- Removed the invalid `Unknown` drive type category (0.10% of records)
- Retained outliers after analysis, since extreme values correspond to genuine vehicles such as electric, hybrid, and high-performance models

## Exploratory Data Analysis

Analysis covered the target distribution, feature distributions, relationships with MPG, and a correlation heatmap.

**Correlation with Combined MPG**

| Feature | Correlation |
|---------|------------:|
| CO₂ emission | -0.82 |
| Annual fuel consumption | -0.80 |
| Annual fuel cost | -0.75 |
| Engine displacement | -0.56 |
| Engine cylinders | -0.51 |
| Model year | 0.19 |

**Key insights**

- Most vehicles achieve between 15 and 25 MPG, and the target is right-skewed
- Larger engines and more cylinders are associated with lower fuel economy
- 4-cylinder and 6-cylinder engines are the most common configurations
- Average fuel economy improved noticeably from 2009 onward
- Electric vehicles show the highest MPG values (measured as MPGe), followed by diesel
- Compact, subcompact and small station wagon classes are the most efficient, while pickup trucks are the least

## Modeling

**Preprocessing:** `ColumnTransformer` with `StandardScaler` for numerical features and `OneHotEncoder` for categorical features.

**Train-test split:** 80% training, 20% testing (`random_state=42`).

**Models trained**

- Linear Regression
- Ridge Regression (L2)
- Lasso Regression (L1)
- ElasticNet (L1 + L2)

**Evaluation metrics:** R², MSE, RMSE, MAE and MAPE.

## Results

| Model | R² | RMSE | MAE | MAPE |
|-------|----|------|-----|------|
| **Linear Regression** | **0.929** | **1.71** | **1.03** | **5.2%** |
| Ridge Regression | 0.928 | 1.72 | 1.04 | 5.2% |
| Lasso Regression | 0.695 | 3.55 | 1.49 | 7.0% |
| ElasticNet | 0.668 | 3.70 | 1.52 | 7.0% |

**Final model: Linear Regression**, with a training R² of 0.915 and a test R² of 0.929. The close match between training and test scores shows the model generalizes well. On average, predictions are within about 1 MPG of the actual value.

## Sample Prediction

| Input | Value |
|-------|-------|
| Cylinders / Displacement | 4 / 2.0 L |
| Model year | 2022 |
| Drive type | Front-Wheel Drive |
| Transmission | Automatic 6-Spd |
| Fuel type | Regular Gasoline |
| Vehicle class | Compact Cars |
| Manufacturer | Toyota |

**Predicted combined MPG (Linear Regression): 27.3**

## Tools and Technologies

Python · Pandas · NumPy · Matplotlib · Seaborn · Scikit-learn · Jupyter Notebook

## Project Structure

```
vehicle-mpg-prediction/
├── vehicle_mpg_regression.ipynb
├── requirements.txt
├── README.md
└── data/
    └── vehicles_mpg.csv
```

## How to Run

1. Download `vehicle_mpg_regression.ipynb`, `requirements.txt` and `data/vehicles_mpg.csv` from this folder.
2. Install the dependencies:

```bash
pip install -r requirements.txt
```

3. Open the notebook:

```bash
jupyter notebook vehicle_mpg_regression.ipynb
```

## Author

**Sachin More**
Aspiring Data Analyst | Data Science | AI & Machine Learning

- GitHub: [@Sachin-Analytics](https://github.com/Sachin-Analytics)
- Email: [moresachin9124@gmail.com](mailto:moresachin9124@gmail.com)
