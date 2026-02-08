# Airline Delay Cause Classification using Multinomial Logistic Regression

## What this project is about
Flight delays don’t happen for just one reason. They can be caused by weather,
airline operations, air traffic congestion (NAS), security issues, or late-arriving aircraft.

In this project, I built a **multinomial logistic regression model** to identify the
**primary cause of delay** for Flights using real operational data.
Instead of predicting how long a flight will be delayed, the focus is on
*why* the delay happened.

I also extended the model to go beyond simple classification by using predicted
probabilities to estimate the **expected delay contribution** of each cause.
This makes the results more interpretable and operationally useful.

---

## Dataset
The project uses the **Airline Delay Causes** dataset, which contains
aggregated delay statistics for domestic flights in the United States.

The dataset includes:
- Year and month of operation  
- Airline carrier and airport codes  
- Number of arriving flights and delayed flights  
- Delay minutes broken down by cause (carrier, weather, NAS, security, late aircraft)

### Dataset credit
Dataset source: **Kaggle – Airline Delay Causes**

The dataset is used strictly for educational and research purposes.
All rights belong to the original data providers.

The CSV file is not included in this repository due to licensing and size
considerations. To reproduce the results, download the dataset from Kaggle
and place it in the same directory as the notebook.

---

## Target construction
The target variable (`delay_cause`) is created by selecting the delay category
with the **maximum delay minutes** for each observation:

- Carrier delay  
- Weather delay  
- NAS delay  
- Security delay  
- Late aircraft delay  

This converts the problem into a **multiclass classification task** where each
flight is assigned its dominant delay cause.

---

## Model and approach
- Categorical variables are one-hot encoded
- Numerical operational features are used directly
- Data is split using a stratified train–test split
- A **multinomial logistic regression** model is trained using the LBFGS solver

Logistic regression was chosen for its interpretability and well-defined
probabilistic outputs.

---

## Evaluation
Model performance is evaluated using:
- Precision, recall, and F1-score for each class  
- Confusion matrix visualization  
- Class-wise accuracy comparison  
- Baseline comparison using a naive classifier  

This helps identify where the model performs well and where delay causes
tend to overlap.

---

## Expected delay attribution (extension)
Instead of stopping at class prediction, the model’s predicted probabilities
are combined with total delay minutes to estimate **expected delay contribution**
for each cause:

Expected contribution =  
`P(delay cause | features) × total delay minutes`

This provides a more meaningful view of operational risk by showing how much
delay impact is attributable to each cause on average.

---

## Key takeaways
- Weather and NAS delays show strong seasonal behavior  
- Carrier-related delays vary noticeably across airlines  
- Most confusion occurs between carrier and NAS delays  
- Probability-based attribution offers more insight than labels alone  

---

## Tools used
- Python  
- pandas  
- scikit-learn  
- seaborn  
- matplotlib  

---

## How to run
1. Download the dataset from Kaggle  
2. Place the CSV file in the same folder as the notebook  
3. Run the notebook from top to bottom  

---

## Notes
This project was built as a learning and analysis exercise focused on
interpretable machine learning and practical modeling decisions.
