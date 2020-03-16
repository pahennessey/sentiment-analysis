# Sentiment Analysis using AWS Sagemaker, Lambda, and API Gateway functionality

## Introduction

This project highlights the use of cloud-based training and serving for a PyTorch-based Recurrent Neural Network (RNN) for sentiment analysis. The model was trained using the Stanford [IMDb dataset](http://ai.stanford.edu/~amaas/data/sentiment/)

> Maas, Andrew L., et al. [Learning Word Vectors for Sentiment Analysis](http://ai.stanford.edu/~amaas/data/sentiment/). In _Proceedings of the 49th Annual Meeting of the Association for Computational Linguistics: Human Language Technologies_. Association for Computational Linguistics, 2011.

to infer whether or not a review is positive or negative based on only the words of the review, not a direct thumbs-up/thumbs-down system.

## Pipeline

For both training the model, and serving the model, the reviews must first be processed from sentences into feature vectors.

### Convert reviews to words

To start, first the text input is stripped of all HTML tags and non-alphanumeric characters, convert all characters to lowercase, and split into a list of individual words. Stop words are also removed from this list to remove unwanted noise from the reviews, and the remaining words in the list are stemmed using the PorterStemmer method from the nltk library.

### Build vocabulary dictionary

To convert word into integers required for the RNN, a dictionary is created based on the 4998 mot commonly occuring words across all reviews. These are order based on frequency, and indexed in that order. That is, words that appear most often (i.e. "movie") will have an index near 0 and words that appear least often, but still in the most common 5000 words (i.e. "kwigybo") will be near 5000. Indexes 0 and 1 will be reserved for "no word," in the case that a review is too short (more on that in the next section) and "uncommon word" for any words in the review that do not fall in the top 4998 most used words.

Machine learning algorithms tend to give more weight to numbers with higher magnitude, keeping the most commonly used words at the bottom of the scale allows the parts of a review that are most similar to not drive the output of the classifier.

### Transform to feature vector

To create a degree of uniformity between reviews, each review will be fixed at a 500-word length, and reviews that are shorter than 500 words will be padded with blanks (index 0 as described above). In addition, since the length of the review before this step could be of interest to the classifier as it trains, so we'll append the real lenght of the list of words prior to this step at the beginning of this vector, to give us a final array lenght of 501, composed of the elements `length_of_review, review[500]`

## PyTorch Model

TODO: write information about the PyTorch model implemented.

## AWS SageMaker Training and Deploy

placeholder

## AWS Lambda

placeholder

## API Gateway

placeholder
