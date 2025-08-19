# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 19-08-2025

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```
DEVELOPED BY : VELLACHI TILAK
REG NO : 212223240172
```

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

df = pd.read_csv("/content/Gold_price_2025 new.csv")

print("Dataset Head:\n", df.head())

df['Date'] = pd.to_datetime(df['timeOpen'] / 1000, unit='s')
df.set_index('Date', inplace=True)
display(df.head())

# Convert price columns to numeric, replacing commas with periods
price_cols = ['priceOpen', 'priceHigh', 'priceLow', 'priceClose']
for col in price_cols:
    df[col] = df[col].astype(str).str.replace(',', '.', regex=False)
    df[col] = pd.to_numeric(df[col], errors='coerce')

plt.figure(figsize=(10,5))
plt.plot(df['priceClose'], label='Original Data')
plt.title("Gold Price - Original Data")
plt.legend()
plt.show()

# Step 2: Regular Differencing
df['Price_diff'] = df['priceClose'].diff()

plt.figure(figsize=(10,5))
plt.plot(df['Price_diff'], label='Regular Differencing')
plt.title("Gold Price - After Regular Differencing")
plt.legend()
plt.show()

# Step 3: Seasonal Adjustment (Seasonal Differencing, assuming yearly seasonality = 12 months)
df['Price_seasonal_diff'] = df['priceClose'].diff(12)

plt.figure(figsize=(10,5))
plt.plot(df['Price_seasonal_diff'], label='Seasonal Differencing')
plt.title("Gold Price - After Seasonal Adjustment")
plt.legend()
plt.show()

# Step 4: Log Transformation
df['Price_log'] = np.log(df['priceClose'])

plt.figure(figsize=(10,5))
plt.plot(df['Price_log'], label='Log Transformation')
plt.title("Gold Price - After Log Transformation")
plt.legend()
plt.show()


log_reg_diff = df['Price_log'].diff()
plt.figure(figsize=(10,5))
plt.plot(log_reg_diff, label="Log + Regular Differencing")
plt.legend()
plt.title("Gold Price - After Log + Regular Differencing")
plt.show()
# check_stationarity(df['Sales_log_diff'], "After Log + Regular Differencing") # This function is not defined, so I'm commenting it out.


df['Price_log_seasonal_diff'] = df['Price_log'].diff(12).diff()
plt.figure(figsize=(10,5))
plt.plot(df['Price_log_seasonal_diff'], label="Log + Regular + Seasonal Differencing")
plt.legend()
plt.show()
# check_stationarity(df['Sales_log_seasonal_diff'], "After Log + Regular + Seasonal Differencing")


plt.tight_layout()
plt.show()

df.plot(kind='line')
```


### OUTPUT:

# ORIGINAL :
<img width="1060" height="573" alt="image" src="https://github.com/user-attachments/assets/9f5b5b37-77b2-4601-88f1-9b24fc014286" />



# REGULAR DIFFERENCING:

<img width="1062" height="560" alt="image" src="https://github.com/user-attachments/assets/5e660472-16d8-4329-865f-291c56741944" />



# SEASONAL ADJUSTMENT:

<img width="1058" height="563" alt="image" src="https://github.com/user-attachments/assets/0ada7626-13c4-486b-9438-a210f28200ec" />



# LOG TRANSFORMATION:

<img width="1038" height="562" alt="image" src="https://github.com/user-attachments/assets/9efb369b-71c8-43eb-a29e-1036c5bd7089" />

# LOG AND REGULAR DIFFERENCING:

<img width="1055" height="561" alt="image" src="https://github.com/user-attachments/assets/b5673ac2-0bb5-40d6-aac1-e16765e9c255" />

# LOG AND REGULAR AND SEASONAL DIFFERENCING:
<img width="1056" height="527" alt="image" src="https://github.com/user-attachments/assets/db84894e-1a99-4bd8-ab92-3deccae41a48" />

# OVER ALL:

<img width="692" height="549" alt="image" src="https://github.com/user-attachments/assets/aa8c9888-d1ff-482e-a392-d700d59b1104" />


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
