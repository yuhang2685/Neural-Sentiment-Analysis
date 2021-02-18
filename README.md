# Sentiment-Analysis

[![license](https://img.shields.io/github/license/mashape/apistatus.svg)](LICENSE)

## Introduction

We experiment how to use Neural Network and [GloVe](https://www.aclweb.org/anthology/D14-1162/) word vector representations for Sentiment Analysis.

The dataset is [Sentiment140](http://www.sentiment140.com/), 
which is a collection of 1.6 million tweets that have been tagged as either positive or negative.

GloVe is available for [download](https://nlp.stanford.edu/projects/glove/) from Stanford. 
We use the "100 dimension" version in "glove.6B.zip".

## Neural Network

We constructed a simple LSTM Neural Network as below:

<img src="model-summary.png" width="50%">

## Performance

Our simple 4 layer LSTM model achieves 70% accuracy.

![Figure](performance.png)

## Other Popular Techniques

1. SVM: 
   - accuracy - 85%    
   - training - very long

2. Maximum Entropy
   - accuracy - 83%    
   - training - very long

3. [Lexicon & Rule-based](https://github.com/cjhutto/vaderSentiment)
   - accuracy - 80%    
   - labor consuming
   
4. [Naive Bayes](https://github.com/vivekn/sentiment): 
   - accuracy - 70% ~ 80%   
   - fast execution

## Future Work

We will continue to explore how to improve the accuracy,
which includes applying various pre-processing steps like URLs, handles, Hashtags, punctuations, emoticons, twitter specific terms and stemming,
investigating the following features - unigrams, bigrams, trigrams and negation detection, see https://github.com/ayushoriginal/Sentiment-Analysis-Twitter.

We will also experiment with transfer learning sophisticated Neural Networks, such as Attension Model.


