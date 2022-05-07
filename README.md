# Analysis-of-Sentiments-of-COVID-19-Vaccination

## Objective
To analyze the common sentiments/views on effects & progress of COVID vaccination drive globally expressed on twitter via sentiment analysis using NLTK, VADER, Textblob API and ensemble method.

## Motivation
After considering our syllabus for the course, we were looking for some practically relevant problem statements where we could apply the learnings as well as extract some valuable result with whatever we had learnt.
COVID was (and is), still a part of our lives and hence the pandemic period dominated our thinking and led us to finding something there. Also, the recent maneuver of Elon Musk with twitter is hot and hence the off-spring: Twitter’s functioning in COVID.

## Methodology
Our main objective is to analyze the Tweets regarding Covid 19 vaccines and classify them as positive, neutral and negative. We have used two methods namely Sentiment analysis using Textblob and Sentiment analysis using NLTK Vader. Then we combined the two methods and did the composite sentiment analysis with the ensemble method. Our methods for the analysis of Covid-19 vaccine tweets involve four significant steps :-

## Data Collection
The following work employs a Kaggle dataset called “All COVID-19 Vaccines Tweets”. The data was collected using a Python package called Tweepy, which enables a user to access the Twitter API if they have successfully created a Twitter Developer account and obtained access credentials.
Below is the link to the original dataset.

https://www.kaggle.com/datasets/gpreda/all-covid19-vaccines-tweets?resource=download


## Exploratory Data Analysis
The primary goal of the exploratory data analysis phase of this project was to get acquainted with the columns of the data frame and start brainstorming research questions.
Starting with the step of loading the data using pandas, some basic data frame operations allow us to see that, for each tweet, all of the following information is available:
Information about the user who tweeted
user_name: Twitter handle
user_location: where in the world the person tweets from (NOTE: there is no validation here… “your bed” is technically acceptable)
user_description: user-written biography
user_created: when they created their Twitter account
user_followers: number of followers
user_friends: number of accounts the user is following
user_favourites: number of tweets the user has liked
user_verified: indicates if the user is a well-known figure (boolean)
Information about the tweet itself
id: indexing value for Twitter API
date: a datetime object in the form of YYYY-MM-DD HH:MM:SS
text: the tweet itself (**MOST IMPORTANT**)
hashtags: list of hashtags used in the tweet (without ‘#’ character)
source: which device was used for the tweet
retweets: number of retweets received at the time the data was collected
favorites: number of likes received at the time the data was collected
is_retweet: indicates if the tweet is original or a retweet (boolean)


Out of the above columns, text, date, user_name, user_location, hashtags, favorites, and retweets will be most relevant for this analysis. Though the tweets were queried using vaccine-related keywords, the specific vaccine being referred to in the tweet is not explicitly included as a column in the dataset. Therefore, we will need to filter for vaccine references in order to do any comparative analysis.


Which device are people tweeting about the vaccine from?


User verified?
Top 10 most retweeted tweets



## Preprocessing Data
Data cleaning involves transforming the raw data into a form that is more understandable, useful and efficient. Cleaned data can be easily interpreted by our machine learning algorithm. It is one of the most crucial steps in any machine learning model since it impacts the success and accuracy of our model. This process involves removing the duplicates, the redundant data and the outliers. It improves the quality of our dataset, helps in making accurate predictions and thereby, increases the overall accuracy of our model.
The extracted data in the CSV file is in raw form, so we need to clean and preprocess the data before training our model.

Major cleaning tasks we have performed include:

We have dropped the ID column as it does not help in our analysis.
Removing duplicate tweets.
Strip each tweet of mentions, hashtags, retweet information, and links using regular expressions.

## Sentiment analysis

### Sentiment Analysis with TextBlob
Pivoting to the sentiment analysis portion of this work, we can take this intuition of some of the tweets being informative and some of the tweets being opinionated to partition the greater discourse into separate sets of tweets with similar quantitative features. These features can be obtained using a Python package called TextBlob, which provides an API for NLP tasks such as part-of-speech tagging, noun phrase extraction, sentiment analysis, classification, translation, and more.
TextBlob returns polarity and subjectivity of a sentence. Polarity lies between [-1,1], -1 defines a negative sentiment and 1 defines a positive sentiment. Negation words reverse the polarity. TextBlob has semantic labels that help with fine-grained analysis. For example — emoticons, exclamation mark, emojis, etc. Subjectivity lies between [0,1]. Subjectivity quantifies the amount of personal opinion and factual information contained in the text. The higher subjectivity means that the text contains personal opinion rather than factual information. TextBlob has one more parameter — intensity. TextBlob calculates subjectivity by looking at the ‘intensity’. Intensity determines if a word modifies the next word. For English, adverbs are used as modifiers (‘very good’).

TextBlob is not context-aware, so the scores returned from its API should be interpreted loosely, in a way that prompts further analysis.


### Sentiment Analysis with NLTK Vader
Valence Aware Dictionary and sEntiment Reasoner (Vader) model, which is a lexicon and rule-based sentiment analysis tool aimed at sentiment analysis of social media text. It uses a bag of words approach with simple heuristics (e.g. increasing sentiment intensity in presence of certain words like “very”).
Vader returns compound scores, which are single unidimensional sentiment measures for a given text. The score ranges from -1 (most negative) to +1 (most positive), and the score for neutral sentiment is set arbitrarily between -0.05 and 0.05. We have chosen neutral threshold to be 0.01.

### Composite sentiment with ensemble method - 
Ensemble method is used to create a composite score from the average of different  sentiment scores. Both NLTK Vader and TextBlob scores were already in the range [-1,1], and were given equal weights when computing the mean.
As with previous steps, score ≥0.05 was defined as Positive, score ≤-0.05 was defined as Negative, and anything in between was set as Neutral. 

## Results
We were looking for some practically relevant output from this project and this is what we found. 

![1](https://user-images.githubusercontent.com/63241474/167245040-cf5ec213-81b7-4592-9fbb-65a7482e1b65.png)

![2](https://user-images.githubusercontent.com/63241474/167245047-d2399b66-e88c-40d4-8395-2c391956d2f2.png)

![3](https://user-images.githubusercontent.com/63241474/167245077-b1d706cb-8d56-4112-a49c-1db8234043b3.png)

## Conclusion/Findings
Our limited analysis indicates that the proportion of positive sentiments (51.4%) is  greater that of negative sentiments (18.7%). This suggests that the general sentiment towards COVID-19 vaccine at the point of analysis tends to be on a positive side which indicates that people were willing to get vaccinated.
