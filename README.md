# Modeling ERCOT FTR Prices
## Problem
Given ERCOT FTR data for unknown nodes, find any relationships, provide interpretations, and produce out-of-sample predictions for contract values using system features (loads, wind, line ratings).
## Data
Inputs (CSV): contract_data.csv, line_ratings.csv, load.csv, wind.csv
* Hourly ERCOT FTR contract values for unspecified nodes from 2019 to October 2021 
* Corresponding hourly zonal load and wind data, as well as line ratings
* See code for details on preprocessing
## Approach 
Build predictive models for contract values using 80/20 train/test split
* Lasso Linear - disciplined regression to handle strong collinearity among system features and avoid overfitting while providing simplicity and interpretable coefficients
* Random Forest Regressor - ensemble of decision trees to model nonlinearities and interaction effects and still providing some interpretability 
## Results
Strong correlation with panhandle wind and line capacity
* Suggests that this specific FTR contract is between a node in the panhandle and a load center to the South, perhaps DFW
    * The Texas panhandle is a hotspot for wind energy development, suggesting the possibility that the panhandle line reaches capacity and results in grid congestion
    * Locational prices around the binding line diverge, possibly flipping negative in the panhandle and incentivizing curtailment from wind turbines
    * This is consistent with a strong positive correlation between contract value and panhandle wind, and a negative correlation with the line rating
## Improvements
* Implement time-ordered splits as opposed to random splits, which would prevent look-ahead leakage and mimic production
* Spend time on hyperparameter tuning for random forest (n_estimators, max_depth, max_features, min_samples_leaf) to improve model performance and stability
