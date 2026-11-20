# Non-Stationary to Stationary Time Series Transformation

A rigorous implementation of time series stationarization methods, analyzing the impact of first-order differencing, annual seasonal adjustment, and logarithmic variance stabilization on cyclical data.

---

## Objective

Most parametric time series forecasting models (such as ARMA, ARIMA, and Box-Jenkins algorithms) assume weak covariance stationarity: constant mean, constant variance, and autocovariance that depends solely on the temporal lag. This experiment transforms non-stationary, season-dominated series into stationary processes ready for econometric modeling.

---

## Dataset Utilized

- **Dataset Name**: Daily Minimum Temperatures in Melbourne
- **Filename**: `daily-min-temperatures-Melbourne.csv` (`daily-min-temperatures.csv`)
- **Domain**: Climatological Time Series
- **Location**: Melbourne, Australia
- **Sample Period**: January 1, 1981 – December 31, 1990 (3,650 daily observations)
- **Target Variable**: `Temp` (Minimum daily temperature recorded in Celsius, °C)
- **Primary Characteristics**: Strong deterministic 365-day annual seasonality, sinusoidal temperature oscillations, and weather-driven residual shocks.

---

## Transformation Methodology & Formulas

### 1. First-Order Regular Differencing
Eliminates secular mean trends and linear drift:
$$\Delta y_t = y_t - y_{t-1}$$

### 2. Seasonal Differencing
Eliminates recurring annual periodic cycles using a seasonal period of $s = 365$ days:
$$\Delta_{365} y_t = y_t - y_{t-365}$$

### 3. Combined Regular and Seasonal Differencing
Simultaneously addresses mean drift and seasonal patterns:
$$\Delta \Delta_{365} y_t = (y_t - y_{t-1}) - (y_{t-365} - y_{t-366})$$

### 4. Logarithmic Transformation
Stabilizes variance and compresses right-skewed fluctuations using $\ln(1 + y_t)$ (`np.log1p`):
$$z_t = \ln(1 + y_t)$$

---

## Results & Comparative Visualizations

### 1. Original Daily Minimum Temperature
<img width="1391" height="349" alt="Original Daily Minimum Temperature" src="https://github.com/user-attachments/assets/9a471876-df00-4ec1-bf5d-05281bef85df" />

### 2. After Regular Differencing
<img width="1392" height="346" alt="Regular Differencing" src="https://github.com/user-attachments/assets/0b834005-9edb-45b1-8007-f7d3573de9fc" />

### 3. After Seasonal Differencing (365 Days)
<img width="1391" height="341" alt="Seasonal Adjustment" src="https://github.com/user-attachments/assets/a425013e-eefb-46a9-93b5-633f7af17d31" />

### 4. Log Transformation vs. Original Temperature
<img width="1393" height="341" alt="Log Transformation" src="https://github.com/user-attachments/assets/a6b9f08f-0cf5-4d07-9b6b-5e832486a60d" />

---

## License

This project is licensed under the GNU General Public License v3.0. See the [LICENSE](LICENSE) file for details.
