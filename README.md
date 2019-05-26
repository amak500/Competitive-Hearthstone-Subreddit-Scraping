# Project 3: NLP Analysis. 

## Problem Statement: 

The Hearthstone community is currently hemorrhaging users. Interest in Hearthstone from a global perspective is at an all time low. Additionally, many popular Twitch streamers such as Reynad or Amaz, now stream Dota 2 Autochess, a competing game because they have grown bored with Hearthstone and Autochess is seen as more popular/lucrative. Regular player engagement is also down, as the popular sentiment is that the Hearthstone metagame has stagnated heavily, and that there are balancing issues within the game itself. The question is how do we regain the users and streamers that we've lost over the past few years?  I propose that we use Random Forest Classification with TfidfVectorizer in order to first classify whether a post was made during the Knights of the Frozen Throne, or KOFT, expansion, or during the Mean Streets of Gadgetzan, or MSOG, expansion. We can then examine the most popular cards and archetypes posted during those expansions in order to inform our balances decision for wild. I hope to expand this model in the future to cover all Hearthstone expansions, so we can best keep community sentiment towards certain problematics cards/archetypes in mind when we release balance updates for standard as well.   

  
## Data Acquisition

Of the three main hearthstone subreddits, I chose to use reddit.com/r/competitivehs, as I felt that it would yield the most productive data regarding card and deck popularity. I used the pushshift.io api to scrape the reddit.com/r/competitivehs subreddit for data between the first and second months after the KOFT and MSOG Hearthstone expansions going 1000 posts at a time and loading my results into a json file, and then coverting those json files into dataframes.  

## Data Cleaning and EDA

After I scraped the data, I cleaned the data by removing all links, posts by bots, and deck codes. I then created a dummy variable named KOFT with a value of 1 for posts from the KOFT expansion and a value of 0 for posts from the MSOG expansion. A preliminary examination of the data revealed that amongst the most popular words for KOFT, Aggro, Jade, Druid, and Priest were in the top 100 most common. Additionally, Reno, Jade, Shaman, and Druid were in the top 100 most common for MSOG. Character and word count for each comment were also skewed to the right, which makes sense, as long deck guides are sometimes posted in the competitivehs subreddit.   


## Modeling

During this project, I constructed 2 models in total: Naive Multinomial Bayes with Tfidf, and  RandomForest with Tfidf. The auc_roc scores of the models respectively were 0.8884191123345472 and 0.8655484148315126. I chose RandomForest to be my production model even though it has a slightly lower auc_roc score because I believe that its top predicting features are more relevant to my dataset than those of my Naive Multinomial Bayes model. According to my production model, the most important features appear to be related to Reno Priest, Reno Warlock, Shaman, and Aggro Pirate Warrior. 


##  Conclusion
My production model correctly identified that Jade, Reno, and Aggro decks seemed to be the most problematic during their respective expansions. This was further backed up by the Vicious Syndicate metagame reports from the KOFT and MSOG expansions. I suggest that we take a further look at the power of Reno decks in particular, as their singleton nature means that they can only get better as more and more cards are printed and moved into wild. Additionally, we should take care to not let Aggro decks become too strong again, as that leads to a very polarized meta of aggro decks and decks that counter aggro decks, completely shutting out tempo decks. Additionally, I would like to scrape more expansions so that I can better classify problematic cards for future balancing decisions. 