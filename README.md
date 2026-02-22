# What Drives the Price of a Car?

## Objective
Analyze a used car dataset to identify which factors most strongly influence car prices and translate these findings into clear, actionable recommendations for a used car dealership. This project follows the **CRISP-DM** framework to provide a structured, data-driven approach to solving the business problem.

## Project Link
- [Jupyter Notebook: prompt_II.ipynb](prompt_II.ipynb)

---

## 1. Business Understanding
The goal is to help a used car dealership understand what consumers value in used cars. By identifying key price drivers, the dealership can fine-tune its inventory and pricing strategy to maximize profitability and turnover.
**Key Questions:**
- Which features (year, mileage, condition, fuel type, etc.) have the most significant impact on price?
- How accurately can we predict car prices using these features?
- What are the most profitable categories of vehicles to stock?

## 2. Data Understanding
The dataset, sourced from Kaggle, contains 426K used car listings. Initial exploratory data analysis (EDA) revealed:
- **Missing Values:** Columns like `condition`, `drive`, and `type` had significant missing data, which were handled via imputation or by creating "unknown" categories.
- **Outliers:** Extreme values in `price` and `odometer` were identified and removed using the IQR method to improve model robustness.
- **Skewness:** Car prices were highly right-skewed, requiring a logarithmic transformation (`log1p`) to normalize the distribution for linear modeling.

## 3. Data Preparation
Data cleaning and feature engineering steps included:
- **Feature Creation:** Calculated car `age` (using 2023 as the baseline).
- **Encoding:** 
    - **Frequency Encoding** for high-cardinality features like `model` and `region`.
    - **One-Hot Encoding** for categorical variables like `fuel`, `transmission`, `drive`, and `type`.
    - **Ordinal Encoding** for `condition`.
- **Scaling:** Applied `StandardScaler` to numerical features like `odometer` and `age` within a `Pipeline` to prevent data leakage.

## 4. Modeling
We implemented multiple regression models to predict the log-transformed price:
- **Linear Regression:** Baseline model for initial performance.
- **Lasso & Ridge Regression:** Used `LassoCV` and `RidgeCV` for hyperparameter tuning (alpha) and feature selection.
- **Random Forest Regressor:** An ensemble model to capture non-linear relationships and feature interactions.

Cross-validation was used across all models to ensure performance stability.

## 5. Evaluation
Models were evaluated using **Mean Squared Error (MSE)**, **Mean Absolute Error (MAE)**, **Root Mean Squared Error (RMSE)**, and **R² Score**. All metrics were calculated on the original price scale (back-transformed from log) for business interpretability.

### Model Performance Comparison:
| Model | MAE ($) | RMSE ($) | R² Score |
| :--- | :--- | :--- | :--- |
| **Random Forest** | **$3,203** | **$5,498** | **0.8172** |
| Lasso Regression | $5,010 | $7,531 | 0.6570 |
| Ridge Regression | $5,014 | $7,563 | 0.6541 |
| Linear Regression | $5,014 | $7,563 | 0.6541 |

**Recommendation:** The **Random Forest Regressor** is the recommended model, as it explains **81.7%** of the variance in used car prices and has an average error (MAE) of only **$3,203**.

## 6. Findings & Recommendations (Deployment)

### Key Price Drivers
- **Age (44.7% Importance):** The single most critical factor. Newer cars depreciate significantly each year.
- **Odometer (14.2% Importance):** High mileage strongly reduces value.
- **Vehicle Type & Drive:** **Trucks and Pickups** maintain higher resale values, especially those with **4WD** configurations.
- **Fuel Type:** Diesel vehicles represent a higher-value niche market.

### Actionable Insights for Dealers
1. **Inventory Strategy:** Prioritize stocking **4WD Trucks and Pickups**, as they show higher impact on price and better value retention than standard sedans.
2. **Pricing Policy:** Use the model’s **MAE ($3,203)** as a baseline for pricing flexibility. If a car is priced $4,000 above the model's estimate, it may sit on the lot longer.
3. **Age & Mileage Tiers:** Implement strict acquisition criteria for cars under 10 years old and 100,000 miles, as these are the primary drivers of predictable value.
4. **Regional Optimization:** Adjust inventory based on regional demand (captured by the `region_frequency` feature), as local market density significantly affects pricing power.

---

## Technical Overview
- **Libraries:** `pandas`, `numpy`, `seaborn`, `matplotlib`, `scikit-learn`.
- **Preprocessing:** `ColumnTransformer`, `StandardScaler`, `OneHotEncoder`, `OrdinalEncoder`.
- **Validation:** 80/20 Train-Test split and 5-fold Cross-Validation.

