Project Title: Advanced EDA & Feature Engineering
DecodeLabs Internship – Data Science Project 1

---Description
This project focuses on transforming a raw e-commerce orders dataset into a clean, analysis-ready dataset. The main goals are:

- Handling missing values using appropriate statistical methods
- Detecting and neutralizing outliers using the IQR method and Winsorization
- Engineering meaningful predictive features for downstream analysis or modeling

The final output is a fully cleaned dataset with original columns plus newly engineered features.


---Dataset
-Source: DecodeLabs E-commerce Orders Dataset  
-Original Shape: 1,200 rows × 14 columns  
-Final Shape: 1,200 rows × 24 columns  


---How to Run

Requirements
- Python 3.8+
- Libraries: `pandas`, `numpy`, `matplotlib`, `seaborn`, `openpyxl` (for Excel support)

You can install the required libraries with:

```bash
pip install pandas numpy matplotlib seaborn openpyxl
```

Steps
1. Place the original dataset (`Dataset for Data Analytics.xlsx`) in the same folder as the notebook.
2. Open the Jupyter Notebook (`project1.ipynb`).
3. Run all cells in order (from top to bottom).
4. After running the final cell, two cleaned files will be generated:
   - `Cleaned_Ecommerce_Orders.csv`
   - `Cleaned_Ecommerce_Orders.xlsx`

Project Workflow

1. Missing Value Treatment
| Column       | Missing Count | Missing % | Method Used             | Justification                                                                 |
|--------------|---------------|-----------|--------------------------|-------------------------------------------------------------------------------|
| CouponCode   | 309           | 25.75%    | Filled with "No Coupon"  | Missingness is meaningful (customer did not use a coupon). Avoids artificial patterns from KNN. |

Result: 0 missing values remaining.

2. Outlier Detection & Treatment
-Method: Interquartile Range (IQR) + Winsorization
-Columns Examined: `TotalPrice`, `UnitPrice`

| Column      | Outliers Found | Action Taken                          |
|-------------|----------------|---------------------------------------|
| TotalPrice  | 8 (0.67%)      | Winsorized (capped at IQR boundaries) |
| UnitPrice   | 0              | No action needed                      |

3. Feature Engineering
New predictive features created:

| Feature              | Description                                      | Type     |
|----------------------|--------------------------------------------------|----------|
| Price_Per_Item       | TotalPrice_clean ÷ Quantity                      | Numeric  |
| Cart_Utilization     | Quantity ÷ ItemsInCart                           | Numeric  |
| Used_Coupon          | 1 if a coupon was used, otherwise 0              | Binary   |
| High_Value_Order     | 1 if order is in the top 25% of TotalPrice       | Binary   |
| Year, Month, Quarter | Extracted from the Date column                   | Numeric  |
| Is_Weekend           | 1 if the order was placed on a weekend           | Binary   |


Final Deliverables
- `Cleaned_Ecommerce_Orders.csv`
- `Cleaned_Ecommerce_Orders.xlsx`
- This `README.md` file


Key Decisions
- Used "No Coupon" instead of KNN imputation to avoid introducing artificial patterns.
- Applied Winsorization instead of deleting outlier rows to preserve the full dataset.
- Engineered features that capture price efficiency, cart behavior, coupon usage, and time-based patterns.
