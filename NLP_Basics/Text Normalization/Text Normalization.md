# Text Normalization

In any natural language, depending on situation, we can represent the same word in more than one form. That’s what makes the language such a thrilling part of our lives, right? For example:

- She ate the food and washed the dishes.
- They were eating noodles at a cafe.
- Don’t you want to eat before we leave?
- We have just eaten our breakfast.
- It also eats fruit and vegetables.

In all these sentences, we can see that the word `eat` has been used in multiple forms. For us humans, it is very easy to understand that eating is the activity here. So it doesn’t really matter to us whether it is ‘ate’, ‘eat’, or ‘eaten’ – we know what is going on.

Unfortunately, it's not that simple for machines. They treat these words differently. Therefore, we need to normalize them to their root word, which is “eat” in our example.

Hence, **Text Normalization is a process of transforming a word into a single canonical or base form**. This can be done by two processes, `stemming` and `lemmatization`.

## Background

The Languages we speak and write are all made up of several words which are derived from one another. When a language contains words that are derived from another word as their use in the speech changes is called `Inflected Language`.

> In grammar, inflection is the modification of a word to express different grammatical categories such as tense, case, voice, aspect, person, number, gender, and mood. An inflection expresses one or more grammatical categories with a prefix, suffix or infix, or another internal modification such as a vowel change" [Wikipedia]

Let's take a few examples:

![image](https://user-images.githubusercontent.com/22586467/122587918-11e9f700-d07c-11eb-8134-0e5a2adb0476.png)

This example might have given you a little idea of what we are trying to achieve.

Now, Let’s see both of them in detail.

## What are Stemming and Lemmatization?
 
> Stemming and Lemmatization is simply normalization of words, which means reducing a word to its root form.

In most natural languages, a root word can have many variants. For example, the word ‘play’ can be used as ‘playing’, ‘played’, ‘plays’, etc. You can think of similar examples (and there are plenty)

### Stemming

> "Stemming is the process of reducing inflection in words to their root forms such as mapping a group of words to the same stem even if the stem itself is not a valid word in the Language."

Stemming is a text normalization technique that cuts off the end or beginning of a word by taking into account a list of common prefixes or suffixes that could be found in that word

### Lemmatization

> Lemmatization, unlike Stemming, reduces the inflected words properly ensuring that the root word belongs to the language. In Lemmatization root word is called Lemma. A lemma (plural lemmas or lemmata) is the canonical form, dictionary form, or citation form of a set of words.

For example, runs, running, ran are all forms of the word run, therefore run is the lemma of all these words. Because lemmatization returns an actual word of the language, it is used where it is necessary to get valid words.

## Methods to Perform Text Normalization

**1. Text Normalization using NLTK**

`PorterStemmer()` and `WordNetLemmatizer()` can be used in NLTK for Stemming and Lemmatization respectively.

**Stemming**
```python
from nltk.corpus import stopwords
from nltk.tokenize import word_tokenize 
from nltk.stem import PorterStemmer

set(stopwords.words('english'))

text = """He determined to drop his litigation with the monastry, and relinguish his claims to the wood-cuting and 
fishery rihgts at once. He was the more ready to do this becuase the rights had become much less valuable, and he had 
indeed the vaguest idea where the wood and river in question were."""

stop_words = set(stopwords.words('english')) 
  
word_tokens = word_tokenize(text) 
    
filtered_sentence = [] 
  
for w in word_tokens: 
    if w not in stop_words: 
        filtered_sentence.append(w) 

Stem_words = []
ps =PorterStemmer()
for w in filtered_sentence:
    rootWord=ps.stem(w)
    Stem_words.append(rootWord)
print("Filtered Sentencs:")
print(filtered_sentence)
print("Stemmed Words:")
print(Stem_words)
```
Output
```python
Filtered Sentencs:

He determined drop litigation monastry, relinguish claims wood-cuting fishery rihgts. He 
ready becuase rights become much less valuable, indeed vaguest idea wood river question.

Stemmed Words:
He determin drop litig monastri, relinguish claim wood-cut fisheri rihgt. He readi becuas
right become much less valuabl, inde vaguest idea wood river question.
```
**Lemmatization**
```python
from nltk.corpus import stopwords
from nltk.tokenize import word_tokenize 
import nltk
from nltk.stem import WordNetLemmatizer
set(stopwords.words('english'))

text = """He determined to drop his litigation with the monastry, and relinguish his claims to the wood-cuting and 
fishery rihgts at once. He was the more ready to do this becuase the rights had become much less valuable, and he had 
indeed the vaguest idea where the wood and river in question were."""

stop_words = set(stopwords.words('english')) 
  
word_tokens = word_tokenize(text) 
    
filtered_sentence = [] 
  
for w in word_tokens: 
    if w not in stop_words: 
        filtered_sentence.append(w) 
print("Filtered Sentence:") 
print(filtered_sentence) 

lemma_word = []
import nltk
from nltk.stem import WordNetLemmatizer
wordnet_lemmatizer = WordNetLemmatizer()
for w in filtered_sentence:
    word1 = wordnet_lemmatizer.lemmatize(w, pos = "n")
    word2 = wordnet_lemmatizer.lemmatize(word1, pos = "v")
    word3 = wordnet_lemmatizer.lemmatize(word2, pos = ("a"))
    lemma_word.append(word3)
print("Lemmatized words:")
print(lemma_word)
```
Output
```python
Filtered Sentence:
He determined drop litigation monastry, relinguish claims wood-cuting fishery rihgts. He 
ready becuase rights become much less valuable, indeed vaguest idea wood river question.

Lemmatized words:
He determined drop litigation monastry, relinguish claim wood-cuting fishery rihgts. He 
ready becuase right become much le valuable, indeed vaguest idea wood river question.
```

> Here, v stands for verb, a stands for adjective and n stands for noun. The lemmatizer only lemmatizes those words which match the pos parameter of the lemmatize method.

Lemmatization is done on the basis of part-of-speech tagging (POS tagging). We’ll talk in detail about POS tagging in an upcoming article.

**2. Text Normalization using spaCy**

SpaCy is an amazing NLP library. It provides many industry-level methods to perform lemmatization. Unfortunately, spaCy has no module for stemming. To perform lemmatization, check out the below code:
```python
#make sure to download the english model with "python -m spacy download en"

import en_core_web_sm
nlp = en_core_web_sm.load()

doc = nlp(u"""He determined to drop his litigation with the monastry, and relinguish his claims to the wood-cuting and 
fishery rihgts at once. He was the more ready to do this becuase the rights had become much less valuable, and he had 
indeed the vaguest idea where the wood and river in question were.""")

lemma_word1 = [] 
for token in doc:
    lemma_word1.append(token.lemma_)
lemma_word1
```
Output
```python
-PRON- determine to drop -PRON- litigation with the monastry, and relinguish -PRON- claim
to the wood-cuting and \n fishery rihgts at once. -PRON- be the more ready to do this 
becuase the right have become much less valuable, and -PRON- have \n indeed the vague idea
where the wood and river in question be.
```

Here -PRON- is the notation for pronoun which could easily be removed using regular expressions. The benefit of spaCy is that we do not have to pass any pos parameter to perform lemmatization.

