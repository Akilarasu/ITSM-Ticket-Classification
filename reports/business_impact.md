# Business Impact & Modeling Philosophy

## Data Integrity & Imbalance Handling Strategy

This project preserves the real operational structure of IT Service Management (ITSM) data.  
Techniques such as SMOTE were intentionally avoided at the dataset level to prevent introducing synthetic incidents that do not reflect real production behavior.

ITSM environments naturally contain strong class imbalance:

- Priority-1 / Priority-2 incidents are rare but high impact
- RFC generation events are infrequent
- Change failures occur at low rates (≈5%)
- Some routing categories have very low volume

Instead of artificially balancing the dataset, cost-sensitive learning approaches were applied:

- `class_weight='balanced'` (Logistic Regression, Random Forest)
- `scale_pos_weight` (XGBoost, LightGBM)

This ensures rare but critical operational events are detected without distorting the real distribution of the IT environment.

## Evaluation Philosophy Based on Business Risk

Accuracy was not used as the primary evaluation metric due to severe class imbalance.  
Instead, metrics were selected based on operational risk.

### High-Priority Incident Prediction (≈99:1 imbalance)

- Focused on **Recall and F1-score**
- Objective: Detect true critical incidents without excessive false alarms
- Accuracy was avoided because a naive model could achieve ~99% by predicting all tickets as low priority

### Incident Volume Forecasting

- Daily incident counts showed weekly seasonality and outage-driven spikes
- One-year forecasting produced unstable projections
- A **six-month forecasting horizon** was selected to align with:
  - Workforce planning
  - Shift rotation
  - Capacity management
- Models compared: Naive baseline, SARIMA, Prophet, LightGBM
- MAE used as evaluation metric due to skewed spikes

### Auto-Tagging & Smart Routing

- Multi-class classification problem
- Extremely rare categories were consolidated into an “Others” class
- Evaluated using **Macro F1-score** to ensure fair performance across departments
- Accuracy was not used alone due to class imbalance

### RFC Generation Prediction (≈44,701 : 525 imbalance)

- Highly imbalanced target
- Evaluated using Recall and F1-score
- Objective: Avoid missing change-related risk events

### Change Failure Prediction (≈95:5 imbalance)

- Most changes succeed, but a small fraction cause major disruption
- Recall prioritized over accuracy
- Goal: Identify risky changes without overwhelming operations with false alerts

## Key Operational Insights

### Software & Application Layers Drive Most Risk

Software-related configuration items generated the highest RFC rates, indicating that digital platforms and application releases are the primary drivers of operational change.

### Emergency & High-Priority Changes Are Riskier

Priority-1 and Priority-2 changes exhibited significantly higher failure rates.  
This confirms that urgent and rushed changes introduce instability and should undergo stricter governance and validation.

### Behavioral Patterns of Failed Changes

Failed changes typically show:

- Higher reassignment counts
- More related follow-up incidents
- Repeated change activity
- Longer resolution and closure times

These patterns validate the engineered features used in the predictive models.

### Rare Systems Carry Higher Operational Risk

Frequency-encoded CI categories revealed that low-volume systems tend to have higher instability.  
This may be due to:

- Limited expertise
- Poor documentation
- Weaker automation

### Short-Term Forecasting Is More Actionable

Six-month forecasts provide stable, practical insight for:

- Staffing decisions
- On-call scheduling
- Capacity planning

Long-term forecasts introduce speculative volatility and reduced reliability.

## Overall Business Value

This project demonstrates how predictive modeling can enhance ITSM operations by:

- Improving SLA adherence through early critical incident detection
- Enabling proactive workforce planning through volume forecasting
- Reducing manual triaging through automated routing
- Minimizing production outages through change risk prediction

All models were built using real operational data without artificial manipulation, ensuring realistic and production-aligned insights.
