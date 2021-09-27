# EC601-
EC601 A2 Product Design in Electrical and Computer Engineering (Fall 2021)

## Exploring the Twitter API

Use the request module in the twitter API to filter and track real-time tweets.After creating a personal project and creating a new app in the developer portal, obtain the token and enter the personal API in the program_ key， API_ secret, access_ token_ key， access_ token_ Secret to request access to the twitter server and obtain real-time user and tweet data.

The tracking term set by this simple program is' covid 19 ', and the location range of filtered tweeting users is set (San Francisco is set in the program). It can be seen from the graph of the result that tweets containing tracking terms can be successfully obtained from the returned data.

![image](https://user-images.githubusercontent.com/90360797/134836493-56a1959f-bfe0-4d46-af4a-0b6c538fc09d.png)

In addition, we can also change the tracking term of tweets to 'restaurant', and filter the user's tweeting location to the longitude and latitude range of New York. This gives Twitter users a rough idea of the restaurants in New York.

![image](https://user-images.githubusercontent.com/90360797/134837563-06794319-4c81-4f3f-878c-399747a473fc.png)

The python program for tracking specific terms and filtering location information is shown below.

```Python
# -*- coding:utf-8 -*-
from TwitterAPI import TwitterAPI
from TwitterAPI import TwitterPager

the_consumer_key = "<the_consumer_key>" 
the_consumer_secret = "<the_consumer_secret>"
the_access_token_key = "<the_access_token_key>"
the_access_token_secret = "<the_access_token_secret>"

api = TwitterAPI(consumer_key=the_consumer_key,
                consumer_secret=the_consumer_secret,
                access_token_key=the_access_token_key,
                access_token_secret=the_access_token_secret)

   
def stream_tweets(TRACK_TERM, TRACK_LOCATION, api):
    r = api.request('statuses/filter', {'track': TRACK_TERM, 'locations': TRACK_LOCATION})
    for item in r:
        print( item['text'] if 'text' in item else item, '\n' )
 
if __name__ == "__main__":
    TRACK_TERM = 'Restaurant'
    TRACK_LOCATION = '-74,40,-73,41' # New York City
    stream_tweets(TRACK_TERM, TRACK_LOCATION, api)
```
