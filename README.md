# Project Overview

This repository demonstrates a Sequence-to-Sequence Sentiment Mapping model designed to interpret the emotional context of text and predict the most appropriate emoji. This project focuses on the implementation of Long Short-Term Memory (LSTM) networks to capture semantic context  in short-form text, leveraging pre-trained word embeddings for semantic depth.

# Resources 

This model utilizes the GloVe 6B 100d dataset, a collection of pre-trained word embeddings from Stanford University. By mapping words to 100-dimensional vectors based on a 6-billion-token corpus from Wikipedia and Gigaword, the model understands their semantic relationships.

# Model Architecture 
```
┌─────────────────────────────────────────┐
│          INPUT LAYER                    │
│    Tokenized Sentences (maxlen=10)      │
│    Shape: (batch_size, 10)              │
└─────────────────┬───────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────┐
│         EMBEDDING LAYER                 │
│    vocab_size=312, embed_dim=100        |
│    Using GloVe Pre-trained Weights      │
│    trainable = False                    │
│    Output: (10, 100)                    │
└─────────────────┬───────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────┐
│           LSTM LAYER 1                  │
│           units = 16                    |
│      return_sequences = True            │
│    Output: (10, 16)                     │
└─────────────────┬───────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────┐
│           LSTM LAYER 2                  │
│            units = 4                    │
│      return_sequences = False           │
│     Output: (4,)                        │
└─────────────────┬───────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────┐
│           DENSE LAYER                   │
│            units = 5                    │
│        activation = softmax             │
│     Output: (5,) - 5 Emoji Classes      │
└─────────────────────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────┐
│          OUTPUT (Emoji)                 │
│  0: ❤️ (love)     1: ⚾ (sports)       |
│  2: 😃 (happy)    3: 😞 (sad)          │
│  4: 🍽️ (food)                           |
└─────────────────────────────────────────┘
```

# Credits 
@ Coding-Lane
- This project was inspired while learning implentations in Reccurent Neural networks:
   [RNN playlist](https://www.youtube.com/watch?v=lWPkNkShNbo&list=PLuhqtP7jdD8ARBnzj8SZwNFhwWT89fAFr)


#  Future Aspirations

##  Future Aspirations

This project lays a strong foundation for context-aware emoji prediction, but there is significant potential to evolve it into a more robust, real-world solution. My future roadmap focuses on three key areas:

### 1. Scaling to Real-World Data & Vocabulary

The current model is trained on a limited vocabulary, which restricts its ability to generalize. My primary goal is to adopt a much larger and more diverse dataset, specifically the **[Twitter Emoji Prediction dataset from Kaggle](https://www.kaggle.com/datasets/hariharasudhanas/twitter-emoji-prediction)**. This dataset contains thousands of real tweets with corresponding emoji labels, exposing the model to authentic, informal, and diverse language patterns, including slang, abbreviations, and varied sentence structures.

### 2. Advancing the Architecture for Performance

To effectively learn from this larger, more complex dataset, I plan to upgrade the model architecture:

- **From LSTM to Bi-directional LSTM (Bi-LSTM):** The recommended approach for the Twitter dataset is a Bi-LSTM, which will allow the model to capture context from *both* past and future words in a sentence, leading to a deeper semantic understanding.

- **Leveraging Larger Embeddings:** I will integrate pre-trained **GloVe 42B-dimensional embeddings** (as suggested for the dataset), moving from my current 100-dimensional vectors. This will provide a richer, more nuanced representation of word meanings.

