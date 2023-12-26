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
- we can designate the dimension of words
ㄴ try to minimize coputational complexity

### 1. FEEDFORWARD NEURAL NET LANGUAGE MODEL(NNLM)
- It consists of input, projection, hidden, and output layer
- input layer: N previous words are encoded using 1-of-V coding(V = size of the voca)
- projection layer: input layer is then projected to a projection layer (N * D)
- hidden layer: used to compute probability distribution over all the words in vocabulary
- output layer: dimensionality of V
  
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
- limitation: need to specify the context length (N)

### 2. Recurrent Neural Net Language Model(RMNLM)
- It constist of input, hidden and output layer(**NO projection layer**)
- It can represent more complex patterns thatn the shallow neural networks
- hidden layer and output layer connections using time-delay: short term memory
-> Q = (H * H) + (H * V) (D = H)
  with hierarchical softmax, most of the complexity comes from H * H


## NEW Log-linear Models

### 1. Continuous Bag-of-Words Model (CBOW)
- non-linear hidden layer is removed and the projection layer is shared for all words
- thus, all words get projected into the same position(vectors are  averaged)
- the order of words in the history does not influence the projection
- use words from the future(correctly classify the current(middle) word)
- predict the current word based on the context
  
### 2. Continuous Skip-gram Model
- tries to maximize classification of a word based on another word in the same sentence
- current word as an input to classifier, certain range before and after the current word as an 
  output
- increasing range improves quality of the resulting word vectors, computational complexity
-> Q = (C * D + D * log2(V))



HOW TO FIND 'Smallest' when 'Big-Biggest'relation and 'small' are presented??
- X = vector("biggest") - vector("big") + vector('small') (measured by cosine distance)
- cosine distance = 1 - cosine similarity(X dot Y / ||X|| dot ||Y||)


  
