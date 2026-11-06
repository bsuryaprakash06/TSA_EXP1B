# Ex.No: 1B CONVERSION OF NON STATIONARY TO STATIONARY DATA
### Date: 06 - 11 - 2026

# AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data.

# ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.

# PROGRAM:
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# 1. Load and process the data once
data = pd.read_csv(
    'https://raw.githubusercontent.com/jbrownlee/Datasets/master/daily-min-temperatures.csv'
)
data['Date'] = pd.to_datetime(data['Date'])
data = data.sort_values('Date')
data = data.set_index('Date')

data['Temp'] = pd.to_numeric(data['Temp'], errors='coerce')
data = data.dropna(subset=['Temp'])

# 2. Compute transformations
data['temp_diff'] = data['Temp'].diff()

period = 365
data['temp_seasonal_diff'] = data['Temp'].diff(period)
data['temp_regular_seasonal_diff'] = (
    data['Temp'].diff().diff(period)
)
data['temp_log'] = np.log1p(data['Temp'])

# 3. Visualizations
plt.figure(figsize=(16, 20))

# Plot 1: Original Series
plt.subplot(5, 1, 1)
plt.plot(data['Temp'], label='Original', color='blue')
plt.title('Original Daily Minimum Temperature')
plt.ylabel('Temperature (°C)')
plt.grid(True)
plt.legend()

# Plot 2: Regular Differencing
plt.subplot(5, 1, 2)
plt.plot(data['temp_diff'], label='Regular Differencing', color='orange')
plt.title('After Regular Differencing')
plt.ylabel('Temp Diff')
plt.grid(True)
plt.legend()

# Plot 3: Seasonal Differencing
plt.subplot(5, 1, 3)
plt.plot(data['temp_seasonal_diff'], label='Seasonal Differencing (365 days)', color='green')
plt.title('After Seasonal Differencing')
plt.ylabel('Seasonal Diff')
plt.grid(True)

# Plot 4: Regular + Seasonal Differencing
plt.subplot(5, 1, 4)
plt.plot(data['temp_regular_seasonal_diff'], label='Regular & Seasonal Differencing', color='purple')
plt.title('After Regular and Seasonal Differencing')
plt.ylabel('Differenced Temp')
plt.grid(True)

# Plot 5: Log Transformation comparison
plt.subplot(5, 1, 5)
plt.plot(data['Temp'], label='Original Temperature', alpha=0.5)
plt.plot(data['temp_log'], label='Log Transformation', color='red')
plt.title('Log Transformation vs Original Temperature')
plt.ylabel('Values')
plt.grid(True)

plt.legend()
plt.tight_layout()
plt.show()
```

# OUTPUT:

## Original Daily Minimum Temperature:
<img width="1391" height="349" alt="{254CD2FA-3E3D-4A5B-94F9-51BF3830D52D}" src="https://github.com/user-attachments/assets/9a471876-df00-4ec1-bf5d-05281bef85df" />


## REGULAR DIFFERENCING:
<img width="1392" height="346" alt="{215CF071-6E1F-41FD-8971-1D848E8611D5}" src="https://github.com/user-attachments/assets/0b834005-9edb-45b1-8007-f7d3573de9fc" />


## SEASONAL ADJUSTMENT:
<img width="1391" height="341" alt="{15E66AA4-4857-4D2B-B573-7A033DDC1CB5}" src="https://github.com/user-attachments/assets/a425013e-eefb-46a9-93b5-633f7af17d31" />


## LOG TRANSFORMATION:
<img width="1393" height="341" alt="{D8C03BB6-E53C-47EA-9EE6-9FD8BCFFFFEC}" src="https://github.com/user-attachments/assets/a6b9f08f-0cf5-4d07-9b6b-5e832486a60d" />


# RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
