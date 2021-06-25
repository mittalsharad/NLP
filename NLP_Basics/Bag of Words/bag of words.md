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

# What are N-Grams?

Again same questions, what are n-grams and why do we use them? Let us understand this with an example below-

Sentence 1: “This is a good job. I will not miss it for anything”

Sentence 2: ”This is not good at all”

For this example, let us take the vocabulary of 5 words only. The five words being-

good
job
miss
not
all

So, the respective vectors for these sentences are:

“This is a good job. I will not miss it for anything”=[1,1,1,1,0]

”This is not good at all”=[1,0,0,1,1]

Can you guess what is the problem here? Sentence 2 is a negative sentence and sentence 1 is a positive sentence. Does this reflect in any way in the vectors above? Not at all. So how can we solve this problem? Here come the N-grams to our rescue.

An N-gram is an N-token sequence of words: a 2-gram (more commonly called a bigram) is a two-word sequence of words like “really good”, “not good”, or “your homework”, and a 3-gram (more commonly called a trigram) is a three-word sequence of words like “not at all”, or “turn off light”.

For example, the bigrams in the first line of text in the previous section: “This is not good at all” are as follows:

“This is”
“is not”
“not good”
“good at”
“at all”

Now if instead of using just words in the above example, we use bigrams (Bag-of-bigrams) as shown above. The model can differentiate between sentence 1 and sentence 2. So, using bi-grams makes tokens more understandable (for example, “HSR Layout”, in Bengaluru, is more informative than “HSR” and “layout”)

So we can conclude that a bag-of-bigrams representation is much more powerful than bag-of-words, and in many cases proves very hard to beat.

