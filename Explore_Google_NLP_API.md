# EC601-
EC601 A2 Product Design in Electrical and Computer Engineering (Fall 2021)

## Exploring the Google NLP API

Using the Google NLP API to perform Sentiment Analysis on a string and finding out the Score and Magnitude using the Natural Language API.The Score of the sentiment ranges between -1.0 (negative) and 1.0 (positive) and corresponds to the overall sentiment from the given information.The Magnitude of the sentiment ranges from 0.0 to +infinity and indicates the overall strength of sentiment from the given information. The more information that is provided the higher the magnitude. 

When expressing strong emotions, such as "Boston is a particularly good city", the result obtained by using sentiment analysis is shown below.

> text = "Boston is a particularly good city"
> 
> analyze_text_sentiment(text)
> 
> > text      : Boston is a particularly good city
> >
> > score     : 80.0%
> >
> > magnitude : 80.0%

When expressing relatively flat emotions, that is, emotions are neutral and do not favor positive or negative emotions, the calculated score of the sentient will be relatively low. For example, "I had lunch at 11:00 this morning", the results obtained by using text emotion analysis are shown in the figure below.

> text = "I had lunch at 11 this morning"
> 
> analyze_text_sentiment(text)
>
> > text      : I had lunch at 11 this morning
> >
> > score     : 0.0%
> > 
> > magnitude : 0.0%

The functions of sentiment analysis are as follows.

``` Python
from google.cloud import language


def analyze_text_sentiment(text):
    client = language.LanguageServiceClient()
    document = language.Document(content=text, type_=language.Document.Type.PLAIN_TEXT)

    response = client.analyze_sentiment(document=document)

    sentiment = response.document_sentiment
    results = dict(
        text=text,
        score=f"{sentiment.score:.1%}",
        magnitude=f"{sentiment.magnitude:.1%}",
    )
    for k, v in results.items():
        print(f"{k:10}: {v}")
``` 
