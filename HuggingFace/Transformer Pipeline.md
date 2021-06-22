# Transformer Pipeline


Let's see what happens on the inside after we transport a pipeline,(as described in the previous article). We will take example of a **Sentiment Analysis** pipeline.

```python
from transformers import pipeline

classifier = pipeline("sentiment-analysis")
classifier([
    "I've been waiting for a HuggingFace course my whole life.", 
    "I hate this so much!",
])
```

Output:

```python
[{'label': 'POSITIVE', 'score': 0.9598047137260437},
 {'label': 'NEGATIVE', 'score': 0.9994558095932007}]
 ```
 
 As we saw in previous article, this pipeline groups together three steps: 
 - preprocessing
 - passing the inputs through the model
 - postprocessing

![image](https://user-images.githubusercontent.com/22586467/122866518-b5216180-d345-11eb-84ef-3219aa05aeed.png)

Let's go through them one by one.

## Preprocessing with a tokenizer

While using a pipeline, all this preprocessing needs to be done in exactly the same way as when the model was pretrained for. 

The preprocessing step does the following:
- Splitting the input into words, subwords, or symbols (like punctuation) that are called tokens
- Mapping each token to an integer
- Adding additional inputs that may be useful to the model

To download the model, we use the `AutoTokenizer` class and its `from_pretrained` method. Using the checkpoint name of our model, it will automatically fetch the data associated with the model’s tokenizer and cache it (so it’s only downloaded the first time you run the code below).

Since the default checkpoint of the sentiment-analysis pipeline is distilbert-base-uncased-finetuned-sst-2-english (you can see its model card [here](https://huggingface.co/distilbert-base-uncased-finetuned-sst-2-english)), we run the following:

```python
from transformers import AutoTokenizer

checkpoint = "distilbert-base-uncased-finetuned-sst-2-english"
tokenizer = AutoTokenizer.from_pretrained(checkpoint)
```

Once we have the tokenizer, we can directly pass our sentences to it and we’ll get back a dictionary that’s ready to feed to our model! The only thing left to do is to convert the list of input IDs to tensors.

```python
raw_inputs = [
    "I've been waiting for a HuggingFace course my whole life.", 
    "I hate this so much!",
]
inputs = tokenizer(raw_inputs, padding=True, truncation=True, return_tensors="pt")
print(inputs)
```

here:
Padding: all the sentences needs to be of same size before passing them to the model. So we use Padding
Truncation: If the size of input text exceds the max size allowed by model, truncate it.
return_tensor: the type of tensor our tokenizer should return. can be PyTorch, TensorFlow, or plain NumPy

Output
```python
{
    'input_ids': tensor([
        [  101,  1045,  1005,  2310,  2042,  3403,  2005,  1037, 17662, 12172, 2607,  2026,  2878,  2166,  1012,   102],
        [  101,  1045,  5223,  2023,  2061,  2172,   999,   102,     0,     0,     0,     0,     0,     0,     0,     0]
    ]), 
    'attention_mask': tensor([
        [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1],
        [1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0]
    ])
}
```

## Going through the model

We can download our pretrained model the same way we did with our tokenizer. 🤗 Transformers provides an `AutoModel` class which also has a `from_pretrained` method:

```python
from transformers import AutoModel

checkpoint = "distilbert-base-uncased-finetuned-sst-2-english"
model = AutoModel.from_pretrained(checkpoint)
```

This architecture contains only the base Transformer module: given some inputs, it outputs what we’ll call hidden states, also known as features. For each model input, we’ll retrieve a high-dimensional vector representing the contextual understanding of that input by the Transformer model.

While these hidden states can be useful on their own, they’re usually inputs to another part of the model, known as the head.

**A high-dimensional vector?**

The vector output by the Transformer module is usually large. It generally has three dimensions:
- **Batch size:** The number of sequences processed at a time (2 in our example).
- **Sequence length:** The length of the numerical representation of the sequence (16 in our example).
- **Hidden size:** The vector dimension of each model input.

It is said to be “high dimensional” because of the last value. The hidden size can be very large (768 is common for smaller models, and in larger models this can reach 3072 or more).

We can see this if we feed the inputs we preprocessed to our model:

```python
outputs = model(**inputs)
print(outputs.last_hidden_state.shape)
```
Output

```python
torch.Size([2, 16, 768])
```

Note that the outputs of 🤗 Transformers models behave like namedtuples or dictionaries. You can access the elements by attributes (like we did) or by key (outputs["last_hidden_state"]), or even by index if you know exactly where the thing you are looking for is (outputs[0]).

## Model heads: Making sense out of numbers

The model heads take the high-dimensional vector of hidden states as input and project them onto a different dimension. They are usually composed of one or a few linear layers:

![image](https://user-images.githubusercontent.com/22586467/122883498-e48e9900-d35a-11eb-91be-914b503853d0.png)

The output of the Transformer model is sent directly to the model head to be processed.

In this diagram, the model is represented by its embeddings layer and the subsequent layers. The embeddings layer converts each input ID in the tokenized input into a vector that represents the associated token. The subsequent layers manipulate those vectors using the attention mechanism to produce the final representation of the sentences.

There are many different architectures available in 🤗 Transformers, with each one designed around tackling a specific task. Here is a non-exhaustive list:

- *Model (retrieve the hidden states)
- *ForCausalLM
- *ForMaskedLM
- *ForMultipleChoice
- *ForQuestionAnswering
- *ForSequenceClassification
- *ForTokenClassification
and others 🤗

For our example, we will need a model with a sequence classification head (to be able to classify the sentences as positive or negative). So, we won’t actually use the AutoModel class, but `AutoModelForSequenceClassification`:

```python
from transformers import AutoModelForSequenceClassification

checkpoint = "distilbert-base-uncased-finetuned-sst-2-english"
model = AutoModelForSequenceClassification.from_pretrained(checkpoint)
outputs = model(**inputs)
```

Now if we look at the shape of our inputs, the dimensionality will be much lower: the model head takes as input the high-dimensional vectors we saw before, and outputs vectors containing two values (one per label):

```python
print(outputs.logits.shape)
```
Output
```
torch.Size([2, 2])
```

## Postprocessing the output

The values we get as output from our model don’t necessarily make sense by themselves.

```python
print(outputs.logits)

#Output
tensor([[-1.5607,  1.6123],
        [ 4.1692, -3.3464]], grad_fn=<AddmmBackward>)
```

Our model predicted [-1.5607, 1.6123] for the first sentence and [ 4.1692, -3.3464] for the second one. Those are not probabilities but logits, the raw, unnormalized scores outputted by the last layer of the model. To be converted to probabilities, they need to go through a [SoftMax](https://en.wikipedia.org/wiki/Softmax_function) layer (all 🤗 Transformers models output the logits, as the loss function for training will generally fuse the last activation function, such as SoftMax, with the actual loss function, such as cross entropy):

```python
import torch

predictions = torch.nn.functional.softmax(outputs.logits, dim=-1)
print(predictions)
```
Output
```python
tensor([[4.0195e-02, 9.5980e-01],
        [9.9946e-01, 5.4418e-04]], grad_fn=<SoftmaxBackward>)
```
Now we can see that the model predicted [0.0402, 0.9598] for the first sentence and [0.9946, 0.0544] for the second one. These are recognizable probability scores.To get the labels corresponding to each position, we can inspect the id2label attribute of the model config:

```python
model.config.id2label
```
Output
```python
{0: 'NEGATIVE', 1: 'POSITIVE'}
```

Now we can conclude that the model predicted the following:

- First sentence: NEGATIVE: 0.0402, POSITIVE: 0.9598
- Second sentence: NEGATIVE: 0.9946, POSITIVE: 0.0544

We have successfully reproduced the three steps of the pipeline: preprocessing with tokenizers, passing the inputs through the model, and postprocessing!
