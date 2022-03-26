# Starbucks

## Motivation

In this repository for the Udacity Data Scientist degree Capstone project I am going to analyse the Starbucks dataset from 2017, containing data of 17000 individuals who were given kinds of offers to find out, how they react to them.

The goal is to find out, which person might be best provided with which offer (if any) to maximize their spendings.

## Project Overview

First I had a look at the dataset. There are three different files give:

    portfolio.json:         Description of the ten different offers made to people.

    profile.json:           Personal data (age, gender and income) of 17,000 people who took part. For 2175 no personal details are given.

    transcript.json:        The different interactions of offers and users. There are four different types.
                      
                            offer received: user received and offer.
                      
                            offer viewed: user viewed the offer.
                      
                            offer completed: user completed the offer.
                      
                            transaction: user spent money.
                      


Other files are:

    workspace.ipny:        Jupyter notebook containing the code.
    
    ready_dataset.pkl:     pickle file of data saved for ml model.
    
    statistical_data.pkl:  pickle file of dataset for statistical approach

  

  ## Results
  
  After having a look at the data at first I thought about training a neural network to predict the spending of a user.
  
  I transformed the data in a way, that the personal details, but also the the history of each individual will play a role (how often did the person viewed, completed which offer, how much money did that person spend while one or the other offer was active (and how much while none was active)).
  So I restructered the data to take all that into account, and each new status of every person was one datapoint. Every time the status changed (new offer viewed, offer completed or offer expired) I made a new datapoint containing all the users history up to that point.
  
  With that dataset (Having ~110,000 datapoints) I split into training and testing dataset on a user level.
  
  Then I did a gridsearch on the model, which turned out to perform rathe poorly.
  
  After removing the outliers, I could improve the performance by roughly factor four, but it was still too bad to be used reliably.
  
  So in a third attempt I tried to only focus on ppl who gave personal information and on the later timesteps where there was at least some personal history known. I hoped that this would improve the model to a certain point. The downside was, that the dataset shrinked to 1/4 of its original size. This seemed to have a stronger bad efect than the potentially positive effect of the more relevant datapoints. So this model performed slightly worse than the second one.
  
  In the end I decided to go for a statistical model, removing the people who did not give any personal data and splitting the rest by gender, 7 ag groups and 7 income groups.
  Then for each group I summed up the amounts spend and the times each offer category (informational, bogo, discount) was active, to get the average spending per timespan for each offer type for each group.
  This showed quite good results, and that different groups behave very differently. The downside is, that for rare combinations of age, gender and income the predictions are much worse than for common combinations. Also personal history is not taken account.
  
  So maxbe there is a diffferent way to combine personal history and general personal statistics, but thats for another time...
