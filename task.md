Identify up to 10 cities around the world (including Exeter) that are described on Wikipedia. 

Using text-mining, download the text describing each city. After cleaning the text, perform a frequency analysis to discover the most prominent concepts adopted in describing each city. 

Colour each word according to its sentiment score from VADER and produce a word cloud of these concepts, one for each city. 

Are there systematic differences to observe? 

In describing cities, concepts like "greenery" or "art" were mentioned more or less frequently? 

Implement all the above steps as a mini-tutorial on an HTML webpage, so that the analysis is fully automated and results between different cities can be visualised and compared.

-----

Tutorial

In this tutorial, we will be exploring 

1. How to scrape text from wikipedia page
2. How to perform a frequency check on the page
3. Analyze the result from step 2 and discover which word characterizes the city the best using sentiment score

First step:

This step is called **tokenization**, and it produces our familiar structure, a list of words and punctuation.





# Question

How to find out the sentiment score?