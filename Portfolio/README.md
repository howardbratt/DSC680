# DSC680 Applied Data Science Portfolio

**Shelia Howard | Master of Data Science | Bellevue University**

This portfolio brings together ten projects from my Master of Data Science program. The work spans statistical modeling, research ethics, data preparation, predictive analysis, visualization, and generative AI. My two DSC680 projects apply those skills to hospital quality improvement and bike rental operations.

## Portfolio at a glance

| #   | Project                                                                                     | Course             | Focus                               |
| --- | ------------------------------------------------------------------------------------------- | ------------------ | ----------------------------------- |
| 1   | [Comparing Linear Regression Models for Housing Prices](#1-comparing-linear-regression-mod  | DSC520 ·           | Regression diagnostics and model    |
|     | els-for-housing -prices)                                                                    | Statistics for     | comparison                          |
|     |                                                                                             | Data Science       |                                     |
| 2   | [Bias and Ethics in Healthcare Research](#2-bias-and-ethics-in-healthcare-research-the-tus  | DSC520 ·           | Participant selection,              |
|     | kegee-syphilis-s tudy)                                                                      | Statistics for     | generalizability, and research      |
|     |                                                                                             | Data Science       | ethics                              |
| 3   | [Factors Influencing Healthcare Costs](#3-factors-influencing-healthcare-costs)             | DSC530 · Data      | Exploratory analysis and            |
|     |                                                                                             | Exploration and    | predictionof insurance charges      |
|     |                                                                                             | Analysis           |                                     |
| 4   | [County-Level Health Data Preparation](#4-county-level-health-data-preparation)             | DSC540 · Data      | Data cleaning, SQLite, and SQL      |
|     |                                                                                             | Preparation        | joins                               |
| 5   | [Machine Learning with Diabetes Encounter Data](#5-machine-learning-with-diabetes-encounte  | DSC550 · Data      | 30-day readmission prediction and   |
|     | r-data)                                                                                     | Mining             | subgroup performance                |
| 6   | [Stroke Risk Prediction](#6-stroke-risk-prediction)                                         | DSC630 ·           | Predictive modeling for preventive  |
|     |                                                                                             | Predictive         | outreach                            |
|     |                                                                                             | Analysis           |                                     |
| 7   | [Visualizing Childcare Affordability](#7-visualizing-childcare-affordability)               | DSC640 · Data      | Audience-specific communication and |
|     |                                                                                             | Presentation &     | county screening                    |
|     |                                                                                             | Visualization      |                                     |
| 8   | [Healthcare Data Mapping Assistant](#8-healthcare-data-mapping-assistant)                   | DSC670 · Advanced  | Fine-tuning, structured responses,  |
|     |                                                                                             | Uses of            | and analyst review                  |
|     |                                                                                             | GenerativeAI       |                                     |
| 9   | [Hospital Readmission Penalty Risk](#9-hospital-readmission-penalty-risk)                   | DSC680 · Applied   | Hospital and condition-level        |
|     |                                                                                             | Data Science,      | readmission performance             |
|     |                                                                                             | Project 1          |                                     |
| 10  | [Bike Demand Forecasting for Operational Planning](#10-bike-demand-forecasting-for-operati  | DSC680 · Applied   | Hourly demand forecasting and       |
|     | onal-planning)                                                                              | Data Science,      | operational planning                |
|     |                                                                                             | Project 2          |                                     |

## Projects

### 1. Comparing Linear Regression Models for Housing Prices

This analysis compares nested linear regression models for housing prices. It documents data preparation, uses residual diagnostics to assess model assumptions, and tests whether the additional predictors improve model fit.

[Link to the project README and final R analysis using paths relative to this file. Name the housing dataset, the models compared, and the conclusion of the nested-model test.]

### 2. Bias and Ethics in Healthcare Research: The Tuskegee Syphilis Study

This paper examines how participant selection affects the generalizability of research findings and considers the consequences of decisions about consent and treatment in the Tuskegee Syphilis Study.

[Link to the project README and final paper. Add one sentence stating the paper’s central conclusion if you want to highlight it here.]

### 3. Factors Influencing Healthcare Costs

Using the Medical Cost Personal Dataset, this project explores how demographic and behavioral characteristics relate to medical insurance charges. It uses statistical and machine learning methods to assess which variables are most strongly associated with charges and how well they predict them.

[Link to the project README and final notebook. Identify the exploratory methods and report one observed pattern or model result from the notebook.]

### 4. County-Level Health Data Preparation

This notebook loads three cleaned county-level health datasets into separate SQLite tables, joins them with SQL, and creates five visualizations from the combined data. It uses cleaned records from earlier milestones to demonstrate the database, join, and visualization workflow in one notebook.

[Link to the project README and final notebook. Confirm which CDC PLACES release was used, name the other two datasets, and identify the county join key and where the cleaned inputs are available.]

### 5. Machine Learning with Diabetes Encounter Data

The notebook and paper use the UCI Diabetes 130-US Hospitals dataset, which covers encounters from 1999 through 2008. The analysis derives a binary 30-day readmission outcome from the original `readmitted` field and considers how model performance varies across demographic groups.

[Link to the project README, final notebook, and paper. Summarize the evaluation split, the strongest model and its metric, and one subgroup finding or limitation.]

### 6. Stroke Risk Prediction

This project uses 5,110 records from the Stroke Prediction Dataset published on Kaggle by Fedesoriano. It evaluates whether demographic, medical, and lifestyle variables can support prioritization for preventive outreach. The analysis is a course proof of concept based on a binary recorded-stroke outcome.

[Link to the project README and final analysis. Name the models compared, describe how class imbalance was handled, and report an evaluation result and a limitation relevant to outreach.]

### 7. Visualizing Childcare Affordability

Using the National Database of Childcare Prices, this project presents affordability as a workforce development concern. The final notebook documents preparation and assumptions and brings together a five-slide executive presentation, a county screening dashboard, a one-page public infographic, and the final paper. The three formats use the same evidence and tailor the detail and call to action to their audiences. Affordability and workforce measures serve as screening criteria for a proposed local pilot.

[Link to the project README and final notebook. Add direct links to the presentation, dashboard, and infographic if they are available separately. Identify one finding shared across the three formats.]

### 8. Healthcare Data Mapping Assistant

This Streamlit prototype recommends one of 13 approved demographic fields or returns `REVIEW` for an analyst. It accepts source field metadata, provides a rationale, and records the analyst’s decision separately. I fine-tuned the model with Hugging Face Transformers on synthetic examples. On 48 held-out cases, it returned the correct target or review decision in 41 cases and met the JSON response requirements in all 48. The project README documents local setup and the checkpoint needed for live inference.

[Link to README.md for DSC670](https://github.com/howardbratt/DSC680/blob/37d4921dcac3e5032192774dfd970f96cc5cefbb/Portfolio/DSC670/README.md)
[Link to DSC670 Folder](https://github.com/howardbratt/DSC680/tree/37d4921dcac3e5032192774dfd970f96cc5cefbb/Portfolio/DSC670)

### 9. Hospital Readmission Penalty Risk

This DSC680 project uses public data from the Centers for Medicare & Medicaid Services to examine 30-day readmission performance by hospital and condition. It compares logistic regression with tree-based models using hospital characteristics, condition type, and discharge volume. The analysis is intended to help hospital quality teams identify conditions for further review.

[Link to the project README and available deliverables. Confirm the CMS data release and study period, then add the final evaluation result if available.]

### 10. Bike Demand Forecasting for Operational Planning

Using hourly Capital Bikeshare rental data, this DSC680 project compares ridge regression and random forest models with calendar inputs and with calendar plus observed weather inputs. Observed weather reduced test error for both models. Among hours when the selected calendar model underestimated demand, the largest average shortfall was about 292 rentals at 8 a.m. The project recommends reviewing morning staffing and bike reserves and testing on recent data before changing operations.

[Link to the project README, final notebook, white paper, and presentation. Add the recording link if it is included in the portfolio.]

## Viewing the portfolio

The project entries provide an overview of the question, approach, and available evidence. Use the linked notebooks, papers, and presentations to inspect the analysis. For projects with executable code, consult the project README for dataset access, software requirements, and run instructions.

[Link to Portfolio Github Page](https://howardbratt.github.io/DSC680/)
