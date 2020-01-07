# SleepBot

SleepBot is a **Click Prediction Bot** which uses the data from google search console to predict the *Net Clicks* of Keyword for a given date. 


## Dataset

The bot is trained using the *FDF* which has:

* 1368792 **Records**
* 74 **Features**
* 19269 **Keywords**


## Methodology

The Dataset is divided into three classes based on the Net Clicks:

* **Clicks Level 0** If Net Clicks is 0
* **Clikcs Level 1** If Net Cliks is 1
* **Clicks Level 2** Otherwise

This division is done to facilitate the training of *3 Level Model*:

* **Level 1 *Classifier*** which predicts 0 (Clicks Level 0) or 1 (Clicks Level other than 0) 
* **Level 2 *Classifier*** which predicts 0 (Clicks Level 1) or 1 (Clicks Level 2)
* **Level 3 *Regressor*** which predicts the Net Clicks


## Features

Extra Features added to the *FDF* are:

* Mean of the Bert Embedding Vector for Keyword
* Median of the Bert Embedding Vector for Keyword
* Number of Words in the Keyword
* Number of Characters in the Keyword
* Average Number of Words in the Keyword
* Number of Stop Words in the Keyword
* Number of Digits in the Keyword
* Day of the Week


## Training

### Outlier Removal
The data is grouped by date and outliers are removed from each group using standard z score normalization. Only +-2 std is kept
```python
z=df.groupby('date').transform(lambda group: (group - group.mean()).div(group.std()))
outliers = z.abs()> stds
df_out=df[outliers.any(axis=1)]
```
### Level 1 Model
**XG Boost** Classifier is trained on the data before 2019-10-10 to predict between clicks level 0 or other. The rest of the data is used for testing. Model has **20 estimators** and **6 depth**. These parameters were selected using Cross Validation and Time Series Split.

#### Confussion Matrix 

![Confussion Matrix]("https://github.com/codejones/sleepare_DS/blob/master/graphs/conf_level1.png")

#### Feature Importance


### Level 2 Model
**XG Boost** Classifier is trained on the data before 2019-10-10 predict between clicks level 1 or 2. The rest of the data is used for testing. Model has **25 estimators** and **5 depth**. These parameters were selected using Cross Validation and Time Series Split.


#### Confussion Matrix 


#### Feature Importance


### Level 3 Model
**XG Boost** Classifier is trained on the data before 2019-10-10 predict between clicks level 1 or 2. The rest of the data is used for testing. Model has **40 estimators** and **8 depth**. 



## Results

The data after 2019-10-10 is used for testing. 

#### Combined Confussion Matrix of Level 1 and Level 2 Model


#### Performance

Metric | Value 
------------ | -------------
Mean Absolute Error | 0.028
Root Mean Squared Error | 0.272
Variance Score | 0.628
False Negatives | 5%
False Positives | 1.8%




#### Model Comparison 



