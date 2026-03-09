# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION
Date:09/03/2026
### AIM:
To Implement Linear and Polynomial Trend Estiamtion Using Python.

### ALGORITHM:
Import necessary libraries (NumPy, Matplotlib)

Load the dataset

Calculate the linear trend values using least square method

Calculate the polynomial trend values using least square method

End the program
### PROGRAM:
A - LINEAR TREND ESTIMATION
B- POLYNOMIAL TREND ESTIMATION
```
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd

# 1. Load the dataset
df = pd.read_csv('data.csv')
df['date'] = pd.to_datetime(df['date'])

# Grouping by date for cleaner daily price averages
daily_data = df.groupby('date')['price'].mean().reset_index()
daily_data = daily_data.sort_values('date')

# 2. Prepare independent variable (x) as numerical days from start
x = (daily_data['date'] - daily_data['date'].min()).dt.days.values
y = daily_data['price'].values

# 3. Calculate Linear Trend (Least Square Method - Degree 1)
coeffs_linear = np.polyfit(x, y, 1)
daily_data['linear_trend'] = np.polyval(coeffs_linear, x)

# 4. Calculate Polynomial Trend (Least Square Method - Degree 2)
coeffs_poly = np.polyfit(x, y, 2)
daily_data['poly_trend'] = np.polyval(coeffs_poly, x)

# --- OUTPUT SECTION ---

print("A - LINEAR TREND ESTIMATION")
print("-" * 45)
# Displaying Date and Price as requested
print(daily_data[['date', 'price', 'linear_trend']].head(10).to_string(index=False))

print("\n" + "="*50 + "\n")

print("B - POLYNOMIAL TREND ESTIMATION")
print("-" * 45)
# Displaying Date and Price as requested
print(daily_data[['date', 'price', 'poly_trend']].head(10).to_string(index=False))

# Optional: Visualization
plt.figure(figsize=(10, 5))
plt.plot(daily_data['date'], daily_data['price'], 'o', markersize=4, label='Actual Avg Price', color='gray')
plt.plot(daily_data['date'], daily_data['linear_trend'], label='Linear Trend', linewidth=2)
plt.plot(daily_data['date'], daily_data['poly_trend'], label='Polynomial Trend', linewidth=2)
plt.legend()
plt.title("Trend Estimation Analysis")
plt.show()
```
### OUTPUT
A - LINEAR TREND ESTIMATION
B- POLYNOMIAL TREND ESTIMATION

<img width="826" height="451" alt="tex 2" src="https://github.com/user-attachments/assets/b0097d04-5991-4245-ac6a-1b432f17c104" />

### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
