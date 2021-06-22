# About

In this chapter, we will learn:

1. How to use the pipeline function to solve NLP tasks such as text generation and classification
2. About the Transformer architecture
3. How to distinguish between encoder, decoder, and encoder-decoder architectures and use cases


# Natural Language Processing
Before jumping into Transformer models, let’s do a quick overview of what natural language processing is and why we care about it.

## What is NLP?

NLP is a field of linguistics and machine learning focused on understanding everything related to human language. The aim of NLP tasks is not only to understand single words individually, but to be able to understand the context of those words.

The following is a list of common NLP tasks, with some examples of each:
- **Classifying whole sentences:** Getting the sentiment of a review, detecting if an email is spam, determining if a sentence is grammatically correct or whether two sentences are logically related or not
- **Classifying each word in a sentence:** Identifying the grammatical components of a sentence (noun, verb, adjective), or the named entities (person, location, organization)
- **Generating text content:** Completing a prompt with auto-generated text, filling in the blanks in a text with masked words
- **Extracting an answer from a text:** Given a question and a context, extracting the answer to the question based on the information provided in the context
- **Generating a new sentence from an input text:** Translating a text into another language, summarizing a text

NLP isn’t limited to written text though. It also tackles complex challenges in speech recognition and computer vision, such as generating a transcript of an audio sample or a description of an image.

## Why is it challenging?
Computers don’t process information in the same way as humans. For example, when we read the sentence “I am hungry,” we can easily understand its meaning. Similarly, given two sentences such as “I am hungry” and “I am sad,” we’re able to easily determine how similar they are. For machine learning (ML) models, such tasks are more difficult. The text needs to be processed in a way that enables the model to learn from it. And because language is complex, we need to think carefully about how this processing must be done. There has been a lot of research done on how to represent text, and we will look at some methods in the next chapter.

# Transformers, what can they do?
Transformer models are used to solve all kinds of NLP tasks, like the ones mentioned in the previous section. Here are some of the companies and organizations using Hugging Face and Transformer models, who also contribute back to the community by sharing their models:

![image](https://user-images.githubusercontent.com/22586467/122793679-1bbc6600-d2d9-11eb-8359-c895c316522b.png)

The [🤗 Transformers library](https://github.com/huggingface/transformers) provides the functionality to create and use those shared models. The [Model Hub](https://huggingface.co/models) contains thousands of pretrained models that anyone can download and use. You can also upload your own models to the Hub!

Before diving into how Transformer models work under the hood, let’s look at a few examples of how they can be used to solve some interesting NLP problems.

## Working with pipelines

The most basic object in the 🤗 Transformers library is the pipeline. It connects a model with its necessary preprocessing and postprocessing steps, allowing us to directly input any text and get an intelligible answer:

By default, the pipeline selects a particular pretrained model that has been fine-tuned for the defined task. The model is downloaded and cached when you create the classifier object. If you rerun the command, the cached model will be used instead and there is no need to download the model again.

There are three main steps involved when you pass some text to a pipeline:

1. The text is preprocessed into a format the model can understand.
2. The preprocessed inputs are passed to the model.
3. The predictions of the model are post-processed, so you can make sense of them.

Some of the currently [available pipelines](https://huggingface.co/transformers/main_classes/pipelines.html) are:

- feature-extraction (get the vector representation of a text)
- fill-mask
- ner (named entity recognition)
- question-answering
- sentiment-analysis
- summarization
- text-generation
- translation
- zero-shot-classification

For detailed info on how to use these pipelines, refer to the [Notebook](https://github.com/mittalsharad/NLP/blob/main/HuggingFace/Ch%201.%20Transformer%20Models/Transformer.ipynb)

# [How do Transformers Work](https://huggingface.co/course/chapter1/4?fw=pt)

