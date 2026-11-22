Factors Associated with Medical Insurance Charges

Author
Shelia Howard

Project overview
This project explores which characteristics are associated with medical
insurance charges and compares two approaches to predicting charges.

Data
The final paper identifies the public Medical Cost Personal Dataset and
reports 1,338 observations with no missing values. The outcome is medical
charges. The candidate predictors are age, sex, body mass index (BMI),
number of children, smoking status, and region.

Methods
The paper describes exploratory visualizations, a numeric correlation
matrix, a two-sample t test comparing mean charges by smoking status,
multiple linear regression, and random forest regression. It also reports
using cross-validation to assess the random forest.

Findings reported in the paper
- Charges were right-skewed. Smokers had higher median charges and more
  variability than nonsmokers.
- Mean charges differed by smoking status (p < .001). Correlations with
  charges were approximately 0.30 for age and 0.20 for BMI.
- Smoking status had the largest reported association in the linear
  model. The paper reports lower RMSE for the random forest. Exact scores
  and a common evaluation setup for both models still need verification.

Interpretation
The results describe associations in this dataset. They do not establish
causation or show that either model will generalize to other populations.

How to review
Open "Factors Influencing Healthcare Costs.pdf". Figure 1 compares charges by
smoking status, and Figure 2 shows the numeric correlation matrix.

Reproducibility
The supplied notebook PDF contains separate wine and astronomy exercises.
Before publishing a runnable version, add the matching healthcare costs
notebook, verify the dataset URL and terms, record the dependencies and
run steps, and rerun both models on a common evaluation setup to confirm
the reported comparison.
