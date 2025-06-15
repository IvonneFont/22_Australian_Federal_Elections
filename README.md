# Australian Federal Election 2022: Voter Segmentation and Vote Prediction

## Project Overview

In this capstone project, I analyzed Australian federal election data to uncover patterns in voter behavior. The goal was twofold:

- Identify meaningful voter segments based on demographics, political attitudes, and policy priorities using clustering techniques.
- Build and evaluate multi-class classification models to predict whether a voter supports the Labor Party, the Coalition, or a minor/independent party (Other).

## Dataset

- **Source:** The Australian Election Study (AES), conducted by the Australian National University (ANU), School of Politics and International Relations.
- **File:** `aes22_unrestricted_v3.csv`
- **Sample size:** ~2,400 voters (subset of full survey)
- **Features Used:** 29 features selected from over 350 available variables. Full data dictionary provided in project appendix.
- **Variables included:**  
  - Demographics (age, gender, income, education, residence)
  - Political engagement and attitudes
  - Government spending preferences
  - Top political issues
  - Socio-economic class and policy priorities

## Methodology

### Exploratory Data Analysis (EDA)

- Univariate, bivariate, and aggregate analysis
- Grouping and cross-tabulations to explore relationships between features and vote preferences

### Clustering (Unsupervised Learning)

- **Algorithm:** Fuzzy C-Means Clustering
- Applied to subsets of variables grouped by theme (demographics, attitudes, spending priorities, top issues)
- Variables encoded with MinMaxScaler and One-Hot Encoding
- Optimal number of clusters determined using Fuzzy Partition Coefficient (FPC)

### Classification (Supervised Learning)

- **Target:** First vote preference (Labor, Coalition, Other)
- Feature selection using Recursive Feature Elimination (RFE)
- Three classification models:
  - Multinomial Logistic Regression (interpretable baseline model)
  - Random Forest Classifier (non-linear model with hyperparameter tuning)
  - XGBoost Classifier (gradient boosting model with hyperparameter tuning)

- Hyperparameter tuning performed using `GridSearchCV`
- Threshold tuning based on ROC Curve analysis

## Key Findings

### Clustering Analysis

- Identified distinct voter segments based on:
  - Age group, income, education, residence
  - Spending priorities (health, education, environment, defense, welfare)
  - Top political issues (economy, environment, immigration, etc.)

### Classification Models

#### Logistic Regression

- Most interpretable model; clearly showed how spending preferences, demographics, and issue priorities relate to vote choice.
- Struggled to predict "Other" voters.
- Lower overall accuracy despite threshold tuning.

#### Random Forest

- Improved recall for "Other" voters.
- Captured more complex non-linear patterns, especially for label-encoded variables.

#### XGBoost

- **Best overall model performance:**
  - Accuracy: **61%**
  - ROC AUC (Coalition voters): **0.86**
  - Most balanced classification across all three voter groups.
- Captured complex feature interactions and subtle patterns in voter behavior.

### Overall Insights

- Predicting individual voting behavior remains challenging due to its complexity.
- Both clustering and classification revealed that voter decisions are structured but multi-dimensional.
- Feature importance varied across models:
  - Logistic Regression explained high-level ideological divides.
  - Tree-based models (Random Forest & XGBoost) were better at identifying nuanced or marginal voter behavior, especially for minor parties.
  - Top issues (policy priorities) ranked much higher in importance in tree-based models.

## Tools Used

- Python (Pandas, NumPy, Scikit-learn, SciPy, XGBoost, Matplotlib, Seaborn)
- Fuzzy C-Means Clustering (`scikit-fuzzy`)
- Recursive Feature Selection (RFE)
- Random Forest Classifier
- XGBoost Classifier
- GridSearchCV for hyperparameter tuning
- ROC Curve & Threshold Optimization

## Future Work

- **Expand feature set:** Incorporate additional AES survey features such as media consumption, political knowledge, institutional trust, or issue-specific attitudes.
- **Improve sample balance:** Obtain larger samples of younger voters for better representation.
- **Longitudinal Analysis:** Extend the study to multiple AES waves (1987-2022) to examine trends over time and detect long-term shifts in voter behavior.

