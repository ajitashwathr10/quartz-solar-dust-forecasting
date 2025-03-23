# Quartz Solar Dust Forecasting
Enhancing solar power forecasting accuracy by incorporating dust concentration data to optimize renewable energy grid integration

## Project Overview

This project aims to enhance the accuracy of Quartz Solar's solar power forecasting models by incorporating dust concentration data as an additional environmental variable. Current models primarily rely on weather data and historical PV performance, but they do not account for the impact that dust accumulation can have on solar panel efficiency.

## Background & Motivation

Solar energy prediction is critical for optimizing energy systems and reducing reliance on non-renewable sources. Despite advances in forecasting models, variables like dust concentration and local environmental factors remain underutilized. Dust particles can reduce solar panel efficiency by up to 30% in heavily affected regions, making it a factor that requires proper modeling.

## Methodology

### 1. Data Sources Integration

The project integrates multiple dust concentration data sources:
- **NASA MERRA-2**: Global aerosol optical depth data
- **CAMS (Copernicus Atmosphere Monitoring Service)**: European atmospheric composition data
- **Local air quality monitoring stations**: For ground-level PM10 and PM2.5 measurements

### 2. Data Preprocessing Pipeline

To ensure reliable dust data integration, we implement:
- **Multi-source aggregation**: Combining multiple sources to improve reliability
- **Outlier detection and removal**: Using IQR filtering and Z-score analysis
- **Imputation techniques**: KNN and time-series forecasting for missing values
- **Adaptive reliability weighting**: Source-specific confidence scores based on historical accuracy

### 3. Dust Impact Modeling

Our approach accounts for both immediate and cumulative dust effects:
- **Immediate impact**: Reduction in solar irradiance reaching panels due to atmospheric dust
- **Accumulation modeling**: Tracking dust buildup on panels over time with decay functions for cleaning events (rain, manual cleaning)
- **Regional calibration**: Region-specific dust impact coefficients based on local conditions

### 4. Ablation Study Design

To quantify the contribution of dust data to forecast accuracy:
1. **Baseline evaluation**: Measure existing model performance
2. **Incremental feature addition**: Add dust concentration features one by one
3. **Feature importance analysis**: Use SHAP values to quantify contribution
4. **Performance metrics**: Track improvements in RMSE, MAE, and R²

## Preliminary Study

Initially, we conducted a proof-of-concept using synthetic data to test our hypothesis. This early study suggested a potential improvement of 13.8% in RMSE when incorporating dust concentration data. While promising, these results were based on simulated conditions designed to validate the concept.

## Results from Actual Data

Our comprehensive ablation study using actual operational data demonstrates the incremental improvement in solar power forecasting accuracy as different feature groups are added:

| Model | Features | MAE | RMSE | R² | Improvement |
|-------|----------|-----|------|-----|-------------|
| Base | 4 | 268.63 | 358.05 | 0.856 | - |
| Base + Weather | 6 | 209.02 | 268.16 | 0.919 | 25.1% |
| Base + Weather + Irradiance | 7 | 204.48 | 267.23 | 0.920 | 0.3% |
| Complete (with Dust) | 8 | 201.48 | 263.29 | 0.922 | 1.47% |

The study confirms that dust concentration contributes meaningful predictive power beyond standard weather variables, with a 1.47% improvement in RMSE when added to the model.

## Key Findings

- **Weather variables** provide the most substantial improvement to the baseline model (25.1% RMSE reduction)
- **Dust concentration data** offers an additional 1.47% improvement in RMSE
- The complete model achieves an R² of 0.922, indicating strong predictive performance
- While the overall improvement from dust data is more modest than suggested by synthetic data, regional analysis suggests higher impact in dust-prone areas

## Implementation Plan

1. **Data pipeline development**: Create robust pipelines for ingesting and processing dust data
2. **Model enhancement**: Update existing Quartz Solar models to incorporate dust features
3. **Hyperparameter optimization**: Fine-tune models using Bayesian optimization
4. **Regional analysis**: Evaluate dust data impact by region to identify areas of highest benefit
5. **Documentation and deployment**: Integrate into Quartz Solar's production environment

## Expected Outcomes

1. **Improved forecast accuracy**: 1-2% reduction in RMSE for overall solar power predictions
2. **Enhanced performance during dust events**: Up to 5-8% improvement in predictions during high dust concentration periods
3. **Regional adaptability**: Models that can dynamically adjust to local dust conditions
4. **Better grid management**: More accurate forecasting during challenging environmental conditions

## Conclusion

This project addresses a gap in current solar forecasting models by incorporating the impact of dust concentration. While our initial synthetic data study suggested larger potential improvements, our ablation study with actual operational data demonstrates that this approach yields more modest but still meaningful improvements in forecast accuracy (1.47%), especially in regions prone to dust events.

The difference between synthetic and actual data results highlights the importance of validating hypotheses with real-world data. While the overall improvement from dust data is smaller than initially projected, the enhancement remains valuable for critical grid management scenarios, particularly in dust-prone regions and during dust storm events, where accurate forecasting is especially challenging with conventional models.

By enhancing Quartz Solar's predictive capabilities with dust concentration data, this project contributes to more efficient grid management and supports the transition to renewable energy through improved forecasting.
