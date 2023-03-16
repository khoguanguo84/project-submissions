# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 3: Web APIs & NLP

### Introduction: improv vs StandUpComedy


Which of these performing arts do people want to take up?

"Three key differences between the two to underline: 1) Stand-ups are alone on stage, whereas improv folks are onstage with 2-3 other teammates. 2) Stand-ups craft repeatable messaging designed to sell our audiences on ideas & things we find funny. Improv teams are creating stories on the spot, which forever disappear the moment they're completed – all to never be recreated again. 3) Improv folks are positive." ~ Jon Selig

[https://www.linkedin.com/pulse/necessary-distinction-jon-selig/](https://www.linkedin.com/pulse/necessary-distinction-jon-selig/)

Improv vs Stand Up Comedy, 2 forms of artistic expression that are commonly and erroneously used interchangeably.

---
### Problem Statement

A performing arts center is thinking of adding courses to their roster for revenue and is looking to compile feedback on Improv and Stand Up Comedy. 

1. The performing arts center would like to be able to separate comments from each subreddit for easy reference.
2. They would like to see the terms that are commonly associated with each performing art in order to better formulate their syllabus.
3. As a secondary concern, they would also like to see which art form may respond better to classes and structured instruction.


### Models


I will be using classification models for this project because the main objective stated above is to categorize posts into the subreddits. Multinomial Naive Bayes and Logistic Regression will be used.

Logistic regression is easier to implement, interpret, and very efficient to train. It is very fast at classifying unknown records. It performs well when the dataset is linearly separable. It can interpret model coefficients as indicators of feature importance.

Naive Bayes doesn't require as much training data. It handles both continuous and discrete data. It is highly scalable with the number of predictors and data points. It is fast and can be used to make real-time predictions.

The models will be scored on the following:

Train and test scores
1. Accuracy
2. Sensitivity
3. Specificity
4. Precision

Since the number of improv and StandUpComedy observations are pretty much even, and our objective here is just to correctly and accurately classify the posts in order to garner more information for the best metric to score these models on would be accuracy.

The 4 different metrics will be discussed later on in the project when evaluating the model.

---

### Web scraping

Web scraping was done from both subreddits using Pushshift's API. 
A loop was created to scrape 1000 post submissions at a time, starting from the latest posts until I had 2000 posts from the subreddit. The process was repeated for both subreddits and stored in 2 separate notebooks, named Project 3 part 1 and Project 3 part 2. Resulting data frames were stored as csv files in the 'datasets' folder and combined in Project 3 Main Body notebook.

---

### Data cleaning

The 2 data frames were combined and checked for null values which only appeared in the selftext column. Null values were replaced with "no_text" string values to be removed later on during pre processing as the titles from the posts could still be used.

Regex, BeautifulSoup html parser and other methods were used to remove HTML text, emoticons and emojis, emails, urls, "no_text" and other undesirable text that would have been noise to the model.

Duplicates were also removed and the final dataframe had 3920 entries which after eyeballing was sufficient for the pre-processing and modeling. 

Final dataset to be used for preprocessing was saved as a csv in the 'datasets' folder as combined_df.csv.

#### Data Dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|subreddit|object|combined_df|A specific online community, and the posts associated with it, on the social media website Reddit.|
|selftext|object|combined_df|Selftext: For self-posts, the body of the post from the subreddit.|
|title|object|combined_df|The title of the post on the subreddits that describe the post.|
|combined_text|object|combined_df|Combination of the selftext and title in that order.|
|lower_text|object|combined_df|combined_text in lower case.|

---

### Preprocessing

1. lower_text was tokenized using word_tokenize.
2. subreddit column was converted into 1 and 0 with 1 representing improv and 0 representing StandUpComedy.
3. PorterStemmer was used to stem the tokenized words.
4. WordNetLemmatizer was used to lemmatize tokenized words.
5. Stemming and Lemmatizing were compared and Lemmatizing was selected because stemming caused some words to be unrecognizable and nonsensical.

---

###  EDA and Visualization
Bar charts on unigrams, bigrams and trigrams were plot in order to visualize and obtain meaningful data for the model using both
1. CVEC (Count Vectorization)
2. TF-IDF (Term Frequency-Inverse Document Frequency)

Observations for unigrams:

1. Some common words found when checking the unigram include stop words or nonsensical words like "new" and "ha", the latter probably from when people are typing "haha" to simulate laughter.
2. There are also words that are common to both subreddits that might be meaningful, like "show".
3. There are some words that we can see come up uniquely in improv like "class", "scene" and "game", whereas StandUpComedy includes words like "comedian", "joke", "special" and "set".
4. There are predictor words in the unigram that are worth looking at in terms of significance.

Observations for bigrams:

There are fewer occurances for bigrams across the top 20, but it is worth noting that the words found here have less nonsensical words and are more unique to the individual subreddits. Bigrams like long form/short form and take class/taking classes for improv and open mic/open mics, new special and crowd work are common words associated with StandUpComedy.

Observations for trigrams:

Again, similar to bigram, the trigram returns results that are significantly smaller in values, but offer much more unique results than the unigram. Not much more meaningful information from the bigram, but the results are predictably hilarious for StandUpComedy. Short form game appears again in the improv trigram as with the bigram (short form) which seems to indicate it is a term associated commonly with improv. Same with "open mic" for StandUpComedy.

EDA and Visualization round up

The unigram, bigram and trigram all offer unique word/words that may prove useful when predicting. The words also seem pretty uniform across both TVEC and CVEC results in the unigram and bigram. The trigram however shows differing results for StandUpComedy between both vectorizers. I will be using both in the models and evaluate them accordingly.

---

### Modeling

Baseline was taken using the value counts of both subreddits. 
1   (improv)  0.501276
0   (StandUpComedy)  0.498724

An empty dataframe was created to append results from the models.
A function was then created in order to run the GridSearchCV and plot the confusion matrix for all the models in order to visualize the results of the predictions and also to obtain the best models with the best parameters and scores.

|cvec_tvec|classifier|cv_train|accuracy_train|accuracy_test|sensitivity_test|specificity_test|precision_test|
|--|--|--|--|--|--|--|--|
|CountVectorizer|MultinomialNB|0.8384|0.9102|0.8449|0.8635|0.8262|0.8330|
|TfidfVectorizer|MultinomialNB|0.8282|0.9388|0.8418|0.9022|0.7812|0.8055|
|CountVectorizer|LogisticRegression|0.8422|0.9027|0.8449|0.7475|0.9427|0.9291|
|TfidfVectorizer|LogisticRegression|0.8017|0.8252|0.7939|0.7515|0.8364|0.8218|

##### Best metric to use[](http://localhost:8889/notebooks/Documents/GA/my_materials/project_3/Project%203%20Main%20Body.ipynb#Best-metric-to-use)

Since the number of improv and StandUpComedy observations are pretty much even, and our objective here is just to correctly and accurately classify the posts in order to garner more information for the best metric to score these models on would be accuracy.

Based on accuracy, the Multinomial Naive Bayes models with both cvec and tvec are over fitted. The Logistic Regression model seems to return better results that will generalize better to unseen data.

The Logistic Regression model with both vectorizers are generally better fit, but the tvec model fits better, with lower accuracy scores. The model with cvec is a little more over fit than the model tvec, but has better accuracy scores. I will proceed with the interpretation of the coefficients with the 2 Logistic Regression models.

---

###  Interpreting Coefficients
Best models and best params:

1. CVEC LogisticRegression()
    Best Params: {'cvec__max_features': 10000, 'cvec__ngram_range': (1, 3), 'logreg__C': 0.1, 'logreg__penalty': 'l2', 'logreg__solver': 'liblinear'}
    
    
2. TVEC LogisticRegression()
    Best Params: {'logreg__C': 0.1, 'logreg__penalty': 'l2', 'logreg__solver': 'liblinear', 'tvec__max_features': 15000, 'tvec__ngram_range': (1, 3)}

#### Interpreting the coefficients for Logistic Regression with CountVectorizer[](http://localhost:8889/notebooks/Documents/GA/my_materials/project_3/Project%203%20Main%20Body.ipynb#Interpreting-the-coefficients-for-Logistic-Regression-with-CountVectorizer)

The log coefficient shown above next to the features show how strongly they predict for the 2 subbreddits. The higher the positive value, the better the word predicts for improv, whilst the smaller the negative value, the better it predicts for StandUpComedy.

As can be seen from the top 10 feature predictors for improv, 9 out of 10 are typical words associated with improv literature, namely, "class", "game", "theatre", "team", "troupe", "yes", "audition", "improvisers" and "improvise".

The top 10 feature predictors of StandUpComedy has 7 out of 10 words that are commonly associated with the genre, namely "joke", "comedian", "special", "comic", "mic", "crowd" and "material".

Most of the words are relavent and significant predictors of the 2 topics, improv and StandUpComedy.

#### Interpreting the coefficients for Logistic Regression with TfidfVectorizer[](http://localhost:8889/notebooks/Documents/GA/my_materials/project_3/Project%203%20Main%20Body.ipynb#Interpreting-the-coefficients-for-Logistic-Regression-with-TfidfVectorizer)

The log coefficient shown above next to the features show how strongly they predict for the 2 subbreddits. The higher the positive value, the better the word predicts for improv, whilst the smaller the negative value, the better it predicts for StandUpComedy.

Compared to using the CountVectorizer, usint TFIDfVectorizer has top features predicting improv and standup that are generally similar, but there are more words that are similar to stopwords that may not actually be significant to the topics.

---

### Conclusion
##### Problem statement and data gathering/cleaning:[](http://localhost:8889/notebooks/Documents/GA/my_materials/project_3/Project%203%20Main%20Body.ipynb#Problem-statement-and-data-gathering/cleaning:)

We set out to gather information that might be useful to your school in forming new classes in improv and StandUpComedy. In order to achieve this, we scraped the 4000 most recent posts from 2 subreddits, 2000 posts from each subreddit to use as a data so the information in that text should reflect current sentiment towards both topics.

Removal of stopwords and other key words that may have caused model over fitting was done over 3 rounds of testing with the models to get to the current iteration. It is worth noting that sometimes this trial and error process is necessary to get the results we want, and if future versions of this model are created, perhaps time, or resources can be allocated to this.

##### EDA and Visualization:[](http://localhost:8889/notebooks/Documents/GA/my_materials/project_3/Project%203%20Main%20Body.ipynb#EDA-and-Visualization:)

Through our EDA, and the visualizing of unigrams, bigrams and trigrams, we could see some of the common terms and phrases that were present in the different subreddits. Whilst the results were at times hilarious, we could also see patterns unique to each subreddit that were quite telling in differentiating two commonly mistakenly interchangible disciplines.

improv: is mainly a group activity and is commonly associated with scenes, long and short forms, and classes, and can be associated with not just comedy, but also any other form of artistic expression. It is also generally very positively portrayed as a team and group effort.

StandUpComedy: is mainly a solo performance which involves using humour and comedy as it's main entertainment medium. Some of the words associated with it indicate that it is a more popular form of performance in mainstream media, with words like mic, special(as in Netflix special or some other network special or comedy special) would indicate.

Although not in the top predictors for either subreddit, improv has a generally more positive tone to their posts and the art form is generally described as being supportive of the team members and reacting by always saying yes, and continuing to develop the scene. StandUpComedy on the other hand has some negative sounding phrases that can be construed as negative, for example in the trigrams above, "white trash mortgage", "xanax cure depression" and "red headed bastard". This could indicate that having classes for Stand Up Comedy might have some moral/political correctness implications.

##### Modelling:[](http://localhost:8889/notebooks/Documents/GA/my_materials/project_3/Project%203%20Main%20Body.ipynb#Modelling:)

As we have established that we are using accuracy as the metric to score the models, the LogisticRegression model with CountVectorizer has been selected. This is because it is acceptably fitted as the accuracy train and test scores are within 0.1 of each other, and the test accuracy score for this is also higher than the LogisticRegression model with TfidfVectorizer. The words with the strongest coefficients also make more sense for the LogisticRegression model with CountVectorizer. All models had very similar run times that were relatively fast.

Although we have picked a particular model to use, we can draw some useful information from the other models from the words and phrases that were thrown up in the EDA that will be discussed in the recomendations below.

##### Limitations and Next Steps[](http://localhost:8889/notebooks/Documents/GA/my_materials/project_3/Project%203%20Main%20Body.ipynb#Limitations-and-Next-Steps)

Due to time constraints, I was not able to explore Decision Tree and Random Forest models. I would like to explore their use in this particular project after today when time permits.

The requirements that were given by the performing arts centre were more exploratory in nature and hence kind of a "first step" in exploring these performing arts. As such, I would like to also improve on this project if given the opportunity by introducing sentiment analysis to the reddit posts to further gauge the prevailing attitudes towards both forms performing arts.

---

### Recommendations
1. Use the Logistic Regression model with CountVectorizer for the classifying of posts into the respective subreddits.

2. From the words with the highest coefficients that are commonly associated with the 2 categories:

- Improv: Is more likely to be a class that people will sign up for. It is not generally associated with mainstream media and from the terms that are highly important predictors, can be sold both to individuals or as a group package. As a class, the data shows that it would be easier to have a high student to teacher ratio as it can be taught in groups.

- Stand Up Comedy: Is more likely to be for solo performers. There is likely to be a people taking courses in this out of interest, but it is also likely that people who take this course want to make it a profession. Because it is a solo activity, the student to teacher ratio would most likely have to be smaller. Words like "special", "comedian" and "crowd" also references how popular stand up comedy is in popular culture. It could be worth cashing in on the popularity.

3. Based on point 2, pricing and marketing of these courses can be based on the above information to target individuals vs groups. Pricing can also be higher for the Stand Up Comedy class because of the resources required in a lower student to teacher ratio, and also because it is more likely that people would be willing to pay a bit more for classes in something that could eventually be a career.

4. Class syllabus for improv could be structured more towards building synergy and responding to other people in a group/team.

5. Class syllabus for Stand Up Comedy could focus more on cultivating the individual's sense of humour and developing the ability of individuals to properly tell their jokes from the setup, to the body and finally the punchline.

6. If your performing arts centre is concerned about maintaining a clean image, you might want to steer clear of Stand Up Comedy and focus instead on just doing improv. However, if you are of the opinion that all attention is good attention no matter how controversial, then definitely add in Stand Up Comedy classes.

---
