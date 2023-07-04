# Customer Default Prediction

## Objective 
- Credit default prediction is central to managing risk in a consumer lending business. Credit default prediction allows lenders to optimize lending decisions, which leads to a better customer experience and sound business economics.
- Predicting whether a customer will default in future help create a better customer experience for cardholders by making it easier to be approved for a credit card.

## Dataset 
- **Original Provided Dataset :** https://www.kaggle.com/competitions/amex-default-prediction/data (**Size** : 50GB)
- **Compressed Dataset :** https://www.kaggle.com/datasets/raddar/amex-data-integer-dtypes-parquet-format (**Size** : 4GB)

 ## Evaluation Metric 

 **M** = **0.5** . **(G+D)**

 **G** : **Normalized Gini Coefficient**
 
 **D** : **Default Rate Captured At 4%**

- The default rate captured at 4% is the percentage of the positive labels (defaults) captured within the highest-ranked 4% of the predictions, and represents a Sensitivity/Recall statistic.
-  The negative labels are given a weight of 20 to adjust for downsampling.

## Approach 

- Firstly, Data was analysed and explored . It was found out that Each Customer has at least 13 Transaction Statements in the training data .
- Then For Each Customer , his statements data is aggregated to create new features such as Mean , Median , last and many more .
  Feature engineering was explored using **RAPIDS cuDF** which performs operations like dataframe groupby aggregation on GPU **10-100x faster** than using CPU.
- Model is trained using **Xgboost Algorithm**.Model Training is done on **GPU** using **Batch Gradient Descent**.
- **5-Fold Cross Validation** is done to ensure that chances of overfitting reduces a lot.
- After Training with particular parameters , **Train Log-Loss Score : 0.15-0.17** , **Validation Log-Loss Score : 0.21-0.23** is
  achieved.

## Results

- **Evaluation Metric Score : 0.788 on training data.**
- **Evaluation Metric Score : LB Score - 0.801 on unseen data.**

## Conclusions 

**TOP 20 FEATURES**
![featureimportance](https://github.com/VectorNd/Customer_Default_Prediction/assets/111004091/fcefae65-306d-4f1a-9a5a-c42e568d7aab)

**PREDICTIONS DISTRIBUTION**
![Predictions](https://github.com/VectorNd/Customer_Default_Prediction/assets/111004091/259996ff-61b9-43dd-b4e6-93fe5c3ef1ed)

## Notebook Links 

- EDA Notebook : https://www.kaggle.com/code/rishabhkamboj2003/amex-default?scriptVersionId=135741375
- Training Notebook : https://www.kaggle.com/code/rishabhkamboj2003/xgboost-training?scriptVersionId=135741514
