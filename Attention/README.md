# Self-Attention and Transformers (with numeric example)
In spite of many useful resources for illustrating attention concept, this article tries to recap the concept and more importantly, it shows a simplified numberic example to clarify the process of text generation and translation machine. 

# Preliminary
As shown in [Attention Is All You Need](https://arxiv.org/abs/1706.03762), we need to consider three tools namely Scaled Dot-Product Attention, Multi-Head Attention and Self-Attention.
## Scaled Dot-Product Attention
It involves calculating attention scores between pairs of elements in the input sequences (usually queries, keys, and values) using dot products, scaling the scores, applying a softmax function to obtain weights, and then computing a weighted sum of the values.
## Multi-Head Attention 
This mechanism extends the basic attention by performing multiple attention calculations in parallel. It allows the model to focus on different parts of the input and learn diverse representations. Each "head" has its own set of query, key, and value projections.
## Self-Attention
Self-attention allows each word/token in a sequence to consider dependencies between all other words/tokens in the sequence. It helps capture long-range dependencies efficiently.

# A Frequent Question! What's difference of Attention and Self-Attention?
In traditional attention mechanisms, such as those used in sequence-to-sequence models like the encoder-decoder architecture in machine translation, attention helps the model focus on specific parts of the input sequence while generating the output sequence. However, self-attention, introduced in models like the Transformer, allows each element in a sequence to attend to all other elements in the same sequence. This means that every word in an input sentence, for example, can be connected to and influence the representation of every other word in the sentence.

# Self Attention Numeric Example
In Self-Attnetion process uses below formula where Q is the query of focused word, K^T is matrix of other words (rest of input tokens) keys, d_k is dimension of the key matrix (to avoid huge numbers) and V represents the vector of all values.

Attention(Q, K) = softmax( QK^T / sqrt(d_k) ) * V

# Steps
## Input Encoding
Sentence: "The sitting dog."
This sentence gets broken into tokens (words or subwords) and then embedded into vectors. Each token (word) has three vector 

representations: Query, Key, and Value.

For instance:
"The": Query = [0.2, 0.5, 0.1], Key = [0.1, 0.3, 0.6], Value = [0.3, 0.2, 0.8]

"dog": Query = [0.4, 0.6, 0.2], Key = [0.2, 0.4, 0.7], Value = [0.5, 0.3, 0.9]

"sitting": Query = [0.3, 0.4, 0.1], Key = [0.4, 0.3, 0.5], Value = [0.6, 0.4, 0.9]



## Similarity Calculation

To determine which words are important for each word in the sentence, the model computes the similarity (often using dot product) between the query of the word it's focusing on and the keys of all other words in the sentence.

for example, dot product between the Query vector of "sitting" and the Key vectors of "The" and "dog."

Dot Product (sitting, The)=0.3×0.1+0.4×0.3+0.1×0.6=0.13

Dot Product (sitting, dog)=0.3×0.2+0.4×0.4+0.1×0.7=0.26
 
(assuming d_k​ =3) and apply the softmax function to obtain attention weights for each word.

Softmax (sitting, The)=softmax(0.13/3)

Softmax (sitting, dog)=softmax(0.26/3)

## Weighted Sum

Weighted Sum (sitting, The)=Softmax (sitting, The)×Value (The)

Weighted Sum (sitting, dog)=Softmax (sitting, dog)×Value (dog)


Weighted Sum (sitting, The)≈0.4×[0.3,0.2,0.8] = [0.12, 0.08, 0.32]

Weighted Sum (sitting, dog)≈0.6×[0.5,0.3,0.9] = [0.3, 0.18, 0.54]


Weighted sum = [0.12 + 0.3, 0.08 + 0.18, 0.32 + 0.54] = [0.42, 0.26, 0.86]

This resulting vector [0.42, 0.26, 0.86] represents the context or information that the model considers most relevant for the word "sitting" based on the attention mechanism (how much the word is related to other words of sentence)

## Word Generation




