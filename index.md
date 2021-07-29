# Tutorial

In this tutorial, we will be exploring 

1. How to scrape text from wikipedia pages using python's `wikipedia` and `nltk` package
2. How to perform a frequency check on the content
3. Analyze the result from step 2: what aspect characterizes a city



The analysis will be performed on the 10 cities with the most billionaires in the world (April,2021): 

1. Beijing
2. New York City
3. Hong kong
4. Moscow
5. Shenzhen
6. Shanghai
7. London
8. San francisco, Mumbai
9. Hangzhou

[Data source][https://www.forbes.com/sites/johnhyatt/2021/04/06/worlds-richest-cities-the-top-10-cities-billionaires-call-home/]



1. Step: Tokenization

This step is called **tokenization**, it simply breaks the whole article into words and punctuations, producing the base for the analysis --- a list of words and punctuation. 

I wanted to be able to repeat the analysis, so I defined a function for the frequency analysis. This paragraph deals with the first part of the function, tokenization.

During tokenization, one should consider how to filter the content. Since the task at hand is to analyze how the cities are characterized, the semantic aspect sets the tone. 

After knowing what I wanted, I chose to use `regexp_tokenize()` from `nltk` because I wanted to remove all punctuations and numbers, since they do not contribute to semantic interpretation. Using regexp makes things a lot easier.

There are some other tokenizers from `nltk`, for example the function`word_tokenize()`, which extracts both characters and numbers based on Legality Principle and Onset Maximization. ([Read about Legality principle][http://www.nltk.org/_modules/nltk/tokenize/legality_principle.html])

Another problem regarding purifying the content is that there are words which occur at high frequency but do not say much about the city, for example "the", "it", etc. These are called the stop words and `nltk` provides a list of common stop words (`nltk.corpus.stopwords.words('...')`) for a user-selected language. 

However, this list does not contain every stop word (there are quite a few already), you might need to specify some stopwords on your own. I did it for "many" and "also".

```python
import wikipedia
import nltk
def frequencyCheck(content):
    #elements converted to lowercase
    content=content.lower()
    #1. remove all numbers
    pattern = r'[0-9]'
    content=re.sub(pattern,'',content)
    #2. take words of length >=2 only
    reg=nltk.regexp_tokenize(content, pattern='\w{2,}')
    #3. remove all stopwords
    sw = nltk.corpus.stopwords.words('english')
    words = []
    for word in reg:
        add = True
        for stopword in sw:
            # if a word is a stop word, do not add it into the array
            if word == stopword or word=="many" or word=="also":
                add = False
        if add == True:
            words.append(word)
    return words

```

2. Step:

```python
# #frequency check
def wordListToFreq(words):
    wordfreq = [words.count(p) for p in words]
    return dict(list(zip(words,wordfreq)))
```



```python
# #frequency check
def wordListToFreq(words):
    wordfreq = [words.count(p) for p in words]
    return dict(list(zip(words,wordfreq)))

def frequencyCheck(content):
    # make the content lower case regardless what
    content=content.lower()
    #1. remove all numbers
    pattern = r'[0-9]'
    content=re.sub(pattern,'',content)
    #2. take words of length >=2 only
    reg=nltk.regexp_tokenize(content, pattern='\w{2,}')
    #3. remove all stopwords
    sw = nltk.corpus.stopwords.words('english')
    words = []
    for word in reg:
        add = True
        for stopword in sw:
            # if a word is a stop word, do not add it into the array
            if word == stopword or word=="many" or word=="also":
                add = False
        if add == True:
            words.append(word)


#frequency in pairs
frequencyPair=wordListToFreq(words)    frequencyPair=dict(sorted(frequencyPair.items(), key=lambda kv: kv[1], reverse=True))
print(frequencyPair)

    return words

```











![8-San-Fracisco][https://postimg.cc/V0v2nqGT]

![8-Mumbai](https://postimg.cc/ZvTGfkfW)

![10-Hangzhou](https://postimg.cc/yD5Zhsf8)

