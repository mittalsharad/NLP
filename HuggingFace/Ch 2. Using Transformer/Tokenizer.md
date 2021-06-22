# Tokenizer

Tokenizers are one of the core components of the NLP pipeline. They serve one purpose: to translate text into data that can be processed by the model. Models can only process numbers, so tokenizers need to convert our text inputs to numerical data.The goal is to find the most meaningful representation — that is, the one that makes the most sense to the model — and, if possible, the smallest representation.

# Types of tokenization:

**1. Word-based**

```python
tokenized_text = "Jim Henson was a puppeteer".split()
print(tokenized_text)
```
Output:
```
['Jim', 'Henson', 'was', 'a', 'puppeteer']
```
**2. Character based**

Character-based tokenizers split the text into characters, rather than words. This has two primary benefits:

- The vocabulary is much smaller.
- There are much fewer out-of-vocabulary (unknown) tokens, since every word can be built from characters.

Lets do tokenization will become:

![image](https://user-images.githubusercontent.com/22586467/122931179-461a2c00-d38a-11eb-8d7c-7181d84c644d.png)


Here,we’ll end up with a very large amount of tokens to be processed by our model: whereas a word would only be a single token with a word-based tokenizer, it can easily turn into 10 or more tokens when converted into characters.



**3. Subword tokenization**

Subword tokenization algorithms rely on the principle that frequently used words should not be split into smaller subwords, but rare words should be decomposed into meaningful subwords.


Let’s do tokenization! will become

![image](https://user-images.githubusercontent.com/22586467/122931350-6e098f80-d38a-11eb-8de2-5a65e3e28da7.png)

These subwords end up providing a lot of semantic meaning: for instance, in the example above “tokenization” was split into “token” and “ization”, two tokens that have a semantic meaning while being space-efficient (only two tokens are needed to represent a long word).


# Loading and Saving Tokenizer

Loading and saving tokenizers is as simple as it is with models. Actually, it’s based on the same two methods: `from_pretrained` and `save_pretrained`. These methods will load or save the algorithm used by the tokenizer (a bit like the architecture of the model) as well as its vocabulary (a bit like the weights of the model).

```python
from transformers import BertTokenizer

tokenizer = BertTokenizer.from_pretrained("bert-base-cased")


# OR

from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained("bert-base-cased")
```

```python
tokenizer("Using a Transformer network is simple")
```
Output
```
{'input_ids': [101, 7993, 170, 11303, 1200, 2443, 1110, 3014, 102],
 'token_type_ids': [0, 0, 0, 0, 0, 0, 0, 0, 0],
 'attention_mask': [1, 1, 1, 1, 1, 1, 1, 1, 1]}
```
Saving a tokenizer:

```
tokenizer.save_pretrained("directory_on_my_computer")
```

# Encoding

Translating text to numbers is known as encoding. Encoding is done in a two-step process: the tokenization, followed by the conversion to input IDs.

The first step is to split the text into words (or parts of words, punctuation symbols, etc.), usually called tokens. The second step is to convert those tokens into numbers, so we can build a tensor out of them and feed them to the model. To do this, the tokenizer has a vocabulary, which is the part we download when we instantiate it with the from_pretrained method.

```python
#Tokenization
from transformers import AutoTokenizer
tokenizer = AutoTokenizer.from_pretrained("bert-base-cased")

sequence = "Using a Transformer network is simple"
tokens = tokenizer.tokenize(sequence)

print(tokens)
```
O/P
```
['Using', 'a', 'transform', '##er', 'network', 'is', 'simple']
```

The conversion to input IDs is handled by the `convert_tokens_to_ids` tokenizer method:
```
ids = tokenizer.convert_tokens_to_ids(tokens)

print(ids)
```
#O/P:
```
[7993, 170, 11303, 1200, 2443, 1110, 3014]
```

# Decoding

Decoding is going the other way around: from vocabulary indices, we want to get a string. This can be done with the decode method as follows:

```
decoded_string = tokenizer.decode([7993, 170, 11303, 1200, 2443, 1110, 3014])
print(decoded_string)
```
O/P
```
'Using a Transformer network is simple'
```
Note that the decode method not only converts the indices back to tokens, but also groups together the tokens that were part of the same words to produce a readable sentence. 


For detailed info, refer to [Huggingface Course](https://huggingface.co/course/chapter2/4?fw=pt)
