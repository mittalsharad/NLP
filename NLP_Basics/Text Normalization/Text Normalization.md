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
