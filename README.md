# AWT-LSTM-ARIMAX-FIEGARCH Hybrid Model

This repository contains the research and codebase for my **Investment Analysis MSc Research Project**. The project develops a hybrid forecasting framework that integrates econometric models, wavelet-based signal processing, and deep learning to improve stock market prediction accuracy.

---

## 📖 Project Overview
The goal of this project is to forecast the **S&P 500 index** by combining:
- **Adaptive Wavelet Transform (AWT):** For multi-frequency decomposition and denoising of financial time series.
- **ARIMAX-FIEGARCH Models:** To capture linear dependencies, long memory, and volatility dynamics.
- **LSTM Networks:** To learn nonlinear temporal patterns in returns and exogenous variables.

This hybrid model aims to outperform standalone econometric and deep learning models by leveraging both statistical rigor and machine learning flexibility.

---

## ⚙️ Methodology Workflow
1. **Data Acquisition**  
   - S&P 500 OHLCV data  
   - Exogenous variables: Dollar Index, WTI Oil prices  
   - Technical indicators derived from trading data  

2. **Preprocessing**  
   - Compute log returns  
   - Apply Adaptive Wavelet Transform for noise reduction  
   - Conduct stationarity & long memory tests  
   - Fit ARIMAX-FIEGARCH for conditional mean & volatility  

3. **Feature Engineering**  
   - Select important trading indicators with XGBoost  
   - Add lagged returns and exogenous variables  
   - Normalize and scale inputs  

4. **LSTM Modeling**  
   - Multi-layer LSTM with adaptive weighting for wavelet components  
   - Hyperparameter tuning (layers, neurons, dropout, etc.)  
   - Rolling window evaluation for multiple forecast horizons  

5. **Ensemble Forecasting & Evaluation**  
   - Nonlinear integration of wavelet components using Random Forest  
   - Evaluate forecasts using RMSE, MAE, R², SMAPE  
   - Benchmark against traditional models  

---

## 🛠️ Tech Stack
- **Languages:** Python (primary), R (optional for econometrics)  
- **Core Libraries:**  
  - Data: `pandas`, `numpy`  
  - Econometrics: `statsmodels`, `arch`  
  - Machine Learning: `scikit-learn`, `xgboost`, `tensorflow/keras`  
  - Signal Processing: `pywavelets`  
  - Bloomberg Data Access: `blpapi`  
- **Environment:** Jupyter Notebooks (via Anaconda), GitHub for version control  

---

## 📈 Progress
- [x] Set up repository and environment  
- [x] Created first Jupyter notebook  
- [ ] Implement data acquisition from Bloomberg, Yahoo Finance, LSEG or CRSP  
- [ ] Preprocess and denoise time series  
- [ ] Fit ARIMAX-FIEGARCH models  
- [ ] Build and train LSTM  
- [ ] Integrate hybrid forecasting system

### Table X: EGARCH(2,1)-t Model Diagnostic Summary

| Metric | Value | Interpretation |
|:--|--:|:--|
| **Model** | EGARCH(2,1)-t | Chosen specification (best AIC/BIC) |
| **Distribution** | Student-t | Captures heavy tails and fat-tailed shocks |
| **AIC** | 10006.60 | Lowest among tested models → best parsimony-fit balance |
| **BIC** | 10044.23 | Consistent with AIC → supports model selection |
| **Leverage (γ[1])** | -0.1724 | Negative and significant → leverage effect present |
| **p-value (γ)** | 2.7e-32 | Highly significant asymmetry (p < 0.001) |
| **Ljung–Box p (lag 10)** | 0.00049 | Mild serial correlation remains in standardized residuals |
| **Ljung–Box p (lag 20)** | 0.00042 | Same as above – likely mean model effect |
| **ARCH LM p (lag 12)** | 0.64 | No remaining heteroskedasticity (model well-specified) |
| **Overall Assessment** | ✅ Good | Volatility and asymmetry well captured; mild autocorrelation acceptable |
