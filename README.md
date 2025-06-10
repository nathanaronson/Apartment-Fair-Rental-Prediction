# Apartment Rental Price Prediction

**CIS 5450 Final Project**  
Nathan Aronson, Savir Basil, Khoi Dinh

---

## Overview

This project investigates the main drivers of apartment rental prices across the United States in 2023. Using a large dataset of apartment listings, we performed data cleaning, exploratory data analysis (EDA), feature engineering, and built predictive models to estimate fair rental prices and identify the most important predictors.

---

## Table of Contents

- [Dataset](#dataset)
- [Installation & Requirements](#installation--requirements)
- [Data Preprocessing](#data-preprocessing)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Feature Engineering](#feature-engineering)
- [Modeling](#modeling)
- [Results](#results)
- [Key Findings](#key-findings)
- [Future Work](#future-work)

---

## Dataset

- **Source:** Aggregated US apartment listings (2023), originally from Kaggle, hosted on GitHub.
- **Features:** Price, location (latitude/longitude, state, city), square footage, amenities, bedrooms, bathrooms, pets allowed, and more.
- **Size:** ~99,000 listings before cleaning.

---

## Installation & Requirements

**Version:**
Python 3.10

**Python Libraries:**
- pandas
- numpy
- matplotlib
- seaborn
- folium
- plotly
- scikit-learn
- torch (PyTorch)

**To install dependencies:**

```pip install pandas numpy matplotlib seaborn folium plotly scikit-learn torch```

---

## Data Preprocessing

- Dropped columns with little predictive value: `id`, `category`, `title`, `body`, `currency`, `address`, `source`, etc.
- Filled missing values:
  - `amenities`, `pets_allowed`: filled with "Missing".
  - `bedrooms`, `bathrooms`: filled with median values.
- Dropped rows with remaining missing values.
- One-hot encoded categorical features (`amenities`, `pets_allowed`, `has_photo`, `state`, `fee`).
- Removed outliers using 1.5x IQR for `bathrooms`, `bedrooms`, `price`, `square_feet`.
- Converted `bathrooms` and `bedrooms` to integers.
- Final dataset: ~92,000 rows, 43 columns after cleaning and encoding.

---

## Exploratory Data Analysis

- **Distribution Analysis:** Price and square footage are approximately normal with slight right skew.
- **Geographic Trends:** High-density clusters in major cities; West and East coasts have higher prices than central US.
- **Feature Relationships:** Strong correlation between square footage and price; bedrooms and bathrooms less correlated with price than expected; longitude/latitude most predictive.

---

## Feature Engineering

- Created `total_rooms` = bedrooms + bathrooms.
- Created `is_premium_listing`: listings with both a photo and a fee.
- Dropped high-cardinality and low-value columns: `cityname`, `time`.
- One-hot encoded all categorical variables; standardized numeric features.

---

## Modeling

| Model                    | R² (Test) | MSE (Test)  |
|--------------------------|-----------|-------------|
| Linear Regression (PCA)  | 0.44      | 151,673     |
| Gradient Boosting (Tuned)| 0.56      | 120,514     |
| Random Forest (Tuned)    | 0.86      | 38,727      |
| Neural Network           | 0.64      | 98,997      |

- **Best Model:** Random Forest Regressor (tuned).

---

## Key Findings

- **Location (longitude, latitude)** is the most significant predictor, far outweighing amenities or even square footage.
- **Square footage** is the next most important factor.
- **State-level effects** (e.g., Colorado) can also influence pricing.
- **Amenities and pets policies** have minor impact compared to location and size.
- **Random Forest** outperformed all other models, explaining ~86% of price variance and achieving the lowest MSE.
- **Neural networks** showed promise but require more tuning and data for optimal results.

---

## Future Work

- Integrate socioeconomic and neighborhood data (e.g., census, crime rates, commute times).
- Expand temporal coverage to analyze trends and seasonality.
- Develop a fair pricing classifier (underpriced, fair, overpriced).
- Further tune neural networks (architecture, hyperparameters).
- Explore additional geospatial features for more granular location effects.

---

**For any questions or contributions, please contact the project authors.**

---
