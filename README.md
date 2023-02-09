# Twitter-Sentiment-Analysis
# load packages
# Note: please install the Tweepy package if you haven't
# to do so, run "pip install tweepy" on your command line
`!pip install tweepy` command installs the tweepy package, which is a Python library for accessing the Twitter API. The "!" symbol is used to run shell commands in a Jupyter notebook or other environments, indicating that the following command should be executed in the terminal.

`!pip install vaderSentiment` command installs the `vaderSentiment` package, which is a Python library for performing sentiment analysis on texts. Like the previous command, the "!" symbol is used to run shell commands in the terminal, and the command installs the `vaderSentiment` package.


# Tweepy allows us to access the twitter API in python
import tweepy  

# Pandas will allow us to extract tweets/users and load the data into dataframe 
import pandas as pd

# JSON will allow us to work with JSON files
import json

# json_normalize() will allows us to normalize semi-structured JSON data into a flat table
from pandas import json_normalize

from collections import Counter


# Sets up the authentication for accessing the Twitter API using the tweepy library-
`consumer_key`, `consumer_secret`, `access_key`, and `access_secret` are string variables that store the credentials required to access the Twitter API. These credentials are specific to your Twitter account and you should use your own values instead of the examples shown in the code.

`auth` is an instance of the `tweepy.OAuthHandler` class that takes the `consumer_key` and `consumer_secret` as arguments and sets them as the authentication credentials.

The `set_access_token` method is then called on the `auth` object and takes the `access_key` and `access_secret` as arguments to set the access token for the API.

The `api` object is then created using the `tweepy.API` class and the `auth` object is passed as an argument. This `api` object can then be used to perform various actions, such as retrieving tweets, posting tweets, and more.



# Uses the `tweepy` library to retrieve the most recent 100 tweets from the Twitter account with the screen name  and store the data in several lists-

`ID`, `tweets`, `likes`, `time`, `retweet`, and `Source` are lists that will store the tweet information.
The `tweepy.Cursor` class is used to loop through the tweets and retrieve the required information. The `api.user_timeline` method is used to retrieve the tweets, and the `screen_name` argument is set to "iamchitrang" to specify the Twitter account. The `tweet_mode` argument is set to "extended" to retrieve the full text of tweets that were truncated in the previous API version.

The loop uses the `.items` method to retrieve the most recent 100 tweets and stores the tweet information in the respective lists. The information stored for each tweet includes the tweet ID, tweet text, number of likes, time the tweet was created, number of retweets, and source of the tweet.

# Generates a word cloud from the list of tweets retrieved previously using the tweets list-
`from wordcloud import WordCloud, STOPWORDS` imports the `WordCloud` class and the `STOPWORDS` constant from the `wordcloud` library. The `WordCloud` class is used to generate the word cloud, and `STOPWORDS` is a set of common stop words that can be filtered out when generating the word cloud.

`stopwords` is a set that contains the stop words from the `STOPWORDS` constant.
`unique_string` is a string that concatenates all of the tweets in the `tweets` list using the `join` method.
`wordcloud` is an instance of the `WordCloud` class that takes the `unique_string` as an argument and generates the word cloud. The `width`, `height`, and `max_words` arguments are used to set the width, height, and maximum number of words to display in the word cloud.

The `plt.figure` method creates a figure, and the `figsize` argument sets the size of the figure.
The `plt.imshow` method displays the image of the word cloud.
The `plt.axis` method sets the axis of the plot to be "off".
The `plt.tight_layout` method sets the layout of the plot to be tight, with a padding of 0.
The `plt.show` method displays the plot.



# The Vader Sentiment Analysis library to calculate the sentiment score of each tweet in the tweet_list column of the dataframe df-

`from vaderSentiment.vaderSentiment import SentimentIntensityAnalyzer` imports the `SentimentIntensityAnalyzer` class from the Vader Sentiment Analysis library.

`sentiment_analyzer_scores` is a function that takes as an argument a text and returns the sentiment score of the text using the `SentimentIntensityAnalyzer` class. The function creates an instance of the `SentimentIntensityAnalyzer` class and uses the `polarity_scores` method to get the sentiment score of the text. The sentiment score is a dictionary that contains several sentiment scores such as positive, negative, neutral, and compound scores. The compound score is a normalized, weighted composite score of the sentiment scores, and it ranges from -1 to 1.

`df['score'] = df['tweet_list'].apply(lambda x: sentiment_analyzer_scores(x))` creates a new column `'score'` in the dataframe `df` and populates it with the sentiment scores of the tweets. The apply method is used to apply the `sentiment_analyzer_scores` function to each element of the `'tweet_list'` column, and the resulting scores are stored in the `'score'` column. The lambda function is used to pass each tweet in the `'tweet_list'` column as an argument to the `sentiment_analyzer_scores` function.



