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

<img width="478" alt="image" src="https://github.com/wkdtjrrb/Paper_study/assets/103736979/3ae34bd1-ea2d-4576-875c-940503419d64">

- the computational complexity reduction
1. hierarchical version of softmax: frequency of words works for obtaning classes in NN
2. avoiding normalized representations of vocabulary
-> most of the computational complexity is caused by N * D * H
- limitation: need to specify the context length (N)


### 2. Recurrent Neural Net Language Model(RMNLM)
- It constist of input, hidden and output layer(**NO projection layer**)
- It can represent more complex patterns than the shallow neural networks
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

<img width="502" alt="image" src="https://github.com/wkdtjrrb/Paper_study/assets/103736979/53ca3b01-c49b-497b-a3e8-58fb4a45b7ae">

<img width="502" alt="image" src="https://github.com/wkdtjrrb/Paper_study/assets/103736979/ac2adb08-6c13-4209-a449-cb72ec409ac4">


HOW TO FIND 'Smallest' when 'Big-Biggest' relation and 'small' are presented??
- X = vector("biggest") - vector("big") + vector('small') (measured by cosine distance)
- cosine distance = 1 - cosine similarity(X dot Y / ||X|| dot ||Y||)

## Results

### Maximization of Accuracy

This paper used a Google News cropus for training the word vectors(6B tokens)

Table 1: Accuracy on subset of the Semantic-Syntactic Word Relationship test set, using word vectors from the CBOW architecture with limited vocabulary. Only questions containing words from the most frequent 30k words are used.

<img width="508" alt="image" src="https://github.com/wkdtjrrb/Paper_study/assets/103736979/4dd6e656-bb4d-4100-a3fd-ec28ad964f1e">

> Improving Dimensionality, the accuracy becomes better because high dimensionality means we can describe the details of the words
> Adding more training data provides diminishing improvements

Table 2: Comparison of architectures using models trained on the same data, with 640-dimensional word vectors. The accuracies are reported on our Semantic- Syntactic Word Relationship test set, and on the syntactic relationship test set

<img width="583" alt="image" src="https://github.com/wkdtjrrb/Paper_study/assets/103736979/1547e0b1-47f2-4906-bcd6-a0af70ba2a44">

> Semantic Accuracy: clothing is to shirt as dish is to bowl
> Syntactic Accuracy: A is to B, C is to ____?
>> Adjectives: base/comparative/superlative forms

>> Common nouns: singular/plural forms, possessive/non-possessive forms

>> Verbs: base, past and 3rd person present tense forms

### Comparison of Model Architectures

Table 3: Comparison of publicly available word vectors on the Semantic-Syntactic Word Relationship test set, and word vectors from our models. Full vocabularies are used

<img width="547" alt="image" src="https://github.com/wkdtjrrb/Paper_study/assets/103736979/2f82805f-a594-4f8f-bdc2-81e665c9b747">

> With lower dimensionality, using more training words can be used to improve accuracy

Table 4: Comparison of models trained for three epochs on the same data and models trained for one epoch. Accuracy is reported on the full Semantic-Syntactic data set

<img width="607" alt="image" src="https://github.com/wkdtjrrb/Paper_study/assets/103736979/0d706b07-9ceb-428c-ab12-79e0bf59050a">

> Skip-gram model has very high accuracy but it takes longer time 

Table 5: Comparison of models trained using the DistBelief distributed framework. Note that training of NNLM with 1000-dimensional vectors would take too long to complete

<img width="592" alt="image" src="https://github.com/wkdtjrrb/Paper_study/assets/103736979/4fdf09d6-73ea-4a01-912e-498ec7510543">

Table 6: Comparison and combination of models on the Microsoft Sentence Completion Challenge.

<img width="289" alt="image" src="https://github.com/wkdtjrrb/Paper_study/assets/103736979/88b34e0c-d7de-4ce7-8c5a-b7534cf5414f">

## Conclusion
- high quality of vector representations
- lower computational complexity -> we can use high dimension word vectors
  
