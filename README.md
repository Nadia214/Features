# Features

 Feature Optimization Techniques — with Regression Focus
1️⃣ Feature Selection

Choosing a subset of the original features relevant to the target variable.
🔹 A. Filter Methods (Statistical; model-free)
Method	Use Case	Regression?	Notes
VarianceThreshold	Remove low-variance features	✅	Simple, preprocessing step
SelectKBest	Score-based selection	✅/❌	Use f_regression (✅) or chi2 (❌ for classification)
SelectPercentile	Top % features	✅/❌	Based on scoring function
Correlation Threshold	Drop weakly correlated or highly collinear features	✅	Based on Pearson/Spearman correlation
Mutual Information	Non-linear dependency	✅/❌	Use mutual_info_regression
ANOVA F-test	Feature-class association	❌	Categorical targets only
🔹 B. Wrapper Methods (Model-based search)
Method	Use Case	Regression?	Notes
RFE (Recursive Feature Elimination)	Recursive pruning	✅	Needs a regressor (e.g., SVR, RF)
RFECV	RFE + cross-validation	✅	Finds optimal #features
Forward Selection	Adds one-by-one	✅	Greedy, slow on large sets
Backward Elimination	Starts with all, removes	✅	Inverse of forward
SFS (Sequential FS)	Generalized forward/backward	✅	Can control scoring metric
🔹 C. Embedded Methods (Feature selection inside training)
Method	Use Case	Regression?	Notes
Lasso Regression	Regularization-based	✅	L1 penalty forces sparsity
ElasticNet	L1 + L2 penalty	✅	Better for correlated features
Tree-based models	Use splits to derive importances	✅	RF, XGBoost, LightGBM
Ridge Regression	L2 regularization	✅	Coefficients shrink but not to zero
Logistic Regression	Classification only	❌	Not applicable for regression
🔹 D. Advanced Methods
Method	Use Case	Regression?	Notes
Boruta	All-relevant selection	✅/❌	Based on Random Forest
SelectFromModel	Uses model importance	✅	Works with any estimator with .coef_ or .feature_importances_
Genetic Algorithms	Evolution-based search	✅	Computationally expensive
SHAP-based selection	Use SHAP values to keep top features	✅	Model-agnostic
Permutation Importance	Drop-shuffle-test	✅	Interpretation-friendly
2️⃣ Feature Reduction

Compress features into a smaller transformed space.
🔹 A. Unsupervised Reduction
Method	Use Case	Regression?	Notes
PCA	Projects to max variance directions	✅	Linear, fast
Kernel PCA	Non-linear PCA	✅	Expensive but powerful
t-SNE	Visualization	⚠️	Use only for visualization
UMAP	Visualization	⚠️	Faster alt to t-SNE
TruncatedSVD	Sparse PCA	✅	Faster for sparse matrices
ICA	Independent signal separation	✅	Signal processing focus
🔹 B. Supervised Reduction
Method	Use Case	Regression?	Notes
PLSR (Partial Least Squares Regression)	Preserve X–y correlation	✅	Powerful for few samples, many features
LDA (Linear Discriminant Analysis)	Maximize class separability	❌	Classification only
Supervised PCA	PCA guided by target	✅	Improves upon unsupervised PCA
Autoencoders	Neural compression	✅	Works for both regression & classification
3️⃣ Feature Importance

Measure how much each feature contributes to predictions.
Method	Use Case	Regression?	Notes
Coefficients (Linear Models)	Sign & magnitude matter	✅	Standard for linear models
Tree-based Importances	Based on splits	✅	.feature_importances_
Permutation Importance	Shuffle-drop-test	✅	Works on any model
SHAP Values	Local + global importance	✅	Model-agnostic, most interpretable
LIME	Local explanations	✅	For individual predictions
Drop Column Importance	Retrain without one feature	✅	Simple but slow
Partial Dependence Plots	Feature effect visualization	✅	Visual tool for interpretation
✅ Summary Flow (Which to Use When)

    If target = continuous → You are in regression

    → Use PLSR, PCA, SelectKBest (f_regression), SHAP, Permutation, Autoencoders, etc.

    If target = categorical → You are in classification

    → Use LDA, chi2, ANOVA F-test, Logistic Regression coefficients, etc.
