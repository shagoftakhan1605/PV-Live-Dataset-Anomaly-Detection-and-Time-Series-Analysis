# PV_Live-Dataset-Anomaly-Detection-and-Time-Series-Analysis
This project demonstrates anomaly detection and time series analysis on the Sheffield Solar Monitoring PV_Live dataset. The dataset includes various parameters related to photovoltaic (PV) power generation, such as power generation in MW, installed capacity, and upper and lower confidence limits.

## Project Overview

This project consists of the following key components:
1. **Data Preprocessing**: Loading and cleaning the dataset, handling missing values, and preparing data for analysis.
2. **Anomaly Detection**: Using the Isolation Forest algorithm to detect anomalies in the power generation data.
3. **Fault Diagnosis**: Analyzing the detected anomalies to identify common patterns or faults.
4. **Time Series Analysis**: Decomposing the time series data to observe trends, seasonality, and residuals, and using the SARIMAX model for forecasting future values.

## Dataset

The dataset is obtained from the Sheffield Solar Monitoring PV_Live dataset. It includes the following columns:
- `gsp_id`: ID of the grid supply point.
- `datetime_gmt`: Timestamp of the observation in GMT.
- `generation_mw`: PV power generation in megawatts.
- `lcl_mw`: Lower confidence limit of power generation.
- `ucl_mw`: Upper confidence limit of power generation.
- `installedcapacity_mwp`: Installed capacity in megawatts peak.
- `capacity_mwp`: Capacity in megawatts peak.

## Installation

To run this project, you need to have Python and the following libraries installed:

- pandas
- numpy
- matplotlib
- scikit-learn
- statsmodels
- pmdarima

You can install these libraries using the following command:

```bash
pip install pandas numpy matplotlib scikit-learn statsmodels
```

## Usage

1. Place the dataset file (`PV_Live Historical Results.csv`) in the project directory.

2. Open the Jupyter notebook `PV_Live_Analysis.ipynb` and run the cells sequentially to perform anomaly detection and time series analysis on the dataset.

## Notebook Sections

### 1. Data Preprocessing

- Convert the `datetime_gmt` column to datetime format and set it as the index.
- Handle missing values by forward filling.
- Plot the power generation data.

### 2. Anomaly Detection using Isolation Forest

- Scale the data and train an Isolation Forest model to detect anomalies.
- Plot the power generation data with detected anomalies highlighted.

### 3. Fault Diagnosis

- Analyze the anomalies by examining the time of day when they occur.
- Plot the distribution of anomalies by the hour of the day.

### 4. Time Series Analysis

- Perform the Augmented Dickey-Fuller (ADF) test to check for stationarity.
- Decompose the time series data to observe trends, seasonality, and residuals.
- Train a SARIMAX model for forecasting future values of power generation.

## Results

### Data Preprocessing

- The dataset was successfully loaded and preprocessed. Missing values were handled using forward fill, and the power generation data was plotted to visualize trends over time.

### Anomaly Detection using Isolation Forest

