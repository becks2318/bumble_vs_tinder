# Project 3 - Reddit Data

### Problem Statement


I want to see if I can build a model to classify posts as either belonging to the Tinder or Bumble subreddit.

---


### Executive Summary

The goal of this project was to compare two subreddits and build a model to distinguish posts between them.

Data was collected from the subreddit pushshift API and cleaned.

Bayes search was run across all four models evaluated to determine the best hyperparameters of:
- SVC
- Bernoulli Naive Bayes
- Random Forest
- XG Boost

The best model was: XG Boost with the following hyperparameters:
- Cvec max_df: 0.9
- Cvec max_features: 18,000
- Cvec min_df: 2
- XG max_depth: 15
- XG n_estimators: 279

Predicting accurately on unseen data 69% of the time

---

### File Directory

**data**  
bumble_posts.csv: Posts scraped from the bumble subreddit  
tinder_posts.csv: Posts scraped from the tinder subreddit  
combined_clean.csv: File containing cleaned posts from both subreddits ready for modeling  
model_results.csv: File containing the results of each model run  
 
**code**  
reddit_data_collection.ipynb: Notebook with code to pull data from the reddit API  
reddit_cleaning.ipynb: Notebook with code to clean the posts pulled from reddit  
reddit_modeling.ipynb: Notebook containing all of the models run in this project  

**images**  
tinder_words.png: Frequency of top 10 words from tinder subreddit  
bumble_words.png: Frequency of top 10 words from bumble subreddit  
combined.png: Frequency of top 25 words from all combined posts  
scores.png: Scatterplot of training and test scores from models run  
confusion_matrix_test.png: Confusion matrix of test results from top model  

---


### Data Dictionary

Sources for the data:   
Tinder: https://www.reddit.com/r/Tinder/  
Bumble: https://www.reddit.com/r/Bumble/


|Feature|Type|Dataset|Description|
|---|---|---|---|
|**title**|_object_|Tinder Data|Title of the post|
|**author**|_object_|Tinder Data |Username of the post|
|**created_utc**|_int_|Tinder Data|The date the post was created|
|**selftext**|_object_|Tinder Data|The text of the post|
|**subreddit**|_object_|Tinder Data|The subreddit the post was pulled from|
|**body**|_object_|Tinder Data|The comments of the post|
|**title**|_object_|Bumble Data|Title of the post|
|**author**|_object_|Bumble Data |Username of the post|
|**created_utc**|_int_|Bumble Data|The date the post was created|
|**selftext**|_object_|Bumble Data|The text of the post|
|**subreddit**|_object_|Bumble Data|The subreddit the post was pulled from|
|**body**|_object_|Bumble Data|The comments of the post|
|**text**|_object_|Combined Data|Text of the post: combined Post Title, Post Text, Post Comments fields|
|**subreddit**|_int_|Combined Data|The subreddit the post was pulled from|
|**post_length**|_int_|Combined Data|The number of words in the post|
|**model**|_object_|Model Results Data|The model that was run|
|**best_params**|_object_|Model Results Data|The best params from that run of the model|
|**training_score**|_int_|Model Results Data|The score from running the model on training data|
|**test_score**|_int_|Model Results Data|The score from running the model on unseen test data|



---


### Data Modeling

The data was first collected and cleaned:
- All null values, [removed], or [deleted] posts were removed
- All posts that were only one character or one emoji were removed
- All punctuation was removed  
- A custom list of stop words was created by evaluating the most common combined words from the posts
- All text posts were combined into one text column (title, description, comments)

A baseline model was first run to determine what the likelihood of picking either Bumble or Tinder by chance was: 0.51

I ran and evaluated four different types of models to see which could produce the best results on unseen test data:
- SVC
- Bernoulli Naive Bayes
- Random Forest
- XG Boost

I ran Bayes Search across all models to determine the best hyperparameters to use


---

### Conclusions and Recommendations

XG Boost was the highest model evaluated with the following results:  
Training score: 0.83  
Test score: 0.69  

Best hyperparameters:  
Cvec max_df: 0.9  
Cvec max_features: 18,000  
Cvec min_df: 2  
XG max_depth: 15  
XG n_estimators: 279  

I found that these subreddits ended up being quite similar. The model predicted accurately ~70% of the time which was better than the baseline model of 50% but not as high as I would have liked.

---


### Future Research

Given additional time I would have liked to complete the following:
- Additional analysis on text cleaning: e.g. stemming or lemmatizing, more EDA on minimum post length
- Additional tuning: e.g. exploring additional hyperparameters for each model
