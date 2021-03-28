# Neural-Sentiment-Analysis

[![license](https://img.shields.io/github/license/mashape/apistatus.svg)](LICENSE)

## Overview
We explore the Neural Network approach for Sentiment Analysis. 
The main advantage of the Neural Network approach is the fast speed.


## Data
The dataset is [Sentiment140](http://www.sentiment140.com/), 
which is a collection of 1.6 million tweets that have been tagged as either positive or negative.

[GloVe](https://nlp.stanford.edu/projects/glove/) is one the most popular Word Vector Representations. 
We use the version of "100 dimension" in "glove.6B.zip" which is available on Stanford website. 


## Benchmark
As suggested in [Sentiment Accuracy: Explaining the Baseline and How to Test It](https://www.lexalytics.com/lexablog/sentiment-accuracy-baseline-testing), 
it is not easy to offer benchmarks and general metrics for sentiment accuracy,
which depends on so many factors: 
the type of data you’re dealing with, 
the people who hand-tagged your sentiment library, 
how much sleep they each got the night before, 
the complexity of the language that your industry uses (financial and medical data is particularly arcane)… the list goes on.

Research shows that human analysts tend to agree around 80-85% of the time. 
This is the baseline we (usually) try to meet or beat when we’re training a sentiment scoring system.


## Model

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

Our simplest sentiment classification model, 
trained on very general sentiment libraries, 
performed admirably, reaching 70.5% accuracy. 
With a domain-specific dictionary, 
We are sure we could reach 80% accuracy or more.

![Figure](performance.png)

Of course, the best results will always come from analyzing domain-specific content with a sentiment scoring model trained on similar content.

For example, if you analyze a data set of financial content using a model trained on movie reviews, 
the results won’t be nearly so good. 
But try analyzing the same data set using a system that’s configured to understand financial language. 
You’ll find that you can achieve very high sentiment accuracy without much extra effort.


## Improvements

Our simple LSTM model quickly achieves 99% training accuracy, with 70% validation accuracy.
We will investigate the cause for overfitting and address this problem.

To improve the accuracy, 
[ayushoriginal](https://github.com/ayushoriginal/Sentiment-Analysis-Twitter) suggested applying various pre-processing steps like URLs, handles, Hashtags, punctuations, emoticons, twitter specific terms and stemming,
investigating the following features - unigrams, bigrams, trigrams and negation detection.

Similarly, the article [6 Practices to enhance the performance of a Text Classification Model](https://www.analyticsvidhya.com/blog/2015/10/6-practices-enhance-performance-text-classification-model/) suggested the following strateges:

1. Domain Specific Features in the Corpus
   
   The vocabulary of a corpus varies with domains. 
   Social Media contains a lot of slangs and improper keywords like “awsum, lol, gooood” etc 
   which are absent in any of the formal corpus such as news, blogs etc.
   
2. Use An Exhaustive Stopword List

   Stopwords are defined as the most commonly used words in a corpus. 
   Most commonly used stopwords are “a, the, of, on, … etc”. 
   These words are used to define the structure of a sentence. 
   But, are of no use in defining the context. 
   Treating these type of words as feature words would result in poor performance in text classification. 
   These words can be directly ignored from the corpus in order to obtain a better performance. 
   Apart from language stopwords, There are some other supporting words as well which are of lesser importance than any other terms.
   
3. Noise Free Corpus

   Noisy corpus refers to unimportant entities of the text such as punctuations marks, numerical values, links and urls etc. 
   Removal of these entities from the text would increase the accuracy, because size of sample space of possible features set decreases.

   Yet, it becomes essential to note that, 
   these entities should only be removed if the classification problem does not use these entities. 
   For example – emoticons such as  :), :P, 🙁  are important for sentiment classification but may not be important for other text classifications.

4. Eliminating features with extremely low frequency

   Keywords which occur in lesser frequency in the corpus usually does not play a role in text classification. 
   One can get rid of these low occurring features, resulting in better performance of the model. 
   
   Hence, if we choose a threshold,  all keywords with less frequency can be ignored, resulting in good accuracy.

5. Normalized Corpus (stemming)

   Words are the integral part of any classification technique. 
   However, these words are often used with different variations in the text depending on their grammar (verb, adjective, noun, etc.). 
   It is always a good practice to normalize the terms to their root forms. 
   This technique is known as "Lemmatization".
   
6. Use Complex Features: n-grams and part of speech tags

   In some cases, features as the combination of words provides better significance rather than considering single words as features. 
   Combination of N words together are called N-grams. 
   It is known that Bigrams are the most informative N-Gram combinations. 
   Adding bigrams to feature set will improve the accuracy of text classification model.

   Similarly, considering Part of Speech tags combined with words / n-grams will give an extra set of feature space.  
   

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

   
## Future Work

We will also experiment with transfer learning sophisticated Neural Networks, such as Attension Model.


## Reference

- [GloVe: Global Vectors for Word Representation](https://www.aclweb.org/anthology/D14-1162/)
- [VADER: A Parsimonious Rule-based Model for Sentiment Analysis of Social Media Text](https://www.researchgate.net/publication/275828927_VADER_A_Parsimonious_Rule-based_Model_for_Sentiment_Analysis_of_Social_Media_Text)
- [Fast and accurate sentiment classification using an enhanced Naive Bayes model](https://arxiv.org/abs/1305.6143)
- [Sentiment Accuracy: Explaining the Baseline and How to Test It](https://www.lexalytics.com/lexablog/sentiment-accuracy-baseline-testing)
- [6 Practices to enhance the performance of a Text Classification Model](https://www.analyticsvidhya.com/blog/2015/10/6-practices-enhance-performance-text-classification-model/)
