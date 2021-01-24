# Battery-classifier
Classifying the crystal system of batteries based on different properties found in the following Kaggle dataset: https://www.kaggle.com/divyansh22/crystal-system-properties-for-liion-batteriesaset:

The project was mainly conducted in a Kaggle notebook found here: https://www.kaggle.com/jesperhem/crystal-system-classification-for-batteries-100

## Processing
The different steps of processing the dataset were rather straight-forward. Most categorical columns were simply converted into integer-categories. However, the formula column was more of a challange to represent numerically. Simply converting the formulas into some kind of dummy variables would simply be too lossy in my opinion. Instead I found the "Chemparse" module (https://pypi.org/project/chemparse/) which was used to create columns for each atom in the dataset with integer values representing how many of each atoms are found in the corresponding molecule.

## Classification
When plotting the distribution of the three labels, 40% of the dataset was classed with label 1. Therefore, the first goal of the classifying was to score an accuracy greater than 40%, as a baseline model only predicting 1's would result in 40% accuracy.

The two models used were a Descision Tree Classifyer, as well as an Xgboost classifier. When simply loading them in from Scikit-learn and running them on an 80/20-split dataset, both scored 100% accuracy. But when splitting the dataset into 10 different splits with KFold, the variance of the Decision Tree model was far greater whan Xgboost which remained at 100% no matter how we split the data.

|Classifier|Best|Worst|Mean|Std|
|----------|-----|-----|-------|-----|
|Decision tree classifier| 100% | 85% |96%|0.05
|Xgboost | 100% | 100% | 100% | 0 |

## Notes:
The dataset only contains roughly 300 observations, which means that the models could be at risk for being overfitted. It would be very interesting, however, to see how the final Xgboost model would perform on a larger dataset of unseen data.

## Tech used:
- Python
- Sklearn
- Pandas
- Numpy
- Chemparse (https://pypi.org/project/chemparse/)
- Xgboost
- Matplotlib
- Seaborn
- KFold
