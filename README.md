# Download_tweets_with_python_Twitter_API
Tutorial for downloading live tweets from Twitter API with python tweepy



Twitter
1. Create Twitter Developer Account

Go to: https://developer.twitter.com/en/apply-for-access and apply for a developer account.

Once you get access to your developer account you will be able to use Twitter API for your project.

You should read the "Restricted use cases" before starting your project just to be on the safe side.

2. Create an App

While logged in go to: https://developer.twitter.com/en/apps/create

Give a description of your project and fill the required fields

Once you have your new app you will be able to access it. Inside your app there is a tab called "Keys and Tokens".

You will be able to generate "Consumer API keys" and "Access token & access token secret". These series of codes will be used later for downloading live tweets

You are good to go

Python

1. Importing libraries

import tweepy

import csv

import pandas as pd


2. insert App credentials

consumer_key = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxx' #insert your API key
consumer_secret = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' #insert your API secret key
access_token = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' #insert Access token
access_token_secret = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' #Access token secret
auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)
api = tweepy.API(auth,wait_on_rate_limit=True)

3. Create a csv.file that will hold all the downloaded tweets

csvFile = open('tweets.csv', 'a')

4. Write tweets in the csv file

csvWriter = csv.writer(csvFile)
for tweet in tweepy.Cursor(api.search,q="#xxxx",count=100,   # instead of xxxx you can use any hashtag of your choise
                           lang="en",
                           since="xxxx-xx-xx").items():     #xxxx-xx-xx use date(you can go back 2 weeks before present date)
    print (tweet.created_at, tweet.text, 'utf-8')
    csvWriter.writerow([tweet.created_at, tweet.text.encode('utf-8')])
    
   
