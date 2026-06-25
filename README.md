# Norwegian Salmon Export Price Forecasting

Time series forecasting of monthly Norwegian salmon export 
prices (NOK/kg) over a 12-month horizon, using ARIMA, ETS, 
and VAR. Data retrieved live from Statistics Norway (SSB) 
via public API (table 03024), covering January 2000 to 
April 2026 (316 monthly observations).

## Models compared
| Model | RMSE | MAE | MASE |
|-------|------|-----|------|
| ETS(A,A,A) | 0.129 | 0.112 | 0.657 |
| ARIMA(2,1,1)(1,0,0)[12] | 0.143 | 0.119 | 0.700 |
| VAR(11) | 0.202 | 0.153 | 0.902 |

## Model selection
ARIMA is selected for the final forecast despite ETS 
achieving a marginally lower RMSE. ETS fails the 
Ljung-Box residual test severely (p = 4.7×10⁻¹²), 
rendering its prediction intervals unreliable. ARIMA 
produces white noise residuals (p = 0.110) and is the 
only model that delivers both point forecast accuracy 
and reliable uncertainty quantification.

## 12-month forecast (May 2026 – April 2027)
NOK 70–78/kg, with a seasonal summer dip before 
partial year-end recovery. 95% prediction interval 
widens from ±7 NOK/kg at 1 month to ±28 NOK/kg 
at 12 months.

## Methods
- Log transformation and ADF/KPSS stationarity tests
- STL decomposition for trend/seasonal analysis
- Structural break testing (QLR/sup-F)
- Granger causality testing for VAR specification
- Out-of-sample evaluation on 40-month hold-out set

## Tech Stack
R · tsibble · fable · feasts · SSB API

## Authors
Torjus Arne Ljungqvist · Jan Henrik Haudemann-Andersen 
· Sebastian Nes Romero
Copenhagen Business School, Spring 2026
