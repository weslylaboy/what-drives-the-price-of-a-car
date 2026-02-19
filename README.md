# What Drives the Price of a Car?

## Objective
Analyze a used car dataset to identify which factors most strongly influence car prices and translate these 
findings into clear, actionable recommendations for a used car dealership.

## Project Link
- [Jupyter Notebook: prompt_II.ipynb](prompt_II.ipynb)

## Summary of Findings
Based on the Exploratory Data Analysis (EDA) of 426K used car listings, the following key factors drive pricing:

*   **Vehicle Age & Mileage:** There is a strong positive correlation (0.64) between `year` and `price`, and a moderate negative correlation (-0.59) between `odometer` and `price`. Newer cars with lower mileage consistently command higher prices.
*   **Manufacturer Brand:** Brands like Ford, Chevrolet, Toyota, and Honda dominate the market volume. However, brands like **RAM** and **GMC** show higher median prices ($29,990 and $21,999 respectively), indicating strong resale value for trucks.
*   **Drive Type:** Vehicles with **4WD** and **RWD** tend to have significantly higher average prices compared to FWD vehicles.
*   **Condition:** While 'New' and 'Like New' conditions fetch higher prices, 'Good' condition vehicles also show a high median price, suggesting buyers value well-maintained used cars.
*   **Regional Trends:** Car type preferences vary significantly by state, though **SUVs** remain the most popular segment across nearly all regions.

## Actionable Recommendations
1.  **Inventory Strategy:** Prioritize stocking **4WD SUVs and Trucks**, particularly from high value brands like RAM and GMC, as they maintain higher median resale prices.
2.  **Mileage Management:** Focus on acquiring vehicles with less than 100,000 miles, as the price depreciation accelerates significantly beyond this point.
3.  **Targeted Sourcing:** Use regional data to stock specific car types that are in high demand in your state (e.g., higher SUV inventory in mountainous regions).
4.  **Condition Labeling:** Ensure accurate reporting of 'Good' and 'Excellent' conditions, as these categories overlap significantly in market value, providing opportunities for competitive pricing.

## Technical Overview
The analysis follows the **CRISP-DM** framework:
1.  **Data Cleaning:** Handled extreme price and odometer outliers using the IQR method and 99th percentile capping.
2.  **Missing Values:** Categorical gaps in `condition`, `drive`, and `paint_color` were handled by creating 'unknown' categories to preserve data integrity for modeling.
3.  **Transformations:** Applied logarithmic transformations to the price variable to normalize distribution and stabilize variance for future regression modeling.

### Dataset Description
The dataset is sourced from Kaggle and contains information on used cars. While the original dataset contained 3 million 
records, this version includes 426K entries to facilitate faster processing.

| Column | Description |
| :--- | :--- |
| **id** | Unique identifier for the listing. |
| **region** | The region where the car is listed. |
| **price** | The listed price of the car (Target Variable). |
| **year** | The manufacturing year of the car. |
| **manufacturer** | The brand/maker of the car. |
| **model** | The specific model of the car. |
| **condition** | The condition of the car (e.g., good, excellent). |
| **cylinders** | The number of cylinders in the engine. |
| **fuel** | The type of fuel used by the car (e.g., gas, diesel). |
| **odometer** | The mileage of the car. |
| **title_status** | The status of the car's title (e.g., clean, salvage). |
| **transmission** | The type of transmission (e.g., automatic, manual). |
| **VIN** | Vehicle Identification Number. |
| **drive** | The type of drive (e.g., 4wd, fwd, rwd). |
| **size** | The size category of the car. |
| **type** | The body type of the car (e.g., sedan, SUV, truck). |
| **paint_color** | The color of the car's exterior paint. |
| **state** | The US state where the car is listed. |

