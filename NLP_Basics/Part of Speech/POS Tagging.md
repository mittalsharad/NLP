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
These tags are the result of the division of universal POS tags into various tags, like NNS for common plural nouns and NN for the singular common noun compared to NOUN for common nouns in English. These tags are language-specific. You can take a look at the complete list here.

For implementation, refer to [Notebook]()

