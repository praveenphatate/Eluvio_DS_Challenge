# Eluvio_DS_Challenge
## Dataset Description
- Total Samples: 509236
- Start date: 1/25/2008, End Date: 11/22/2016.
- Features: time_created, date_created, up_votes, down_votes, title, over_18, author, category
- Total number of articles published each year

![](fig/articles_yearly.png)
- Total number of articles published monthly

![](fig/articles_monthly.png)
- Total number of authors published monthly

![](fig/authors_monthly.png)
#### Libraries Used
- pandas: Used for data manipulation and analysis
- NumPy: Used for handling multi-dimensional arrays and matrices
- nltk: Used for Natural Language preprocessing
- fastText: Used for learning word embeddings and text classification which is created by Facebook's AI team
- faiss: Used for efficient similarity search and clustering of word embeddings
## Recommendation
#### Preprocessing
- Removed stopwords and performed stemming on titles
- Appened time_created, date_created, author, processed titles in order to increase the similarity between same author
#### fastText model
- Trained a fastText with the preprocessed text with embedding size of 100, window size of 5, minimum word count of 5 for 25 epochs
#### recommend
- Used faiss library to create a set of L2 based similarity vectors between all the embeddings create from fastText model
- Searched through similarity vectors to find the closest embeddings based on the given tiitle embeddings
- Implemented two such recommendations: Global article recommendation and last 30 days recommendation
##### Global Article Recommendation
- This recommends 20 similar articles from all the articles, based on upvotes. Reranked using upvotes such that most upvotes shown first.
##### 30 Day Recommendation
- This recommends 5 similar articles from the last 30 days based on upvotes.  Reranked using upvotes such that most upvotes shown first

## Search and Ranking
