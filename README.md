# Wisconsin_Breast_Cancer_Predictions
*https://www.kaggle.com/datasets/uciml/breast-cancer-wisconsin-data*

Last Updated: 06/08/24

**Outstanding Tasks**
1. Add an *Index* to this README.md
2. Adding docustrings to all functions, checking formatting and return statements
3. Ensure notebook is properly notated, left off at Single-Feature modeling
4. *Consider* adding .img of modeling results?


**Index**


## Analysis Goal
"Predict whether the cancer is benign or malignant"


### EDA
- Basic EDA
    - Built out functions create_histogram_ax() and create_subplot_grid() to create grids of histogram plots, with axvline for mean and median, to understand distibution of data
        - Need to add docustrings to better document what the functions accomplish
- Hypothesis Tests
    - Pearson Correlation
        - calculate_pearson_and_significance() to create DataFrame of Pearson correlation coefficients and signficance of values, for relationships between features
        - visualize_correlation_heatmap() visualizes coefficients from calculate_pearson_and_significance() results as an *n x n* heatmap
        - print_non_significant_relationships() to return the relationships that were not significant - not used at this time
    - Point Biserial Correlation (special case of Pearson Correlation) 
        - calculate_pointbiserial_and_significance() to create DataFrame of Point Biserial correlation coefficients and significance of values, for relationships with respect to outcome
        - visualize_singlecol_corr_heatmap() visualizes coefficients from calculate_pointbiserial_and_significance() results as an *n x 1* heatmap
    - T-Tests
        - calculate_t_test() to create DataFrame of t-test results, including means of individual groups and difference between means

     
### Modeling
- Single-Feature Logistic Regression
    - single_feature_logistic_regression() to run Logistic Regression models with one feature predicting the outcome, returns a DataFrame of results and optional scatterplots showing the predictions based on feature value
- Multivariate Logistic Regression
    - fit_lasso_logistic_regression() to run multivariate Logistic Regression with LASSO regularization, returns training and testing data as well as a dictionary of modeling results
    - plot_roc_curve() to plot a ROC curve and AUC score for modeling results returned by fit_lasso_logistic_regression()
    - visualize_confusion_matrix() to visualize the Confusion Matrix of model's predictions
    - plot_odds_ratios() to visualize the feature importance of the model, displaying coefficients as Odds Ratios


## Results
- EDA
    - Basic EDA: Visual representations of features' distributions available in notebook file
 
    - Hypothesis Tests
        - Pearson Correlation: Some features are highly correlated to one another, while others have no relationship. While this information could be used to address multicolinearity, no action will be taken with these results
        - Point Biserial Correlation: The following features had no (significant) relationship to the target 'diagnosis'

| Feature | Correlation Coef. |
| -------- | ------- |
| fractal_dimension_se | 0.08 |
| symmetry_se | -0.01 |
| texture_se | -0.01 |
| fractal_dimension_mean | -0.01 |
| smoothness_se | -0.07 |


- EDA (con't)
    - T-Tests: The following features had no (significant) differences in means when stratified by 'diagnosis'

| Feature | T-Stat | Difference in Means |
| -------- | ------- | ------- |
| fractal_dimension_se | -1.862330 | 0.000426 |
| symmetry_se | 0.155298 | -0.000111 |
| texture_se | 0.197724 | -0.009465 |
| fractal_dimension_mean | 0.305711 | -0.000187 |
| smoothness_se | 1.599365 | -0.000416 |


- Modeling
    - Single-Feature Logistic Regression: The following features were highly predictive of 'diagnosis' on their own (accuracy >= 90%)
 
| Feature |	Accuracy | Coefficient | Intercept | Odds Ratio |
| -------- | ------- | ------- | ------- | ------- |
| perimeter_worst| 0.964912	| 0.161997 | -17.862242 | 1.175856 |
| radius_worst | 0.938596 | 1.054382 | -17.565511 | 2.870199 |
| area_worst | 0.938596	| 0.010865 | -9.285249 | 1.010924 |
| perimeter_mean | 0.929825	| 0.151145 | -14.526079 | 1.163165 |
| area_mean	| 0.921053 | 0.010872 | -7.414512 | 1.010931 |
| area_se | 0.921053 | 0.123675 | -4.540850 | 1.131648 |
| radius_mean | 0.912281 | 0.948621	| -14.036740 | 2.582146 |


- Modeling (con't)
    - Multivariate Logistic Regression: Using LASSO regularization, we were able to go from 27 significant features to 15 features necessary to predict a tumor's malignancy with 97% accuracy
        - Feature Importance results are visualized as Odds Ratios, available in the notebook



