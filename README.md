word2vec+constraints
====================
This is an open source implementation of a modified version of word2vec's skip-gram architecture that includes constraints.

The modified skip-gram is able to jointly learn from corpora and a external source (such as a knowledge base) via a regularization term added in the former loss function. The regularizer incorporates extra semantic information from the external source (e.g. synonymy-related words from a knowledge base) into the learning process and thus adds co-occurrences that do not appear in the corpus.

Data you need
---------------

1. Monolingual or multilingual corpus
2. Monolingual or multilingual constraint file

Each line in the constraint file should start with a target word, followed by its corresponding contraints (space delimited) either monolingual or multilingual. The following example shows the English-Basque bilingual synonymy-related constraints for the word "moon" in WordNet 3.0g:
```
moon ilargi ilargi-argi lunation moonlight moonshine ilargite daydream ...
```

Running the algorithm
----------------------

```
./word2vec_constraints -train CORPORA.txt -output EMBEDDINGS.txt -size SIZE -window W -negative NG -cbow 0 -read-simconstr CONSTRAINTS.cst -lambdasim LAMBDA

./word2vec_constraints -train ENEU.txt -output ENEU.emb -size 300 -window 5 -negative 5 -cbow 0 -read-simconstr ENEU.cst -lambdasim 0.01
```
where "-read-simconstr" makes reference to the constraints file and "-lambdasim" to the regularization coefficient in the regularizer (usually, a coeffcient of 0.01 gives good results). 
