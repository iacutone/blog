---
title: "Machine Learning Word Prediction"
date: 2018-12-27T13:09:01-05:00
draft: true
---

In order to fulfill some work objectives for the quarter, I decided to take my machine learning skills to the next level. To accomplish this task, I explored ways to enhance the user experience for [our fundraiser application](fundraiser.fraxturedatlas.org). An unobtrusive machine learning project to introduce into the fundraising application which enhances the user experience is a word recomendation engine.

Many questions have arisen when exploring ways to implement this feature. The stack at Fractured Atlas is mostly written in Ruby. Do I try to find a Ruby machine learning solution? Also, how complicated of a solution should I write? Do I use a framework, use k-nearest neighbors, use a recurrent neural network in PyTorch?

After many hours researching, I decided the best design is something similar to [this](https://towardsdatascience.com/word-embedding-with-word2vec-and-fasttext-a209c1d3e12c) article. The author explain implementing a suggestion vector with PyTorch. As, I am already familiar with PyTorch, I believe this is a better place to start than other frameworks such as [gensim](https://github.com/RaRe-Technologies/gensim). Furthermore, I wanted a simple solution with less dependencies such as [this](https://github.com/nathanrooy/word2vec-from-scratch-with-python/blob/master/word2vec.py) word2vec python code. However, accounting for

The next thing to do was obtain a more in-depth understanging to word2vec. Tomas Mikolov has the original idea for the word2vec class or algorithms which incluce both skip-gram and continuous bag of tricks. [Here](https://arxiv.org/search/?searchtype=all&query=Mikolov&abstracts=show&size=50&order=announced_date_first) is a link to all of Mikolov's papers and [this](https://arxiv.org/abs/1301.3781) seems to be the first word2vec associated paper. 

Next steps will include some sort of data massaging. There are many words and numbers that can be scrubbed and turned into a better source of truth. I found [this](https://www.kaggle.com/mschumacher/using-fasttext-models-for-robust-embeddings) Kaggle guide valuable to scrub incoming corpus data.

[this](https://towardsdatascience.com/understanding-feature-engineering-part-4-deep-learning-methods-for-text-data-96c44370bbfa) one looks good too
- search #normalize_document as the post is large

Word2Vec
1. Skip-gram
2. Continuous back of words

Extracting similar vectors
gensim

[Stanford Lecture](https://www.youtube.com/watch?v=ERibwqs9p38)
[Fun with colors](https://gist.github.com/aparrish/2f562e3737544cf29aaf1af30362f469)
