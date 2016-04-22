# verb2graph
Here is a tool for presenting word2vec models as graphs using networkx library.

## About
The work is done as a part of VerbNet project developed at *Higher School of Economics, Moscow, Philology department, master's programme [Computational Linguistics](https://www.hse.ru/en/ma/ling/).* For further information on the project, visit http://web-corpora.net/wsgi3/ru-verbs/

### What's that?
We're making a [Princeton](https://wordnet.princeton.edu/)-like lexicon of Russian verbs, and we are set to get the best of both data-driven and lexicography-based approaches. Data-driven approach to populating synset base has many faces. And the first one we tried is to create a proto semantic network out of a word2vec model, which is essentially a distributed semantic model for words with its dimension reduced to a reasonable number without losing the distances. The general idea is as follows:

1. Take a word2vec model trained by Andrey Kutuzov.
2. Either fix a threshold T or a number of most similar words N.
3. Create a graph of all the verbs in the model that are at the same time present in Lyashevskaya-Sharoff frequency dictionary. The frequency dictionary is used to filter out typos and obscure words, which are not any good for statistical model anyway.
4. For each vertex in the graph, add an edge between it and each other vertex that is either has similarity score above T according to the model or is among that vertex' N most similar words.

The graph constructed this way is then analyzed one connected component at a time using graph community detection algorithm, which is basically clustering of graph vertices. The resulting communities often look like feasible synsets or make good sense as a (somewhat narrow) semantic classes that can be partitioned again to get synset-like communities again. The results are then intended to be used for populating the wordnet database.

![cook](http://web-corpora.net/wsgi3/ru-verbs/static/pictures/comm3.png)

You can check out the [initial report](http://web-corpora.net/wsgi3/ru-verbs/static/papers/verb2graph-report.pdf) and [slides](http://web-corpora.net/wsgi3/ru-verbs/static/papers/verb2graph-slides.pdf) on the matter.

## Requirements
* python 3.4+
* ipython/jupyter notebook
* scipy
* numpy
* matplotlib
* gensim
* networkx

## Setup and usage
1. Clone this repository or just download and unzip it.
2. Create `models` folder located in the same folder as your `verb2graph.ipynb.`
3. Put there your models, which you should get from http://ling.go.mail.ru/dsm/en/about#models.
4. Start your ipython/jupyter notebook there, specify the file name of models you want to work with, and you are all set.

## License notes
`community.py` is a module developed by third-party developers and is only placed here for your convenience
as it was originally written in python2 and had to be converted in order to work with python3 notebook.

## Related repos
You can also:
* [Parse yourself some synsets from synonym dictionary](https://github.com/tiefling-cat/bparser)
* [Get yourself a tool to predict aspect of Russian verbs](https://github.com/tiefling-cat/guessing-aspect)
