# L06 — Time Series Forecasting: Knowledge Check (10 MCQs)

**Q1. Time series data violates a core assumption made by every supervised lesson before L06. Which one?**

- A. That features are normally distributed
- B. That observations are independent and identically distributed (i.i.d.)
- C. That the target variable is continuous
- D. That there are more rows than columns

**✅ Answer: B** — Today's value depends on yesterday, last week, and last year, so rows are *not* independent and cannot be shuffled freely.

---

**Q2. Because time series breaks i.i.d., which practice is NOT safe to use?**

- A. Quoting a forecast as a range rather than a single point
- B. Decomposing the series before forecasting
- C. Random k-fold cross-validation
- D. Comparing against a seasonal naive baseline

**✅ Answer: C** — Random shuffling / k-fold leaks future data into the past. Order must be preserved.

---

**Q3. STL decomposition separates a series into which three components?**

- A. Mean, variance, and noise
- B. Trend, seasonality, and residual
- C. Level, slope, and curvature
- D. Lag, lead, and difference

**✅ Answer: B** — Every series = trend + seasonality + residual.

---

**Q4. After running STL, the residual still shows a clear repeating oscillation. What does this most likely mean?**

- A. The decomposition is perfect and ready to forecast
- B. The trend was modelled incorrectly
- C. A seasonality was missed — the wrong/incomplete period was specified
- D. The data must be log-transformed

**✅ Answer: C** — A leftover pattern in the residual means a seasonal period the model didn't capture (e.g., use a longer period or MSTL).

---

**Q5. Why does an STL plot show four panels rather than three?**

- A. The fourth panel is the forecast
- B. The fourth panel is the original series, so you can verify trend + seasonal + residual ≈ original
- C. The fourth panel shows the confidence interval
- D. The fourth panel is a duplicate of the residual

**✅ Answer: B** — Panels are: original, trend, seasonal, residual.

---

**Q6. Why should you always run a trivial baseline (Naive / Seasonal Naive) first?**

- A. It is required by the statsmodels library
- B. It guarantees the lowest possible error
- C. It is the bar every fancier model must clear — if it wins, the simple model is the answer
- D. It is the only model that handles seasonality

**✅ Answer: C** — Baselines are cheap, honest, and must appear on the comparison table with the same split and metric.

---

**Q7. For a clean series with a single, stable seasonality, which method is described as the pragmatic default for classical forecasting?**

- A. ETS / Holt-Winters
- B. HistGradientBoostingRegressor
- C. Linear regression on raw dates
- D. Random forest with shuffled folds

**✅ Answer: A** — ETS models level + trend + seasonality with three intuitive knobs, fits in seconds, and is hard to beat on clean single-seasonality data.

---

**Q8. When you have multiple seasonalities or exogenous signals, what is the recommended reframing?**

- A. Drop the seasonal components entirely
- B. Reframe as tabular regression using lag features (e.g., lag_1, lag_7, lag_365) plus calendar features
- C. Increase the STL period until the residual is flat
- D. Switch to random k-fold cross-validation

**✅ Answer: B** — Build lag + calendar features and let HistGradientBoosting handle the rest, using the same sklearn pipeline you already know.

---

**Q9. Should you scale lag features before feeding them to a HistGradientBoosting model?**

- A. Yes — always standardize features for any model
- B. Yes — gradient boosting requires zero-mean features
- C. No — tree-based models are insensitive to feature scale (scaling matters for neural networks)
- D. No — but you must one-hot encode them first

**✅ Answer: C** — Trees split on thresholds, so scale doesn't matter; scaling is needed for neural networks.

---

**Q10. Your GB forecaster gives RMSE = £500 on training but RMSE = £2000 on a 30-day held-out test. Which is the best interpretation?**

- A. The model is perfectly calibrated
- B. Possible overfitting, or the test period is a different regime (e.g., a holiday season) — inspect test residuals for systematic bias
- C. RMSE is the wrong metric and should be ignored
- D. The training set was too small and nothing can be done

**✅ Answer: B** — A large train/test gap signals overfitting or a regime shift; check residuals and consider more regularisation or features.
