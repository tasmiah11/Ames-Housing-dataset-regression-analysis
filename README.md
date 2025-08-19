📊 Ames-Housing-Dataset-Regression-Analysis

Ames House Price Analysis

This project analyzes the Ames Housing dataset to predict house prices through rigorous regression modeling. It demonstrates the full lifecycle of a data analysis project — from variable screening and exploratory data analysis (EDA) to model diagnostics and final model selection.

📌 Project Overview

The Ames dataset is widely used as a benchmark for predictive modeling, containing over 80 variables describing residential homes in Ames, Iowa.

Objective:

Identify the strongest predictors of housing prices.
Build parsimonious regression models that balance predictive performance with interpretability.

⚙️ Workflow
1. Setup
Loaded R packages: tidyverse, janitor, broom, car, MASS, leaps, GGally, e1071
Established reproducibility (set.seed(42))
Applied global plotting themes

2. Data Preparation
Imported AmesHousing.csv
Dropped identifiers (Order, PID) not suitable for modeling
Converted character fields to categorical factors
Validated data types

3. Variable Screening
Numerical variables:
Correlation and significance testing with SalePrice
Retained variables with |correlation| > 0.30 and p < 0.05
Categorical variables:
One-way ANOVA on SalePrice
Retained significant factors
Produced an initial candidate pool of explanatory variables

4. Exploratory Data Analysis (EDA)
Missing Values:
Removed features with ≥30% missingness
Imputed numerics using mean/median depending on skewness
Imputed categoricals using mode
Special case: imputed Lot.Frontage by neighborhood median
Outliers:
Identified using IQR rule
Flagged extreme values in living area and basement size
Visualization:
Histograms, scatterplots, and boxplots for key predictors vs SalePrice

5. Feature Engineering
Log-transformed SalePrice and skewed predictors
Created dummy variables for categorical predictors (e.g., Lot.Shape, Land.Contour)
Derived composite indicators where appropriate

6. Model Development
Built full regression models with shortlisted predictors
Checked multicollinearity (VIF)
Applied model selection methods:
Stepwise selection (MASS::stepAIC)
Best subset selection (leaps::regsubsets)
Constructed three tiers of models (Option 1–3) to compare parsimony vs explanatory power

7. Model Diagnostics
Residual vs fitted plots, Q-Q plots, and leverage analysis
Influential observations flagged via Cook’s distance
Compared transformations (log vs sqrt) to improve homoscedasticity and normality

📈 Results
We evaluated three progressively reduced models to balance significance, interpretability, and predictive stability.
🔹 Option 1 — Comprehensive Model (~18 variables)
Broad coverage of structural, quality, and neighborhood predictors
Key inclusions:
Gr.Liv.Area, TotalBsmt, Garage.Cars, OverallQual, ExterQual, KitchenQual
Multiple neighborhood and condition dummies
Pros: High explanatory power
Cons: Retained variables with marginal significance → increased complexity

🔹 Option 2 — Streamlined Model (~16 variables)
Removed weaker predictors (e.g., Mas.Vnr.Area, Lot_Shape_IR2, Land.Contour_HLS)
Preserved core structural drivers:
Gr.Liv.Area, TotalBsmt, Garage.Cars, Year.Remod.Add
Retained high-impact quality indicators
Maintained select neighborhood dummies with pricing influence
Pros: Similar fit to Option 1 with improved clarity
Cons: Slightly less coverage than Option 1

🔹 Option 3 — Parsimonious Model (~13 variables)
Focused only on the most statistically robust predictors (p < 1e-10)
Final retained set:
Structural: Gr.Liv.Area, BsmtFin.SF.1, TotalBsmt, Garage.Cars, Fireplaces
Quality: OverallQual, ExterQual, KitchenQual
Neighborhood: Crawfor, NoRidge
Condition: SaleCondition (Normal, Partial), Lot_Shape_Reg
Pros: Strong predictive accuracy with minimal complexity
Cons: Narrower variable coverage

✅ Conclusion
Option 1 → Maximum completeness but noisy
Option 2 → Balanced predictive strength with reduced redundancy
Option 3 → Nearly identical performance to Options 1–2 while being lean and highly interpretable
Final Recommendation: Option 3 (parsimonious model)
Isolates the true economic drivers of house prices
Avoids overfitting
Ensures interpretability and defensibility

📦 Requirements
R (≥ 4.0)
Packages:
tidyverse, janitor, broom, car, MASS, leaps, GGally, e1071

▶️ How to Run
Clone this repository
Open ames house price dataset analysis.Rmd in RStudio
Run chunks sequentially or Knit to HTML to reproduce analysis
