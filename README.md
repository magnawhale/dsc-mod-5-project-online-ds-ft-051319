
# Module 5 Final Project


## Introduction

For the module 5 project, I used the NASA Kepler Telescope data available through their open-access API ([link](https://exoplanetarchive.ipac.caltech.edu/docs/program_interfaces.html)) to perform a calssification task. My goal was to use the data to train models to accurately classify Kepler Objects of Interest (instances where observed stars dim or wobble with regularity) as either exoplanets or false positives (FP here meaning a dimming/wobbling not caused by the existence of an exoplanet).

<img src="https://i.ytimg.com/vi/3yij1rJOefM/maxresdefault.jpg" width=75% class="center">

## Overview

For those who are interested, the Jupyter Notebook containing all of the code for this project can be found here:

   * [Kepler Classification notebook](https://github.com/magnawhale/dsc-mod-5-project-online-ds-ft-051319/blob/master/student.ipynb)
   * [Kepler Feature Names Information](https://exoplanetarchive.ipac.caltech.edu/docs/API_kepcandidate_columns.html)

I began by scraping the cummulative dataset on known Kepler Objects of Interest (KOI) using the open-access API. Once imported, I made sure to remove any features (columns) that contained information supplied after the fact (as the result of analysis), leaving only the raw, un-interpretted data. 

I then proceeded to iterate through numerous modeling tachniques and algorithms to settle upon one which produced the highest accuracy score for the testing data set while also avoiding overfitting (where training accuracy far exceeds testing accuracy).

## Methodology

After scrubbing and tidying my dataset, which including engineering a custom feature, I began experimenting with various classification algorithms, even combining several in a number of ways. XGBoost and Support Vector Machines appeared to show the most promise, so I primarily focused on using, tuning, and combining these two algorithms. 

I ran both of these algorithms on both the raw data and data transformed using Principal Component Analysis. I also compared using the default/vanilla implementations of these techniques to version with their hyperparameters tuned using GridsearchCV. Going even further, I experimented with chaining different algorithms together where a second algorithm was fitted to the mistkes that a first algorithm made. Additonally, I also attempted to use Model Stacking, where a third model is trained on the predictions two separate models made on the raw data. 

For all of the instances that employed hyperparameter tuning (using GridsearchCV), rather than simply accept the "best parameters" returned by the algorithm, I decided to develop my own selection technique. This was done because gridsearchCV has a tendency to overfit a model to the training data. Thus, I calculated the harmonic mean of testing accruacy scores to 1 - the difference between training and testing accuracy. This selects for the parameters that produced the best balance between high test accuracy and overfitting avoidance.

<img src="/images/xgb_conf_matr_importances.png" width=75% class="center">

## Results

The best model I developed produced a testing accuracy score of 83%. Unfortunately, this came from the vanilla version of SVC (Support Vector Classifier), meaning most of my efforts at building more complicated models were wasted in terms of creating a better classifier (but the technical knowledge gained was priceless!). The second best scores of 82% came from various tuned XGBoost models, so perhaps all of my effort were not in vain. 

Although these scores are not bad, more external work will need to be done to properly classify the 17% of KOIs which my model misclassified.

<img src="/images/exoplanets.jpg" width=75% class="center">