- The Isolation Forest algorithm detected several anomalies in the power generation data. These anomalies were visualized on the time series plot.
- The anomalies were further analyzed to understand their distribution over time.
![download(5)](https://github.com/sirisaacnewton540/PV_Live-Dataset-Anomaly-Detection-and-Time-Series-Analysis/assets/58942453/984bbedf-d5dd-4039-b8d2-dc107d57cbd2)
![download(4)](https://github.com/sirisaacnewton540/PV_Live-Dataset-Anomaly-Detection-and-Time-Series-Analysis/assets/58942453/4ba1cf9f-5579-45b3-8b70-e64e1e15bcba)

### Fault Diagnosis

- The anomalies were found to occur more frequently at certain times of the day, suggesting potential issues with PV systems during those periods.
- This information can be used to schedule maintenance or investigate potential causes of anomalies.
![download(3)](https://github.com/sirisaacnewton540/PV_Live-Dataset-Anomaly-Detection-and-Time-Series-Analysis/assets/58942453/099b2c04-f1b1-417e-bb92-bb14600411a9)

### Time Series Analysis

- The time series decomposition showed clear trends and seasonality in the PV power generation data.
- The SARIMAX model was trained on the dataset and used to forecast future power generation values. The forecasted values can help in predictive maintenance and planning.
![download(2)](https://github.com/sirisaacnewton540/PV_Live-Dataset-Anomaly-Detection-and-Time-Series-Analysis/assets/58942453/b56ddbba-e1a2-432b-8814-eb96a91c7ed1)

### SARIMAX Model Results Explanation
![download(1)](https://github.com/sirisaacnewton540/PV_Live-Dataset-Anomaly-Detection-and-Time-Series-Analysis/assets/58942453/c01b05b5-7eeb-41e5-bbbd-a0b218307612)

``` SARIMAX Results                                       
============================================================================================
Dep. Variable:                        generation_mw   No. Observations:                  292
Model:             SARIMAX(0, 1, 3)x(0, 1, [1], 12)   Log Likelihood               -3280.962
Date:                              Tue, 25 Jun 2024   AIC                           6571.924
Time:                                      15:05:41   BIC                           6590.080
Sample:                                  01-01-2023   HQIC                          6579.207
                                       - 10-19-2023                                         
Covariance Type:                                opg                                         
==============================================================================
                 coef    std err          z      P>|z|      [0.025      0.975]
------------------------------------------------------------------------------
ma.L1         -0.6948      0.104     -6.704      0.000      -0.898      -0.492
ma.L2         -0.1952      0.135     -1.444      0.149      -0.460       0.070
ma.L3          0.0557      0.111      0.503      0.615      -0.161       0.273
ma.S.L12      -0.8606      0.076    -11.260      0.000      -1.010      -0.711
sigma2      1.461e+09   1.01e-11   1.45e+20      0.000    1.46e+09    1.46e+09
===================================================================================
Ljung-Box (L1) (Q):                   0.00   Jarque-Bera (JB):                 2.93
Prob(Q):                              0.97   Prob(JB):                         0.23
Heteroskedasticity (H):               1.29   Skew:                            -0.24
Prob(H) (two-sided):                  0.23   Kurtosis:                         3.12
===================================================================================

Warnings:
[1] Covariance matrix calculated using the outer product of gradients (complex-step).
[2] Covariance matrix is singular or near-singular, with condition number 4.49e+36. Standard errors may be unstable.
```
#### Model Specification
- **Dependent Variable:** `generation_mw`
  - This is the variable (likely electrical power generation in megawatts) that the model aims to forecast.

- **Model:** SARIMAX(0, 1, 3)x(0, 1, [1], 12)
  - **Non-Seasonal Part (p, d, q):** (0, 1, 3)
    - `p=0`: No autoregressive (AR) terms.
    - `d=1`: First-order differencing, indicating that the series was differenced once to achieve stationarity.
    - `q=3`: Three moving average (MA) terms.
  - **Seasonal Part (P, D, Q)[S]:** (0, 1, [1], 12)
    - `P=0`: No seasonal autoregressive terms.
    - `D=1`: Seasonal differencing of order 1, suggesting seasonal adjustment over a 12-month period (monthly data).
    - `Q=[1]`: One seasonal moving average term.
    - `S=12`: Seasonal period of 12, indicating monthly data (annual seasonality).

#### Statistical Measures
- **Log Likelihood:** -3280.962
  - Measures the goodness of fit of the model. Higher values indicate a better fit.
  
- **AIC (Akaike Information Criterion):** 6571.924
  - AIC penalizes model complexity. Lower values indicate a better trade-off between model fit and complexity.
  
- **BIC (Bayesian Information Criterion):** 6590.080
  - Similar to AIC but penalizes more severely for complexity.
  
- **HQIC (Hannan-Quinn Information Criterion):** 6579.207
  - Similar to AIC but penalizes less for complexity than BIC.

#### Coefficients
- **ma.L1 (Moving Average):** -0.6948
  - Coefficient for the first lag of the moving average component.
  - Negative values indicate that deviations from the mean in previous periods tend to be corrected.
  
- **ma.L2:** -0.1952
  - Coefficient for the second lag of the moving average component.
  - The impact of this term on the forecast is less pronounced compared to `ma.L1`.
  
- **ma.L3:** 0.0557
  - Coefficient for the third lag of the moving average component.
  - The positive value suggests a minor tendency for the series to revert to the mean in the third lag, although statistically insignificant (p-value of 0.615).
  
- **ma.S.L12 (Seasonal Moving Average):** -0.8606
  - Coefficient for the seasonal moving average term at lag 12 (seasonal period of 12 months).
  - Significant negative value indicates a strong seasonal adjustment component.

- **sigma2 (Residual Variance):** 1.461e+09
  - Estimated variance of the residuals (errors) in the model.
  - Higher values suggest larger variability that the model does not account for, potentially indicating model inadequacies.

#### Diagnostic Tests
- **Ljung-Box (L1) (Q):** 0.00
  - Tests for autocorrelation of residuals at lag 1.
  - A high p-value (0.97) indicates that residuals are not significantly autocorrelated at lag 1, suggesting a good fit in terms of autocorrelation.

- **Jarque-Bera (JB):** 2.93
  - Tests for normality of residuals.
  - A non-significant p-value (0.23) suggests that residuals are normally distributed, which is good for the validity of the model.

- **Heteroskedasticity (H):** 1.29
  - Tests for heteroskedasticity (varying variance) of residuals.
  - A non-significant p-value (0.23) suggests that residuals have relatively constant variance, which is desirable for model reliability.

#### Warnings
- **Covariance Matrix and Condition Number:**
  - The warning about the covariance matrix being singular or near-singular with a very high condition number (4.49e+36) suggests that the standard errors of the coefficients may be unstable.
  - This can impact the reliability of coefficient estimates and should be interpreted with caution.

### Summary and Recommendations

These results indicate a SARIMAX model that fits the data reasonably well, capturing both non-seasonal and seasonal dynamics in the electrical power generation data. However, the high condition number of the covariance matrix suggests potential instability in the model estimates, which warrants further investigation or possibly refining the model specification.
![download(0)](https://github.com/sirisaacnewton540/PV_Live-Dataset-Anomaly-Detection-and-Time-Series-Analysis/assets/58942453/0ecbae59-c5ee-4e25-aa50-9a6de04bccb4)

## Contributing

Contributions are welcome! Please fork the repository and submit a pull request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

Feel free to customize the README file further as per your requirements.
