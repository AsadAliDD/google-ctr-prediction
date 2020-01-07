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

