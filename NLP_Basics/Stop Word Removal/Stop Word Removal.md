# Stop Word Removal

![image](https://user-images.githubusercontent.com/22586467/122515936-c3ad0780-d02b-11eb-89dd-b71b72349b5d.png)

In the previous article, I talked about the first step for any NLP task i.e. "Tokenization". Now, lets move forward with the next tasks which involves **removing stop words**. We will also see how to perform this using some of the most popular python libraries.

## Stop word

Alphabet letters are building blocks for words in the English language. These words group together to form a sentence by following grammatical rules. Because of grammatical reasons, some words occur more frequently than other words. The main goal of these words is to connect different words in a sentence. These words are known as Stopwords. Generally, Stopwords carry no dictionary meaning.

>
Generally, the most common words used in a text are “the”, “is”, “in”, “for”, “where”, “when”, “to”, “at” etc.

Consider this text string – “There is a horse in the garden”. Now, the words “is”, “a”, “in”, and  “the” add no meaning to the statement while parsing it. Whereas words like “there”, “horse”, and “garden” are the keywords and tell us what the statement is all about.

Also, keep in mind that we need to perform tokenization before removing any stopwords. If you want, you to go through my article below on [**Tokenization**](https://github.com/mittalsharad/NLP/blob/main/NLP_Basics/Tokenization/Tokenization.md)


## Why do we Need to Remove Stopwords?

This is an important question and I believe most of you have the same in mind.

To answer this, Stopword removal is not a hard and fast rule in NLP. It depends upon the task that we are working on. For tasks like text classification, where the text is to be classified into different categories, stopwords are removed or excluded from the given text so that more focus can be given to those words which define the meaning of the text. Just like we saw in the above section, words like there, horse, and garden add more meaning to the text as compared to the words is and on.

However, in tasks like [machine translation](https://www.analyticsvidhya.com/blog/2019/01/neural-machine-translation-keras/?utm_source=blog&utm_medium=how-to-remove-stopwords-text-normalization-nltk-spacy-gensim-python) and [Text summarization](https://www.analyticsvidhya.com/blog/2019/06/comprehensive-guide-text-summarization-using-deep-learning-python/?utm_source=blog&utm_medium=how-to-remove-stopwords-text-normalization-nltk-spacy-gensim-python), removing stopwords is not advisable.

Some key benefits of removing stopwords are:
- On removing stopwords, dataset size decreases and the time to train the model also decreases
- Removing stopwords can potentially help improve the performance as there are fewer and only meaningful tokens left. Thus, it could increase classification accuracy
- Even search engines like Google remove stopwords for fast and relevant retrieval of data from the database

## When Should we Remove Stopwords?

Let's summarize this into when we can remove stopwords and when we should avoid doing so.

**1. Remove Stopwords**
- Text Classification
- Spam Filtering
- Language Classification
- Genre Classification
- Caption Generation
- Auto-Tag Generation
 
**2. Avoid Stopword Removal**
- Machine Translation
- Language Modeling
- Text Summarization
- Question-Answering problems

Feel free to add more NLP tasks to this list!

## Different Methods to Remove Stopwords

We  can use NLTK, spaCy and Gensim libraries for removing stop words from a text corpus. Let's see each of them one by one.

#### 1. Stopword Removal using NLTK

NLTK, or the Natural Language Toolkit, is a treasure trove of a library for text preprocessing. It’s one of my favorite Python libraries. NLTK has a list of stopwords stored in 16 different languages.

You can use the below code to see the list of stopwords in NLTK:

```python
import nltk
from nltk.corpus import stopwords
set(stopwords.words('english'))
```
Now, to remove stopwords using NLTK, you can use the following code block. 

```python
text = "Nick likes to play football, however he is not too fond of tennis."
text_tokens = word_tokenize(text)
tokens_without_sw = [word for word in text_tokens if not word in stopwords.words()]
```

#### 2. Stopword Removal using spaCy
spaCy is one of the most versatile and widely used libraries in NLP. We can quickly and efficiently remove stopwords from the given text using SpaCy. It has a list of its own stopwords that can be imported as STOP_WORDS from the spacy.lang.en.stop_words class.

```python
text = "Nick likes to play football, however he is not too fond of tennis."
text_tokens = word_tokenize(text)
tokens_without_sw= [word for word in text_tokens if not word in all_stopwords]

```
An important point to note – stopword removal doesn’t take off the punctuation marks or newline characters. We will need to remove them manually.

#### 3. Stopword Removal using Gensim
Gensim is a pretty handy library to work with on NLP tasks. While pre-processing, gensim provides methods to remove stopwords as well. We can easily import the remove_stopwords method from the class gensim.parsing.preprocessing.

```python
from gensim.parsing.preprocessing import remove_stopwords

text = "Nick likes to play football, however he is not too fond of tennis."
filtered_sentence = remove_stopwords(text)
```
While using gensim for removing stopwords, we can directly use it on the raw text. There’s no need to perform tokenization before removing stopwords. This can save us a lot of time.

## End Notes

Thats all related for Stop word Removal.

All the code blocks are explained in more details in the [Notebook](https://github.com/mittalsharad/NLP/blob/main/NLP_Basics/Stop%20Word%20Removal/Stop%20Word%20Removal.ipynb), alone with some extra information to make the task more refined.
