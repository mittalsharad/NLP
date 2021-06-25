# Term Frequency-Inverse Document Frequency (TF-IDF)

> “Term frequency–inverse document frequency, is a numerical statistic that is intended to reflect how important a word is to a document in a collection or corpus.” [Wikipedia]

## Term Frequency (TF)

Let’s first understand Term Frequent (TF). It is a measure of how frequently a term, t, appears in a document, d:

![image](https://user-images.githubusercontent.com/22586467/123376799-b4d4d080-d5a8-11eb-88de-925e3bd44373.png)

Here, in the numerator, n is the number of times the term “t” appears in the document “d”. Thus, each document and term would have its own TF value.

Let's take an example to understand this better:

  Review: This movie is not scary and is slow

Here,

- Vocabulary: ‘This’, ‘movie’, ‘is’, ‘very’, ‘scary’, ‘and’, ‘long’, ‘not’,  ‘slow’, ‘spooky’,  ‘good’
- Number of words in Review = 8
- TF for the word ‘this’ = (number of times ‘this’ appears in review)/(number of terms in review) = 1/8

Similarly,

- TF(‘movie’) = 1/8
- TF(‘is’) = 2/8 = 1/4
- TF(‘very’) = 0/8 = 0
- TF(‘scary’) = 1/8
- TF(‘and’) = 1/8
- TF(‘long’) = 0/8 = 0
- TF(‘not’) = 1/8
- TF(‘slow’) = 1/8
- TF( ‘spooky’) = 0/8 = 0
- TF(‘good’) = 0/8 = 0

## Inverse Document Frequency (IDF)

IDF is a measure of how important a term is. We need the IDF value because computing just the TF alone is not sufficient to understand the importance of words:

![image](https://user-images.githubusercontent.com/22586467/123378743-c28b5580-d5aa-11eb-8135-2e922f27dedc.png)

We can calculate the IDF values for the all the words in Review:

IDF(‘this’) =  log(number of documents/number of documents containing the word ‘this’) = log(3/3) = log(1) = 0

Similarly,

- IDF(‘movie’, ) = log(3/3) = 0
- IDF(‘is’) = log(3/3) = 0
- IDF(‘not’) = log(3/1) = log(3) = 0.48
- IDF(‘scary’) = log(3/2) = 0.18
- IDF(‘and’) = log(3/3) = 0
- IDF(‘slow’) = log(3/1) = 0.48

Hence, we see that words like “is”, “this” etc., are reduced to 0 and have little importance; while words like “scary”, “slow”, etc. are words with more importance and thus have a higher value.

We can now compute the TF-IDF score for each word in the corpus. Words with a higher score are more important, and those with a lower score are less important:
![image](https://user-images.githubusercontent.com/22586467/123379106-42b1bb00-d5ab-11eb-8cbf-590feb9f148d.png)

We can now calculate the TF-IDF score for every word in Review 2:

TF-IDF(‘this’, Review) = TF(‘this’, Review) * IDF(‘this’) = 1/8 * 0 = 0

Similarly,

TF-IDF(‘movie’, Review) = 1/8 * 0 = 0
TF-IDF(‘is’, Review) = 1/4 * 0 = 0
TF-IDF(‘not’, Review) = 1/8 * 0.48 = 0.06
TF-IDF(‘scary’, Review) = 1/8 * 0.18 = 0.023
TF-IDF(‘and’, Review) = 1/8 * 0 = 0
TF-IDF(‘slow’, Review) = 1/8 * 0.48 = 0.06

Let's see the Tf-IDF for multiple reviews:

Review 1: This movie is very scary and long
Review 2: This movie is not scary and is slow
Review 3: This movie is spooky and good

![image](https://user-images.githubusercontent.com/22586467/123379731-2bbf9880-d5ac-11eb-8a3e-3f99364e47ab.png)

We have now obtained the TF-IDF scores for our vocabulary. TF-IDF also gives larger values for less frequent words and is high when both IDF and TF values are high i.e the word is rare in all the documents combined but frequent in a single document.

For implementation, refer Notebook
