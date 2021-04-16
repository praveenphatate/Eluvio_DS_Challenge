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
- fastText: Used for learning word embeddings and text classification which is created by Facebook's AI
- faiss: Used for efficient similarity search and clustering of vector
## Data Embedding Generation
#### Preprocessing
- Removed stopwords and performed stemming on titles using nltk library
- Appened time_created, date_created, author, processed titles in order to increase the similarity between articles published in and around the same date and same author
#### fastText model
- Trained a fastText with the preprocessed text with embedding size of 100, window size of 5, minimum word count of 5 for 25 epochs
#### faiss
- Creates a set of L2 based similarity index table between the embedding of traget keywords or article and embeddings of all other articles created from fastText model
## Search and Ranking
- Based on the search query entered by the user, the most relevant articles are shown. Reranked using date_created ordered by most recent articles to least recent articles
  NOTE: time_created and up_votes can also be used in reranking. However, it's not implemented as of now. 
## Recommendation System
- Searched through similarity vectors to find the closest embeddings based on the given tiitle embeddings
- Implemented two such recommendation approaches: Global article recommendation and last 30 days recommendation
#### Global Article Recommendation
- This recommends 20 similar articles from all the articles in the database. Reranked using up_votes such that most upvotes shown first.
#### 30 Day Recommendation
- This recommends 5 similar articles from the last 30 days based on upvotes.  Reranked using up_votes such that most upvotes shown first.
## Evaluation
Since there is no ground truth data like user interaction, impressions, likes and dislikes, there is no easy way to generate ground truth and evaluate the model. Hence, it is treated as an unsupervised learning problem. If there was ground truth data we could compare the generated recommendations/ranking and calculate the quality of my approach using metrics like NDCG(Normalized Discounted Cummalative Gain) and/or MAP(Mean Average Precision).


