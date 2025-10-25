# Diamond Price Prediction  
### *Exploratory and Advanced Data Analysis*  

This repository contains two comprehensive phases of a data analysis project conducted as part of a coursework.  
The project aims to explore, model, and predict **diamond prices** based on their characteristics using statistical and machine learning techniques.

---

## Project Overview  

The global diamond market faces persistent challenges of **price transparency** and **valuation inconsistency**.  
This study uses the **Kaggle Diamonds dataset** (also available in R’s `ggplot2` library) to investigate how the *Four Cs* — **Carat, Cut, Color, and Clarity** — along with other physical attributes, influence the retail price of diamonds.

Through a two-stage analytical approach — **Exploratory Data Analysis (EDA)** and **Advanced Predictive Modeling**, this project builds a strong foundation for accurate price forecasting.

---

## Objectives  
- Identify key variables influencing diamond price.  
- Conduct statistical and visual analysis to understand data patterns.  
- Detect and handle data irregularities (outliers, skewness, multicollinearity).  
- Fit, evaluate, and compare predictive models to determine the best performer.  
- Provide insights and recommendations for transparent diamond pricing.

---

## Dataset Details  
**Source:** Kaggle / `ggplot2::diamonds`  
**Records:** 53,940  
**Variables:** 10  

| Variable | Description |
|-----------|--------------|
| carat | Diamond weight (size indicator) |
| cut | Quality of diamond cut |
| color | Color grade (D = best, J = worst) |
| clarity | Measure of imperfections |
| depth | Total depth percentage |
| table | Width of top relative to widest point |
| price | Price in USD (response variable) |
| x | Length (mm) |
| y | Width (mm) |
| z | Depth (mm) |

---

## Phase 1: Exploratory Data Analysis

### **Preprocessing**
- Removed invalid records (x, y, or z = 0).  
- Created derived variables:  
  - `depth_percentage = (z / mean(x, y)) * 100`  
  - `volume = x * y * z`  
- Applied **log transformation** on price to correct skewness.  
- Visualized and analyzed outliers.

### **Descriptive Findings**
- Price is highly skewed — larger diamonds are rarer and exponentially pricier.  
- **ln(price)** and **ln(carat)** show a strong positive linear relationship.  
- Higher **cut**, **color**, and **clarity** grades correspond to higher prices.  

### **Statistical Tests**
- **Kruskal–Wallis Test** confirmed significant differences in price across cut, color, and clarity categories.  

### **PCA and Clustering**
- **PCA** reduced dimensionality (4 components explain 88.9% of variance).  
- **K-Means Clustering** identified 2 main groups:  
  - **Cluster 1:** Large, high-priced diamonds  
  - **Cluster 2:** Small, lower-priced diamonds  

---

## Phase 2: Advanced Analysis

### **Multiple Linear Regression (MLR)**  
- Model: `ln(price) ~ ln(carat) + cut + color + clarity`  
- Adjusted R² = **98.3%**  
- Train–test correlation for predicted vs actual price: **0.979**  
- Residual analysis showed minor violations in independence and homoscedasticity.  

### **Regularization Techniques**  
To address multicollinearity and improve generalization:  
- **Ridge Regression** – reduces coefficient variance.  
- **LASSO Regression** – performs variable selection.  
- **Elastic Net** – hybrid of Ridge and LASSO.  
> 🔹 *Elastic Net achieved the lowest RMSE and highest R², making it the best linear regularized model.*

### **Random Forest Regression**  
- Built with 500 trees using 80/20 train-test split.  
- Achieved **R² = 0.98** and **Correlation = 0.991** between predicted and actual prices.  
- Top features: **carat**, **x**, **y**, **z** (size dimensions).  
> **Random Forest** outperformed all other models with the lowest RMSE and MAPE.

---

## Model Comparison Summary  

| Model | RMSE | R² | Remarks |
|--------|------|----|---------|
| Multiple Linear Regression | Moderate | 0.983 | Strong baseline |
| Ridge Regression | Moderate | High | Handles multicollinearity |
| LASSO Regression | Low | High | Performs feature selection |
| Elastic Net | **Lowest (linear)** | **Highest (linear)** | Best regularized linear model |
| Random Forest | **Overall Best** | **0.98+** | Non-linear, most accurate |

---

## Tools & Technologies  
- **Language:** R  
- **Libraries:** `ggplot2`, `dplyr`, `car`, `glmnet`, `randomForest`, `NbClust`  
- **Techniques:**  
  - Descriptive & Inferential Statistics  
  - PCA & Clustering  
  - Regression Modeling (MLR, Ridge, LASSO, Elastic Net)  
  - Ensemble Learning (Random Forest)

---
## Key Insights  
- Diamond **size (carat, volume)** dominates price prediction.  
- **Quality indicators** (cut, clarity, color) significantly affect value.  
- **Random Forest** delivered the most accurate predictions.  
- Combining **PCA, Regularization, and Ensemble Methods** improved model performance and interpretability.

## References & Resources  
- Dataset: [Kaggle Diamonds Dataset](https://www.kaggle.com/datasets/shivam2503/diamonds) 
