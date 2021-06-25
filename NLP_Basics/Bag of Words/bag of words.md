# Bag of Words (BOW)

The Bag of Words (BoW) model is the simplest form of text representation in numbers. Like the term itself, we can represent a sentence as a bag of words vector (a string of numbers). It is called a 'Bag' because the order of the words is unknows in this representation. We are only concerned whether the word is present in the document or not.

Let's take an example of movie reviews to understand this better. 
- Review 1: This movie is very scary and long
- Review 2: This movie is not scary and is slow
- Review 3: This movie is spooky and good

We will first build a vocabulary from all the unique words in the above three reviews. The vocabulary consists of these 11 words: ‘This’, ‘movie’, ‘is’, ‘very’, ‘scary’, ‘and’, ‘long’, ‘not’,  ‘slow’, ‘spooky’,  ‘good’.

We can now take each of these words and mark their occurrence in the three movie reviews above with 1s and 0s. This will give us 3 vectors for 3 reviews:

![image](https://user-images.githubusercontent.com/22586467/123374604-fcf1f400-d5a4-11eb-949f-8761308139ec.png)

Vector of Review 1: [1 1 1 1 1 1 1 0 0 0 0]

Vector of Review 2: [1 1 2 0 0 1 1 0 1 0 0]

Vector of Review 3: [1 1 1 0 0 0 1 0 0 1 1]

And that’s the core idea behind a Bag of Words (BoW) model.

Drawbacks of using a Bag-of-Words (BoW) Model
In the above example, we can have vectors of length 11. However, we start facing issues when we come across new sentences:

If the new sentences contain new words, then our vocabulary size would increase and thereby, the length of the vectors would increase too.
Additionally, the vectors would also contain many 0s, thereby resulting in a sparse matrix (which is what we would like to avoid)
We are retaining no information on the grammar of the sentences nor on the ordering of the words in the text.

For implementation, Refer to Notebook
