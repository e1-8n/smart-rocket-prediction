# 🚀 Smart Rocket: Flight Outcome Prediction

🥈 **2nd place** in the Smart Rocket (الصاروخ الذكي) prediction competition.

## What is this project?
This project predicts whether a rocket flight will end in **Success**, **At Risk**, or **Failure** based on six sensor readings:
Engine Temperature, Speed, Altitude, Pressure, Fuel Remaining, and Trajectory Deviation.

Instead of relying only on a black-box model, I built an explainable **Flight Health Score** that combines all six readings into one number, and every prediction comes with its top two contributing factors and a short written reason.

## Dataset
- **Training data:** 50 flights with known outcomes (21 Success, 16 At Risk, 13 Failure)
- **Challenge data:** 15 flights to predict
- No missing values

## Method
1. **Exploratory analysis:** Successful flights showed lower engine temperature and trajectory deviation, and higher speed, altitude, pressure and fuel. Failures showed the opposite, and At Risk sat in between.
2. **Health Score:** Each reading is standardized (z-score), multiplied by its direction (+1 if higher is better, −1 if higher is worse), and summed.
3. **Decision rule:**
   - Score < −1.6 → **Failure**
   - −1.6 ≤ Score < 0.7 → **At Risk**
   - Score ≥ 0.7 → **Success**
4. **Validation:** 5-fold stratified cross-validation, compared against Logistic Regression.

## Results
| Model | CV Accuracy | Std |
|---|---|---|
| **Health Score (ours)** | **92%** | 0.07 |
| Logistic Regression | 88% | 0.10 |

- Training accuracy: 98% (49 of 50 flights)
- Logistic Regression agreed with the Health Score on all 15 challenge flights (100%)
- Logistic Regression learned similar weights for all six readings, supporting the equal-weight design
- Final predictions: **8 Success · 3 At Risk · 4 Failure**

## How to use
1. Clone the repository:
   git clone https://github.com/e1-8n/smart-rocket-prediction.git
   cd smart-rocket-prediction
2. Install the requirements:
   pip install -r requirements.txt
3. Open the notebook:
   jupyter notebook Smart_Rocket_Code.ipynb
4. Run all cells. The predictions will be saved to `Smart_Rocket_Submission.xlsx`.

## Tools
Python · pandas · NumPy · matplotlib · seaborn · scikit-learn

## Author
**Eman Almowallad**, Data Science student at Umm Al-Qura University