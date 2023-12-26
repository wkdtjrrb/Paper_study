# Efficient Estimation of Word Representations in vector space(2013)

## Introduction
### Goals : techniques that can be used for learning high-quality word vectors from huge datasets
Expectation that not only will similar words tend to be close to each other, but that words can have **multiple degrees of similarity**
Representation of words as continuous vectors


#### Previous work
NNLM
- feedforward neural network with a linear projection layer and a non-linear hidden layer
- word vectors are first learned using nueural network with a single hidden layer
- word vectors then used to train the NNLM
- expect next word
- computationally expensive

## Model Architectures
- distriuted representations: distribute the meaning of the word in various dimensions

### 1. FEEDFORWARD NEURAL NET LANGUAGE MODEL(NNLM)
- It consists of input, projection, hidden, and output layer
- input layer: N previous words are encoded using 1-of-V coding(V = size of the voca)
- projection layer: input layer is then projected to a projection layer (N * D)
- hidden layer: used to compute probability distribution over all the words in vocabulary
- output layer: dimensionality V
  
- 1-of-V coding: one hot encoding
- N: the total number of words
- D: dimension of word embeddings: specific meaning per each dimension, similar meanings are - 
  mapped nearby
- H: hidden layer size
-> Q = (N * D) + (N * D * H) + (H * V) (dominating term: H * V)

- the computational complexity reduction
- 1. hierarchical version of softmax: frequency of words works for obtaning classes in NN
  2. avoiding normalized representations of vocabulary
-> most of the computational complexity is caused by N * D * H
- limitation: need to specify the context length
- 
### 2. Recurrent Neural Net Language Model(RMNLM)
- 
