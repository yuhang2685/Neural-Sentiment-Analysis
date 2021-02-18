# Sentiment-Analysis

We demonstrate how to use **GloVe** word vector representations in Sentiment Analysis.

The dataset is Sentiment140, which is a collection of 1.6 million tweets that have been tagged as either positive or negative.

GloVe is available for download from Stanford. We use "100 dimension" version in "glove.6B.zip".

We constructed a simple LSTM Neural Network as below:

![Figure](model-summary.png)

Our simple 4 layer LSTM model achieves 70% accuracy.

![Figure](performance.png)

Comparison with "state-of-the-art" techniques:

1. Bayers: accuracy 70%~80%, fast.

2. SVM: accuracy 85% but longer to train.

We will continue to explore how to improve the accuracy,
such as data cleaning, stem, transfer learning the word embedding etc..


