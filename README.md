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

*(Note: Prior documentation erroneously referenced international airline passenger data; the underlying codebase and data specifically evaluate the Melbourne daily minimum temperature records.)*

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

The transformation pipeline visualizes all five states in succession:
1. **Original Raw Series**: Demonstrates recurring seasonal patterns and non-stationary cyclic mean.
2. **Regular Differenced Series**: Removes baseline drift but leaves seasonal peaks intact.
3. **Seasonal Differenced Series**: Removes annual cycles, stabilizing around zero mean.
4. **Regular & Seasonal Differenced Series**: Fully detrended and deseasonalized stationary fluctuations.
5. **Log Transformation**: Variance-stabilized representation.

<p align="center">
  <img src="https://github.com/user-attachments/assets/ea1029c9-63ef-4f1d-b6c8-fceaa98a2eb2" alt="Comparative Time Series Transformation Plots" width="95%" />
</p>

---

## License

This project is licensed under the GNU General Public License v3.0. See the [LICENSE](LICENSE) file for details.
