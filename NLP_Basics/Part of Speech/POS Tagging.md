# Part of Speech (PoS) Tagging

>Knowledge of languages is the doorway to wisdom. – Roger Bacon
                                                              
Today, the way of understanding languages has changed a lot. We now refer to it as linguistics and natural language processing. But its importance hasn’t diminished; instead, it has increased tremendously. Each of these applications involve complex NLP techniques and to understand these, one must have a good grasp on the basics of NLP. Therefore, before going for complex topics, keeping the fundamentals right is important.

That’s why I have created this article in which I will be covering some basic concepts of NLP – Part-of-Speech (POS) tagging, Dependency parsing, and Constituency parsing in natural language processing. We will understand these concepts and also implement these in python. So let’s begin!

## Part-of-Speech(POS) Tagging

In our school days, all of us have studied the parts of speech, which includes nouns, pronouns, adjectives, verbs, etc. Words belonging to various parts of speeches form a sentence. Knowing the part of speech of words in a sentence is important for understanding it.

That’s the reason for the creation of the concept of POS tagging. I’m sure that by now, you have already guessed what POS tagging is. Still, allow me to explain it to you.
> Part-of-Speech(POS) Tagging is the process of assigning different labels known as POS tags to the words in a sentence that tells us about the part-of-speech of the word.

Broadly there are two types of POS tags:

**1. Universal POS Tags:** 
These tags are used in the Universal Dependencies (UD) (latest version 2), a project that is developing cross-linguistically consistent treebank annotation for many languages. These tags are based on the type of words. E.g., NOUN(Common Noun), ADJ(Adjective), ADV(Adverb).

![image](https://user-images.githubusercontent.com/22586467/123293375-8d8eec80-d531-11eb-9d2b-6285ea3f07cf.png)

You can read more about each one of them [here](https://universaldependencies.org/u/pos/).

**2. Detailed POS Tags:** 
These tags are the result of the division of universal POS tags into various tags, like NNS for common plural nouns and NN for the singular common noun compared to NOUN for common nouns in English. These tags are language-specific. You can take a look at the complete list [here](https://spacy.io/api/data-formats#pos-en).

```python
import spacy
nlp=spacy.load('en_core_web_sm')
 
text='It took me more than two hours to translate a few pages of English.'

for token in nlp(text):
 print(token.text, '=>',token.pos_,'=>',token.tag_)
 ```
 Output
 ```
 It => PRON => PRP
took => VERB => VBD
me => PRON => PRP
more => ADJ => JJR
than => SCONJ => IN
two => NUM => CD
hours => NOUN => NNS
to => PART => TO
translate => VERB => VB
a => DET => DT
few => ADJ => JJ
pages => NOUN => NNS
of => ADP => IN
English => PROPN => NNP
. => PUNCT => .
 ```

**Use cases of POS Tags**

Parts of speech tags have a large number of applications and they are used in a variety of tasks such as

- Text Cleaning
- Feature Engineering tasks
- Word sense disambiguation

For example, consider these sentences ![image](https://user-images.githubusercontent.com/22586467/123294728-be235600-d532-11eb-9559-e89624a13c57.png)

In both sentences, the keyword book is used, but in sentence one, it is used as a verb. While in sentence two it is used as a noun.

## Constituency Grammar Parsing

> Constituency Parsing is the process of analyzing the sentences by breaking it down into sub-phrases also known as constituents. These sub-phrases belong to a specific category of grammar like NP (noun phrase) and VP(verb phrase).

The goal of constituency grammar is to organize any sentence into its constituents using their properties. These properties are generally driven by their parts of speech tags, noun or verb phrase identification.

For example, constituency grammar can define that any sentence can be organized into three constituents a subject, a context, or an object. These constituents can take different values and accordingly can generate different sentences.

![image](https://user-images.githubusercontent.com/22586467/123295442-57eb0300-d533-11eb-9337-d00d47f38173.png)

Another way to look at constituency grammar is to define them in terms of their parts of speech tags say a grammar structure containing a <determiner, noun><adjective, verb> <preposition determiner noun>. This corresponds to the same sentence, The dogs are barking in the park.

![image](https://user-images.githubusercontent.com/22586467/123295592-794bef00-d533-11eb-8f50-e15fd6657782.png)


## Dependency Grammar Parsing

> Dependency parsing is the process of analyzing the grammatical structure of a sentence based on the dependencies between the words in a sentence.
  

Dependency grammar states that ” The words of a sentence depends on the other words of the sentence.”

In Dependency parsing, various tags represent the relationship between two words in a sentence. These tags are the dependency tags. For example, In the phrase ‘rainy weather,’ the word rainy modifies the meaning of the noun weather. Therefore, a dependency exists from the weather -> rainy in which the weather acts as the head and the rainy acts as dependent or child. This dependency is represented by amod tag, which stands for the adjectival modifier.

![image](https://user-images.githubusercontent.com/22586467/123297248-06dc0e80-d535-11eb-9877-f97aedc5772c.png)

Similar to this, there exist many dependencies among words in a sentence but note that a dependency involves only two words in which one acts as the head and other acts as the child. As of now, there are 37 universal dependency relations used in Universal Dependency (version 2). You can take a look at all of them [here](https://universaldependencies.org/u/dep/). Apart from these, there also exist many language-specific tags.

**Use cases Of Dependency Grammar**
Dependency grammar have multiple use cases, for instance

- In Named Entity Recognition
- Question- Answering system
- In co-reference resolutions, where the task is to map the pronouns with the respective noun phrases.
- In-text summarization problems.
- Features for Text Classification problems
  
 
