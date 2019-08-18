# NLP Fashion Project

Given all the user generated data around fashion preferences that exists online, how can we leverage this data to identify and predict fashion trends?

I used data from a popular social media fashion site to identify references to garments, recorded references to those garments over time, and am using clustering and time series modeling to attempt to pick out trends.

## Problem 1:
### How do we identify garment words?

How do we know what clothing items a user is talking about? How do we know whether a given word refers to an item of clothing in the first place? We could feed our program a list of manually generated garment words and ask it to count the number of times each occurs, but this wouldn't go very far in identifying latent trends, since we would have had to think of the word in order to track it. We could manually inspect the documents to identify new garment words, but this would take too much time (and largely defeat the point).

## Problem 2:
### How do we identify trends? 

Fashion cycles rise and fall at different rates and over different periods of time depending on how they quickly they are accepted and rejected. Identifying current trends is a matter of locating peaks of acceptance. However, to predict trends, we must figure out how to distinguish between local maxima, where the trend is still rising overall, vs absolute maxima that indicate the peak of a trend and the beginning of its rejection. 

Process:

1) I collected data from approximately 1 million photo posts spanning March, 2008 to
November, 2016. These posts are composed of one or more photos, a title, date, and
a description that might range from a few words to several paragraphs.
The data was processed using BeautifulSoup and stored using
MongoDB and JSON.

2) After adding year, quarter and month features to my dataset, and tokenizing the
photo descriptions, I created a Word2Vec model for the data for years 2009-2012.
I used this model to identify approximately 60 'garment words' based on their
similarity to five 'basic' garment words: 'dress', 'skirt', 'pants', 'shoes' and
'bag.'

3) Using my ~60 identified garment words, I created bigrams that paired every
occurrence of a garment word with the word that immediately preceded it. I then
created new W2V models for each year, 2009 through 2012. I treated this as my
initial training set.

4) I performed EDA using my 'bigramified' text. I collected lists of bigrams
that the W2V models considered 'most similar' to the basic garments and examined
the respective differences in these lists from year to year. I created similar
lists using simple term frequency of bigrams. I then plotted the members of these
disjunctive lists to determine whether members of the list could accurately be
considered 'trends'. Rather than use a hard definition of 'trend', I visually
examined the plots for significant peaks.

5) Moving forward, I plan to use seasonal decomposition to isolate trend cycles from seasonal cycles and apply kmeans in order to create "trend clusters" which I will then match to moving windows in order to predict future trends. 
