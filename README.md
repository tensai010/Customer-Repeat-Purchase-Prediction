# Customer-Repeat-Purchase-Prediction
This project predicts whether an existing customer will purchase again within 30 days using shopping behaviour, loyalty activity and historical campaign features.

Business question
A retention team has limited campaign capacity. The useful question is whether historical customer behaviour can help prioritize customers who are more likely to return.

Approach
1. Created a majority class baseline
2. Used a stratified train and test split
3. Standardized numeric variables and encoded loyalty tier
4. Evaluated Logistic Regression with five fold stratified cross validation
5. Compared it with a constrained Decision Tree
6. Compared it with a Random Forest
7. Tuned the Logistic Regression probability threshold using out of fold predictions
8. Evaluated the selected model once on the holdout test set
9. Reviewed coefficients for directional interpretation
10. Saved the fitted model, preprocessing pipeline and selected threshold
    
Model comparison
Logistic Regression validation ROC AUC: 0.658
Decision Tree validation ROC AUC: 0.611
Random Forest validation ROC AUC: 0.659
Random Forest produced almost the same validation ROC AUC as Logistic Regression, but its training ROC AUC was 0.780 compared with 0.659 on validation. 
I therefore kept Logistic Regression because it was simpler to interpret and had a smaller training to validation gap.

Threshold choice
The default 0.50 threshold had low recall.
Among the thresholds tested, 0.25 produced the strongest validation F1.
At 0.25:
- validation precision: 39.3%
- validation recall: 72.6%
- validation F1: 0.510
Final holdout result

At the selected 0.25 threshold:
- precision: 35.5%
- recall: 69.6%
- F1: 0.470
- ROC AUC: 0.605
- 71 of 102 repeat buyers were identified
- 200 customers were flagged in total

The model is more appropriate as a prioritization tool for inexpensive outreach than as an automated campaign decision engine.

Main learning:
Prediction and causality are different questions.
Historical campaign assignment has a positive Logistic Regression coefficient, but that does not prove the campaigns caused repeat purchases. Customers may have been selected for campaigns because they were already more engaged.
Tools
Python, pandas, scikit learn, Jupyter Notebook, Logistic Regression, Decision Tree, Random Forest, stratified cross validation, threshold tuning

Limitations
- synthetic dataset
- modest holdout ROC AUC
- one holdout split rather than future time period validation
- no causal estimate of campaign impact

Next steps
- validate on later customer periods
- evaluate probability calibration
- connect threshold selection to expected campaign economics
- monitor stability and model drift
