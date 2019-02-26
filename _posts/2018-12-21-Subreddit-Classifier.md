---
layout: post # needs to be post
title: Subreddit Classifier
featured-img: 
categories: [Project, NLP]
---


# Problem Statement:
Using 2 Subreddits: `thanosdidnothingwrong` & `inthesoulstone` How can we scrape reddit data and use NLP classification to train a model that is able to differentiate between two subreddits.?

# Executive Summary:

Using the pushshift.api I scraped 20,000 posts from r/thanosdidnothing wrong(54%) 16983 posts from r/inthesoulstone(46%)

The 3 main models I focused on were Logistic Regression, Random Forest and Ada Boost
Typically for almost all of my models I achieved around an 66% accuracy score.
I typically used the same hyper parameters (n_gram range (1,2),lasso regularization
Count Vectorizer and Tfidf Vectorizer were also used in each model.

from my results I was able to predict 

Precision = 66%                Sensitivity = 50%
Specificity = 78%              Accuracy = 65%

The accuracy of the model is not extremely high, and when I tuned with hyper parameters my scores did not reflect much of change at all. 

# Conclusion:

- Given more time I would be interested in diving into the text to apply NLTK. Upon reviewing the word clouds, I found that there were alot of words that could have been stemmed down to their base words (ex: survived, survives, surviving, upvotes, upvote, etc.)
- These two subreddits are very similar. Both are focused on the Marvel universe, a  lot of the posts are memes!
- Also I believe looking at different timeframes for the data being used heavily impacts these subreddits
