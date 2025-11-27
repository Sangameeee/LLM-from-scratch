# Large Language Model from scratch
## Table of Contents 
- [Introduction](#1-introduction) 
-  [Tokenization and data embedding](#2-Tokenization-and-Data-embedding) 
- [Attention mechanism](#3-Attention-Mechanism) 
- [Results till now](#4-RESULTS-till-now) 

## 1. Introduction:
In this project, I try to create a LLM architecture from start using PyTorch. This project aims to enrich the knowledge about transformers how they work and every steps taken is throughly implemented. For this project Decoder-architecture GPT2 is rebuilt as training takes a huge resources so weight can be imported while also trying to train on small custom dataset.

## 2. Tokenization and Data embedding:
Word embeddings is necessary as LLMs cannot process raw text directly so we represent it as a cotinuous-valued vectors. 
This section covers:
- **Tokenization:** Tokenization is done by using Byte pair encoding. Custom made tokenizer is slower than tiktokenizer library which uses Rust so we are using Tiktokenizer for BPE. Byte Pair encoding is used as complex and unique words gets broken down into most frequent tokens during BPE training. Vocabulary has some tokens for subword and complex word gets broken down into those subwords token. It is both word as well as character level tokenization. 

- **Token Embeddings:** Next convert token IDs into embedding vectors. Token embedding gives meaning to the ids. While training these tokens dimensions will change so tokens having similar meaning are together with each other in vector space. Embeddings are used to find meanings among the words and not see words as  unrelated, random ids.
- **Positional Encoding:** How do we find the order of IDs as transformers process words simultaneously we need to use positional vector to signify position of these ids.
	For eg: text 1 = Man chased the dog 
				text 2 = Dog chased the man.   
				if there was no positional encoding these two text would be same 


## 3. Attention Mechanism:
Attention mechanism allows each word in a sequence to look at each other and provide importance to it.
- **Self attention:** Implemented self attention as a example  without using query,key, values and masking at first to visualize how attention works. 
	- compute attention scores : 
	- Find attention weights: Normalize attention scores 
	- Find context vectors:
- **Self attention with trainable weights(Key, Query, Value):**
	- Query: It represents current item  the model focuses on or tries to understand. (analogous to search query)
	- Key: Key is like using database key used for searching and indexing 
	- Value: actual content or representation of input items
	
	we initialize query weight, key weight, and value weight as random parameters of some size which is the 		 used to find keys, queries, values through matrix multiplication with input.
		- attention score = queries and keys 
		- attention weight = normalization by embedding dimension so its called scaled-dot product attention 
		- context vectors = attention weight and values 
- **Hiding future values with casual attention and using Dropout:**
	Self attention mechanism needs to only consider the tokens that appear prior to the current position when predicting the next token in a sequence. Casual attention is also  called masked attention.mask attention scores with -inf above diagonal and use softmax. 
	- Dropout: Dropout is a technique where randomly selected hidden layer units are ignored during training to prevent overfitting. Dropout is only used during training and disabled afterwards.

- **Multihead attention:**
	Multihead means divinding the attention meachanism into multiple "heads"each operating independently

## 4. RESULTS till now 
In this I have made a GPT2 model architecture from scratch for the training purposes.Since training a model in huge dataset is not feasible and takes huge computing resources. Two approaches are followed where one is we train model on random weight. Next since GPT2 Model weights are publicly available load that weight and train on that weight these approaches are used. <br>
**<u>NOTE: Below given is not a final result work is being carried out and different approach and evaluation metrics will be used and results will be updated</u>**
<br>final.ipynb has everything jumbles in single file if u want to recreate and retrain yourself 

![result1](https://github.com/Sangameeee/LLM-from-scratch/blob/main/results/result1.png?raw=true)

![result2](https://github.com/Sangameeee/LLM-from-scratch/blob/main/results/result2.png?raw=true)






