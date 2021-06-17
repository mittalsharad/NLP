# Tokenization

Solving an NLP problem is a multi-stage process. We need to clean the unstructured text data first before we can even think about getting to the modeling stage. Cleaning the data consists of a few key steps:

- Word tokenization
- Predicting parts of speech for each token
- Text lemmatization
- Identifying and removing stop words, and much more.

So, let's start with the very first and basic task of preprocessing text data **Tokenization** i.e sentence/word segmentation. 

For us humans to understand any given sentence or paragraph in English language, we read each word, interpret its meaning and read the next word till we encounter a full stop. Likewise, the model also needs all words separately making up the sentence. So, if we are given a paragraph, we need to get all sentences. From all these sentences, we need words & then only we can move on for any sort of prediction.

## What is Tokenization?

>Tokenization is essentially splitting a phrase, sentence, paragraph, or an entire text document into smaller units, such as individual words or terms. Each of these smaller units are called tokens.

So, simply we can say that it is nothing but splitting the large chunk into small chunks of words or sentences, called tokens. If the text is split into words, then its called as **Word Tokenization** and if it's split into sentences then its called as **Sentence Tokenization**.

The tokens could be words, numbers or punctuation marks. In tokenization, smaller units are created by locating word boundaries. Wait – what are word boundaries?

These are the ending point of a word and the beginning of the next word. These tokens are considered as a first step for stemming and lemmatization (the next stage in text preprocessing which we will cover in the next article). Generally 'space' is used to perform the word tokenization and characters like 'periods, exclamation point and newline char are used for Sentence Tokenization. 

