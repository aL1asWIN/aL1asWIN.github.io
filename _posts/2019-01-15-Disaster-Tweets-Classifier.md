---
layout: post
title: "Disaster Tweets Classifier"
featured-img:
categories: [Project, NLP]
---

Design:
In this project we sought to make initial steps toward designing and implementing a web-tool or an app for rapid alert and notification about a disastrous event, in close to real time. The tool ideally would alert about the event, similar, for example, to earthquake or tsunami warnings that appear on Google's home page immediately after a major disaster. While traditional methods for alerting on such events rely on official information derived from official sources (e.g. USGS), this tool will utilize social media activity to identify these events and alert when an event first occurs.

The question we look at primarily here is, given a sea of text content from social media platforms, how do you identify what is relevant information for emergency response personnel? And what sort of implementation would be valuable?

_Applied Tools:_

- webscraping
- APIs
- Natural Language Processing (NLP)   

### Data <a name="Data"></a>

- Using Twitter API keys to pull tweets using tweet ids. Need to apply for a key in order to use Twitter's API to obtain consumer key, consumer secret key, oauth token, oath secret. Twython (Python wrapper for the Twitter API) Designed a Tweet Pull Function and While Loop to run through a list of tweet ids in chunks of 900 repeatedly. Ran in tandem with multiple app keys
- Training data: Pulled all 180000 tweets from the peak disaster period (1 hour before landfall in NJ/NY to 2 hours after) in hopes of getting a maximum number of critical tweets to train with
- Test data: Pulled a random sample of ~40000 of the two million tweets after that point to test on.

### Setting up tweet pulls
```python
# these are your twitter credentials to be able to pull the tweets
CONSUMER_KEY = 'INSERT KEY HERE'
CONSUMER_SECRET = 'INSERT KEY HERE'
OAUTH_TOKEN = 'INSERT KEY HERE'
OAUTH_SECRET = 'INSERT KEY HERE'

# loading in Twython to use our credentials
twitter = Twython(CONSUMER_KEY, CONSUMER_SECRET, OAUTH_TOKEN, OAUTH_SECRET)

# defining a function to start pulling tweets at a specific point
# Twitter only allows you to pull 900 tweets within a 15 minute period
def tweet_pull(start_index):
    tweet = None
    lst = []
    for i in tqdm(range(start_index,start_index+900)):
        try:
            dct = twitter.show_status(id=str(sandy_train_ids['tweet_id'][i]))
            lst.append(dct)
        except:
            tweet = None
        sandy_train_ids.set_value(i, 'tweet_texts', tweet)
    return [start_index+900,lst]
    
#While loop for tweet pulling
#Simply set count = [index you want to start at], and set while count < [index you want to end at] (multiple of 900, ideally)
#The while loop will run through all the indices in pulls of 900, shifting the start index up 900 each time,
#and sleeping 15 minutes after each pull to make sure we are never drawing on empty.
#The pulls are added to a single list of dictionaries that can be converted into a df.

count = 0
tweets = []
while count < 3600:    
    pull = tweet_pull(count)
    tweets.extend(pull[1])
    count = pull[0]
    sleep(900) #15 minute wait before starting the next loop
```
