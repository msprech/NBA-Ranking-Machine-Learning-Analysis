# NBA Ranking Machine Learning Analysis

## Objective

We will use the data set provided from Kaggle that contains the final player stats and game rankings from the 2014 - 2020 NBA seasons to predict the overall NBA rating of the players for the 2020 season.

## DataSet

https://www.kaggle.com/mj1196/nba-2k20-player-attributes

## Team Members

Molly S. https://github.com/john10roberts/WERNOTR/tree/Molly

Miguel M. https://github.com/john10roberts/WERNOTR/tree/Miguel

Scott K. https://github.com/john10roberts/WERNOTR/tree/Scott

John R. https://github.com/john10roberts/WERNOTR/tree/John

## Initial Database

Created a script to set up the database to allow for import into postgres: https://github.com/john10roberts/WERNOTR/blob/John/Resources/CreateNBADB.sql

Loaded the data using postgres import function.

## Exploratory Data Analysis

Created a simple jupyter notebook to do an initial exploratory analysis of the data set:
https://github.com/john10roberts/WERNOTR/blob/John/NBA2kRatingsEDA.ipynb

* 2412 rows
* 32 columns
* 0 Null values

## Integrated RandomForest model

* Preprocessing: Our dataset was strong to begin with, so the only consideration before starting the actual analysis was creating a DataFrame from our SQL database data, and splitting the data into smaller datasets based on seasons.

* Feature selection: The 'rankings' column was our sole target variable, while all the other columns fell into the feature set. We also dropped the categorical columns of 'player', 'team', and 'season' from the feature set.

* Training and testing: After splitting the 2019-20 season from the rest of the dataset, we trained the data on all of the other seasons. We used train_test_split on scaled data from past seasons. We then applied the trained RandomForestModel to the 2019-20 dataset in order to predict the rankings.

https://github.com/john10roberts/WERNOTR/blob/Molly/integrated%20rf%20model.ipynb

* RandomForestModel benefits: This model was chosen because of its ability to work with large datasets as well as it's lower risk of overfitting and potential to handle outliers. Another benefit of the RandomForestModel is that it allowed us to look at how important each feature was to calculating the outcome.

* RandomForestModel limitations: The main limitation was that we were not able to evaluate it with the accuracy score alone, which was very low. We therefore had to redefine our standards for accuracy, as many of the predictions were close to the actual rankings, although not exact.

* RandomForestModel outcome: Although the accuracy score was low at .217, we still felt this model had value for our analysis as all but 2% of the predicted rankings were within 5 points of the actual rankings. Within the five-point range, 110/507 predictions were exact and 179/507 were one point away. We included the chart below to help better visualize the accuracy of our model.

https://github.com/john10roberts/WERNOTR/blob/Molly/predictions.jpg

* Database integration: We applied a connection string to our local SQL database in our Jupyter Notebook script to import the dataset for the model to work with. We also connected the transformed dataset back to our local database with the .to_sql method in order to create a new table.
https://github.com/john10roberts/WERNOTR/blob/Molly/rf_data_output.csv

## Linear Neural Network
Created a linear neural network model using tensor flow. Split the data set into a training set of all of the data excluding the 2019-2020 season and a test dataset that was just the 2019-2020 season. Dropped the un-needed categorical columns and used 80% of the data set with a random_state of 0 to train the model. The linear model had a Mean Absolute Error of 1.53. https://github.com/john10roberts/WERNOTR/blob/John/NeuralNetworkDBConnect.ipynb

## Deep Neural Network
Created a deep neural network model using tensor flow. Split the data set into a training set of all of the data excluding the 2019-2020 season and a test dataset that was just the 2019-2020 season. Dropped the un-needed categorical columns and used 80% of the data set with a random_state of 0 to train the model. https://github.com/john10roberts/WERNOTR/blob/John/NeuralNetworkDBConnect.ipynb

* Two Hidden layers
  * Layer 1 - 64 Neurons, relu activation
  * Layer 2 - 64 Neurons, relu activation
* Output Layer

This model had a Mean Absolute Error of 1.81 with the vast majority of projections being within +/- 5 points of the actual rating.

## Dashboard

For the second part of the project I mainly focused on creating the html page for our dashboard. It has a simple search option to be able to look up players using any of their player data from our dataset. Once we've finished refining the machine model, the final exported data will be loaded onto the page. For now there is just the data from the 2019-20 season. 

For the most part our dataset was very clean, but one issue was that in order for that data to be loaded onto the page, it needed to be in javascript and around 6 of the columns in the dataset were throwing errors when converted into js. So, I went and found which columns these were and changed them in jupyter notebook. While I don't I have a machine model on my computer yet, I still went ahead and set up a postgres server and imported our data for use further down the road. A sample of the dashboard can be found here:

* https://stkaran.github.io/FPS/

* https://quixck23.github.io/quixck23WERNOTR.github.io/

## Presentation

Here is our initial draft of the presentation: https://www.canva.com/design/DAE3EHai5PE/view?utm_content=DAE3EHai5PE&utm_campaign=designshare&utm_medium=link&utm_source=publishsharelink