let's see am example of Word and Sentence Tokenization:
![image](https://user-images.githubusercontent.com/22586467/122430559-578dbd80-cfb1-11eb-86fb-cf16880717cd.png)

## Why is Tokenization required in NLP?

Before processing a natural language, we need to identify the words that constitute a string of characters. That’s why tokenization is the most basic step to proceed with NLP (text data). This is important because **the meaning of the text could easily be interpreted by analyzing the words present in the text**.

Let’s take an example. Consider the string: “This is a cat.”

What do you think will happen after we perform tokenization on this string? We get [‘This’, ‘is’, ‘a’, cat’].

There are numerous uses of doing this. We can use this tokenized form to:
- Count the number of words in the text
- Count the frequency of the word, that is, the number of times a particular word is present

And so on. Once we have a list of words we can also use statistical tools and methods to get more insights into the text. For example, we can use word count and word frequency to find out important of word in that sentence or document.

## Different ways of Tokenization

There are multiple ways we can perform tokenization on given text data. We can choose any method based on language, library and purpose of modeling.
In this article, I am going to cover some of the major techniques which are:
1. Tokenization using Python’s split() function
2. Tokenization using Regular Expressions (RegEx)
3. Tokenization using NLTK
4. Tokenization using the spaCy library
5. Tokenization using Keras
6.  Tokenization using Gensim

Let's dive into each of these techniques one by one

### 1. Tokenization using Python’s split() function

Let’s start with the split() method as it is the most basic one. It returns a list of strings after breaking the given string by the specified separator. By default, split() breaks a string at each space. We can change the separator to anything. Let’s check it out.

**Word Tokenization**

```python
text = """Founded in 2002, SpaceX’s mission is to enable humans to become a spacefaring civilization and a multi-planet 
species by building a self-sustaining city on Mars. In 2008, SpaceX’s Falcon 1 became the first privately developed 
liquid-fuel launch vehicle to orbit the Earth."""
# Splits at space 
text.split() 
```
```
Output : ['Founded', 'in', '2002,', 'SpaceX’s', 'mission', 'is', 'to', 'enable', 'humans', 
          'to', 'become', 'a', 'spacefaring', 'civilization', 'and', 'a', 'multi-planet', 
          'species', 'by', 'building', 'a', 'self-sustaining', 'city', 'on', 'Mars.', 'In', 
          '2008,', 'SpaceX’s', 'Falcon', '1', 'became', 'the', 'first', 'privately', 
          'developed', 'liquid-fuel', 'launch', 'vehicle', 'to', 'orbit', 'the', 'Earth.']
```

**Sentence Tokenization**

This is similar to word tokenization. Here, we study the structure of sentences in the analysis. A sentence usually ends with a full stop (.), so we can use “.” as a separator to break the string:

```python
text = """Founded in 2002, SpaceX’s mission is to enable humans to become a spacefaring civilization and a multi-planet 
species by building a self-sustaining city on Mars. In 2008, SpaceX’s Falcon 1 became the first privately developed 
liquid-fuel launch vehicle to orbit the Earth."""
# Splits at '.' 
text.split('. ') 
```

```
Output : ['Founded in 2002, SpaceX’s mission is to enable humans to become a spacefaring 
           civilization and a multi-planet \nspecies by building a self-sustaining city on 
           Mars', 
          'In 2008, SpaceX’s Falcon 1 became the first privately developed \nliquid-fuel 
           launch vehicle to orbit the Earth.']
```
One major drawback of using Python’s split() method is that we can use only one separator at a time. Another thing to note – in word tokenization, split() did not consider punctuation as a separate token.

### 2.Tokenization using Regular Expressions (RegEx)

We can use the re library in Python to work with regular expression. This library comes preinstalled with the Python installation package.

Now, let’s perform word tokenization and sentence tokenization keeping RegEx in mind.

**Word Tokenization**
```python
import re
text = """Founded in 2002, SpaceX’s mission is to enable humans to become a spacefaring civilization and a multi-planet 
species by building a self-sustaining city on Mars. In 2008, SpaceX’s Falcon 1 became the first privately developed 
liquid-fuel launch vehicle to orbit the Earth."""
tokens = re.findall("[\w']+", text)
tokens
```

```
Output : ['Founded', 'in', '2002', 'SpaceX', 's', 'mission', 'is', 'to', 'enable', 
          'humans', 'to', 'become', 'a', 'spacefaring', 'civilization', 'and', 'a', 
          'multi', 'planet', 'species', 'by', 'building', 'a', 'self', 'sustaining', 
          'city', 'on', 'Mars', 'In', '2008', 'SpaceX', 's', 'Falcon', '1', 'became', 
          'the', 'first', 'privately', 'developed', 'liquid', 'fuel', 'launch', 'vehicle', 
          'to', 'orbit', 'the', 'Earth']
```
The re.findall() function finds all the words that match the pattern passed on it and stores it in the list.
The “\w” represents “any word character” which usually means alphanumeric (letters, numbers) and underscore (_). ‘+’ means any number of times. So [\w’]+ signals that the code should find all the alphanumeric characters until any other character is encountered.

**Sentence Tokenization**
To perform sentence tokenization, we can use the re.split() function. This will split the text into sentences by passing a pattern into it.

```import re
text = """Founded in 2002, SpaceX’s mission is to enable humans to become a spacefaring civilization and a multi-planet 
species by building a self-sustaining city on, Mars. In 2008, SpaceX’s Falcon 1 became the first privately developed 
liquid-fuel launch vehicle to orbit the Earth."""
sentences = re.compile('[.!?] ').split(text)
sentences
```

```
Output : ['Founded in 2002, SpaceX’s mission is to enable humans to become a spacefaring 
           civilization and a multi-planet \nspecies by building a self-sustaining city on 
           Mars.', 
          'In 2008, SpaceX’s Falcon 1 became the first privately developed \nliquid-fuel 
           launch vehicle to orbit the Earth.']
```

Here, we have an edge over the split() method as we can pass multiple separators at the same time. In the above code, we used the re.compile() function wherein we passed [.?!]. This means that sentences will split as soon as any of these characters are encountered.


### 3. Tokenization using NLTK
Now, this is a library you will appreciate the more you work with text data. NLTK, short for Natural Language ToolKit, is a library written in Python for symbolic and statistical Natural Language Processing.

NLTK contains a module called tokenize() which further classifies into two sub-categories:

- Word tokenize: We use the word_tokenize() method to split a sentence into tokens or words
- Sentence tokenize: We use the sent_tokenize() method to split a document or paragraph into sentences

Let’s see both of these one-by-one.

**Word Tokenization**
```
from nltk.tokenize import word_tokenize 
text = """Founded in 2002, SpaceX’s mission is to enable humans to become a spacefaring civilization and a multi-planet 
species by building a self-sustaining city on Mars. In 2008, SpaceX’s Falcon 1 became the first privately developed 
liquid-fuel launch vehicle to orbit the Earth."""
word_tokenize(text)
```

```
Output: ['Founded', 'in', '2002', ',', 'SpaceX', '’', 's', 'mission', 'is', 'to', 'enable', 
         'humans', 'to', 'become', 'a', 'spacefaring', 'civilization', 'and', 'a', 
         'multi-planet', 'species', 'by', 'building', 'a', 'self-sustaining', 'city', 'on', 
         'Mars', '.', 'In', '2008', ',', 'SpaceX', '’', 's', 'Falcon', '1', 'became', 
         'the', 'first', 'privately', 'developed', 'liquid-fuel', 'launch', 'vehicle', 
         'to', 'orbit', 'the', 'Earth', '.']
```
Notice how NLTK is considering punctuation as a token? Hence for future tasks, we need to remove the punctuations from the initial list.

**Sentence Tokenization**

```
from nltk.tokenize import sent_tokenize
text = """Founded in 2002, SpaceX’s mission is to enable humans to become a spacefaring civilization and a multi-planet 
species by building a self-sustaining city on Mars. In 2008, SpaceX’s Falcon 1 became the first privately developed 
liquid-fuel launch vehicle to orbit the Earth."""
sent_tokenize(text)
```

```
Output: ['Founded in 2002, SpaceX’s mission is to enable humans to become a spacefaring 
          civilization and a multi-planet \nspecies by building a self-sustaining city on 
          Mars.', 
         'In 2008, SpaceX’s Falcon 1 became the first privately developed \nliquid-fuel 
          launch vehicle to orbit the Earth.']
```

### 4. Tokenization using the spaCy library
spaCy is an open-source library for advanced Natural Language Processing (NLP). It supports over 49+ languages and provides state-of-the-art computation speed.

**Word Tokenization**

```
from spacy.lang.en import English

# Load English tokenizer, tagger, parser, NER and word vectors
nlp = English()

text = """Founded in 2002, SpaceX’s mission is to enable humans to become a spacefaring civilization and a multi-planet 
species by building a self-sustaining city on Mars. In 2008, SpaceX’s Falcon 1 became the first privately developed 
liquid-fuel launch vehicle to orbit the Earth."""

#  "nlp" Object is used to create documents with linguistic annotations.
my_doc = nlp(text)

# Create list of word tokens
token_list = []
for token in my_doc:
    token_list.append(token.text)
token_list
```

```
Output : ['Founded', 'in', '2002', ',', 'SpaceX', '’s', 'mission', 'is', 'to', 'enable', 
          'humans', 'to', 'become', 'a', 'spacefaring', 'civilization', 'and', 'a', 
          'multi', '-', 'planet', '\n', 'species', 'by', 'building', 'a', 'self', '-', 
          'sustaining', 'city', 'on', 'Mars', '.', 'In', '2008', ',', 'SpaceX', '’s', 
          'Falcon', '1', 'became', 'the', 'first', 'privately', 'developed', '\n', 
          'liquid', '-', 'fuel', 'launch', 'vehicle', 'to', 'orbit', 'the', 'Earth', '.']

```

**Sentence Tokenization**

```
from spacy.lang.en import English

# Load English tokenizer, tagger, parser, NER and word vectors
nlp = English()

# Create the pipeline 'sentencizer' component
sbd = nlp.create_pipe('sentencizer')

# Add the component to the pipeline
nlp.add_pipe(sbd)

text = """Founded in 2002, SpaceX’s mission is to enable humans to become a spacefaring civilization and a multi-planet 
species by building a self-sustaining city on Mars. In 2008, SpaceX’s Falcon 1 became the first privately developed 
liquid-fuel launch vehicle to orbit the Earth."""

#  "nlp" Object is used to create documents with linguistic annotations.
doc = nlp(text)

# create list of sentence tokens
sents_list = []
for sent in doc.sents:
    sents_list.append(sent.text)
sents_list
```

```
Output : ['Founded in 2002, SpaceX’s mission is to enable humans to become a spacefaring 
           civilization and a multi-planet \nspecies by building a self-sustaining city on 
           Mars.', 
          'In 2008, SpaceX’s Falcon 1 became the first privately developed \nliquid-fuel 
           launch vehicle to orbit the Earth.']
```


### 5. Tokenization using Keras 
Keras! One of the hottest deep learning frameworks in the industry right now. It is an open-source neural network library for Python. Keras is super easy to use and can also run on top of TensorFlow.

In the NLP context, we can use Keras for cleaning the unstructured text data that we typically collect.

**Word Tokenization**
```
from keras.preprocessing.text import text_to_word_sequence
# define
text = """Founded in 2002, SpaceX’s mission is to enable humans to become a spacefaring civilization and a multi-planet 
species by building a self-sustaining city on Mars. In 2008, SpaceX’s Falcon 1 became the first privately developed 
liquid-fuel launch vehicle to orbit the Earth."""
# tokenize
result = text_to_word_sequence(text)
result
```

 ```
 Output : ['founded', 'in', '2002', 'spacex’s', 'mission', 'is', 'to', 'enable', 'humans', 
          'to', 'become', 'a', 'spacefaring', 'civilization', 'and', 'a', 'multi', 
          'planet', 'species', 'by', 'building', 'a', 'self', 'sustaining', 'city', 'on', 
          'mars', 'in', '2008', 'spacex’s', 'falcon', '1', 'became', 'the', 'first', 
          'privately', 'developed', 'liquid', 'fuel', 'launch', 'vehicle', 'to', 'orbit', 
          'the', 'earth']
 ```
### 6. Tokenization using Gensim

For more info, refer [This website](https://www.machinelearningplus.com/gensim-tutorial/#2whatisadictionaryandcorpus)


**Word Tokenization**

```
from gensim.utils import tokenize
text = """Founded in 2002, SpaceX’s mission is to enable humans to become a spacefaring civilization and a multi-planet 
species by building a self-sustaining city on Mars. In 2008, SpaceX’s Falcon 1 became the first privately developed 
liquid-fuel launch vehicle to orbit the Earth."""
list(tokenize(text))
```

```
Outpur : ['Founded', 'in', 'SpaceX', 's', 'mission', 'is', 'to', 'enable', 'humans', 'to', 
          'become', 'a', 'spacefaring', 'civilization', 'and', 'a', 'multi', 'planet', 
          'species', 'by', 'building', 'a', 'self', 'sustaining', 'city', 'on', 'Mars', 
          'In', 'SpaceX', 's', 'Falcon', 'became', 'the', 'first', 'privately', 
          'developed', 'liquid', 'fuel', 'launch', 'vehicle', 'to', 'orbit', 'the', 
          'Earth']
```

**Sentence Tokenization**

To perform sentence tokenization, we use the split_sentences method from the gensim.summerization.texttcleaner class:

```

from gensim.summarization.textcleaner import split_sentences
text = """Founded in 2002, SpaceX’s mission is to enable humans to become a spacefaring civilization and a multi-planet 
species by building a self-sustaining city on Mars. In 2008, SpaceX’s Falcon 1 became the first privately developed 
liquid-fuel launch vehicle to orbit the Earth."""
result = split_sentences(text)
result
```

```
Output : ['Founded in 2002, SpaceX’s mission is to enable humans to become a spacefaring 
           civilization and a multi-planet ', 
          'species by building a self-sustaining city on Mars.', 
          'In 2008, SpaceX’s Falcon 1 became the first privately developed ', 
          'liquid-fuel launch vehicle to orbit the Earth.']
```

## End Notes

Tokenization is a critical step in the overall NLP pipeline. We cannot simply jump into the model building part without cleaning the text first.

In this article, we saw six different methods of tokenization (word as well as a sentence) from a given text. There are other ways as well but these are good enough to get you started on the topic.

I’ll be covering other text cleaning steps like removing stopwords, part-of-speech tagging, and recognizing named entities in my future posts. Till then, keep learning!
