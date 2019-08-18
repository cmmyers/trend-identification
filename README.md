# NLP Fashion Project

Given all the user generated data around fashion preferences that exists online, how can we leverage this data to identify and predict fashion trends?

I used data from a popular social media fashion site to identify references to garments, recorded references to those garments over time, and used clustering and time series modeling to attempt to pick out trends.

## Problem 1:
### How do we identify garment words?

How do we know what clothing items a user is talking about? How do we know whether a given word refers to an item of clothing in the first place? We could feed our program a list of manually generated garment words and ask it to count the number of times each occurs, but this wouldn't go very far in identifying latent trends, since we would have had to think of the word in order to track it. We could manually inspect the documents to identify new garment words, but this would take too much time (and largely defeat the point).

I started by using a machine learning model called Word2Vec to create a "garment vocabulary". Using data from 2009 through 2011, I built a Word2Vec model and found the 10 most similar words to each of the following: "dress", "shirt", "skirt", "pants", "shoes", and "bag".

script to create annual dataframes from master data: 
