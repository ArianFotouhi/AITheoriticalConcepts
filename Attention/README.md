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
