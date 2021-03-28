# Neural-Sentiment-Analysis

[![license](https://img.shields.io/github/license/mashape/apistatus.svg)](LICENSE)

## Introduction

We explore how to use Neural Network and [GloVe](https://www.aclweb.org/anthology/D14-1162/) Word Vector Representations for Sentiment Analysis. 
The main advantage of Neural Network approach is the speed.

The dataset is [Sentiment140](http://www.sentiment140.com/), 
which is a collection of 1.6 million tweets that have been tagged as either positive or negative.

GloVe is available for [download](https://nlp.stanford.edu/projects/glove/) from Stanford. 
We use the "100 dimension" version in "glove.6B.zip".

## Benchmark
As suggested in , it is not easy to offer benchmarks and general metrics for sentiment accuracy,
which depends on so many factors: 
the type of data you’re dealing with, 
the people who hand-tagged your sentiment library, 
how much sleep they each got the night before, 
the complexity of the language that your industry uses (financial and medical data is particularly arcane)… the list goes on.

Research shows that human analysts tend to agree around 80-85% of the time. 
This is the baseline we (usually) try to meet or beat when we’re training a sentiment scoring system.

Our simplest sentiment classification model, 
trained on very general sentiment libraries, 
performed admirably, reaching 70.5% accuracy. 
With a domain-specific dictionary, 
I’m sure we could reach 80% accuracy or more.

Of course, the best results will always come from analyzing domain-specific content with a sentiment scoring model trained on similar content.

For example, if you analyze a data set of financial content using a model trained on movie reviews, the results won’t be nearly so good. But try analyzing the same data set using a system that’s configured to understand financial language. You’ll find that you can achieve very high sentiment accuracy without much extra effort.

The article [6 Practices to enhance the performance of a Text Classification Model](https://www.analyticsvidhya.com/blog/2015/10/6-practices-enhance-performance-text-classification-model/) suggested the following:
1. Domain Specific Features in the Corpus
2. Use An Exhaustive Stopword List
3. Noise Free Corpus
4. Eliminating features with extremely low frequency
5. Normalized Corpus
6. Use Complex Features: n-grams and part of speech tags

## Neural Network

We constructed a simple LSTM Neural Network as below:
```
Model: "sequential_4"
_________________________________________________________________
Layer (type)                 Output Shape              Param #   
=================================================================
embedding_4 (Embedding)      (None, 16, 100)           7648500   
_________________________________________________________________
bidirectional_7 (Bidirection (None, 16, 256)           234496    
_________________________________________________________________
dropout_2 (Dropout)          (None, 16, 256)           0         
_________________________________________________________________
bidirectional_8 (Bidirection (None, 256)               394240    
_________________________________________________________________
dropout_3 (Dropout)          (None, 256)               0         
_________________________________________________________________
dense_7 (Dense)              (None, 1)                 257       
=================================================================
Total params: 8,277,493
Trainable params: 8,277,493
Non-trainable params: 0
```
## Performance

Our simple LSTM model quickly achieves 99% training accuracy, with 70% validation accuracy.
We see the accuracy is not acceptable, and would try to improve it.

![Figure](performance.png)

## Other Popular Techniques

1. SVM: 
   - accuracy - 85%    
   - training - very long
   - no probability estimation

2. Maximum Entropy
   - accuracy - 83%    
   - training - very long

3. [Lexicon & Rule-based](https://github.com/cjhutto/vaderSentiment)
   - accuracy - 80%    
   - labor consuming
   
4. [Naive Bayes](https://github.com/vivekn/sentiment): 
   - accuracy - 70% ~ 80%   
   - fast execution

5. Our simple LSTM:
   - accuracy - 70%    
   - training - fast
   
## Future Work

We will continue to explore how to improve the accuracy,
which includes applying various pre-processing steps like URLs, handles, Hashtags, punctuations, emoticons, twitter specific terms and stemming,
investigating the following features - unigrams, bigrams, trigrams and negation detection, see https://github.com/ayushoriginal/Sentiment-Analysis-Twitter.

We will also experiment with transfer learning sophisticated Neural Networks, such as Attension Model.

## Reference

- [GloVe: Global Vectors for Word Representation](https://www.aclweb.org/anthology/D14-1162/)
- [VADER: A Parsimonious Rule-based Model for Sentiment Analysis of Social Media Text](https://www.researchgate.net/publication/275828927_VADER_A_Parsimonious_Rule-based_Model_for_Sentiment_Analysis_of_Social_Media_Text)
- [Fast and accurate sentiment classification using an enhanced Naive Bayes model](https://arxiv.org/abs/1305.6143)
- [Sentiment Accuracy: Explaining the Baseline and How to Test It](https://www.lexalytics.com/lexablog/sentiment-accuracy-baseline-testing)
- [6 Practices to enhance the performance of a Text Classification Model](https://www.analyticsvidhya.com/blog/2015/10/6-practices-enhance-performance-text-classification-model/)
