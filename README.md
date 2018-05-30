# Optimized word2vec and fastText for biomedical embeddings

This repo includes pre-trained Skip-Gram word2vec and fastText models as well as additional resources that were generated as part of the following publication. Please cite this paper if any of the resources are utilized or consult it if you require further details:

Dieter Galea, Ivan Laponogov, Kirill Veselkov. (2018). Sub-word information in pre-trained biomedical word representations: evaluation and hyper-parameter optimization. To appear in Proceedings of the 18th Workshop on Biomedical Natural Language Processing, Melbourne, Australia. (c) Association for Computational Linguistics. 

## Citation
```
@inproceedings{dieter2018fasttext,
  title={Sub-word information in pre-trained biomedical word representations: evaluation and hyper-parameter optimization},
  author={Dieter Galea, Ivan Laponogov, and Kirill Veselkov},
  booktitle={Proceedings of the 18th Workshop on Biomedical Natural Language Processing},
  year={2018}
}
```

## Pre-trained models

We provide the pre-trained models for the optimized word2vec and fastText. These models are trainable, i.e. they include all the necessary files for you to keep training these models with your own data. Having said that, these files (especially fastText models) can be quite large!

Optimization is based on development set of extrinsic NER corpora: CHEMDNER, JNLPBA, and BC2GM. Specifically, the optimized hyper-parameters are shown in the table below. Models optimized on the intrinsic datasets as well as globally-optimized (across intrinsic and extrinsic data) models will be available here soon.

| Hyper-parameter | word2vec (intrinsic) |  fastText (intrinsic)     |  word2vec (extrinsic)    |    fastText (extrinsic)   |
|----------------------------------|--------------------------------|-------|------|-------|
| Window                           | 30                             | 25    | 2    | 1     |
| Negative                         | 15                             | 3     | 5    | 10    |
| Sampling                         | 1e-5                           | 1e-5  | 1e-3 | 1e-3  |
| Min-count                        | 0                              | 0     | 10   | 5     |
| Alpha                            | 0.05                           | 0.05  | 0.1  | 0.025 |
| Dim                              | 200                            | 200   | 50   | 100   |
| N_grams                          | -                              | 6-7   | -    | 3-7   |


|   |  word2vec |  fastText |
|---|---|---|
| **extrinsic-optimized**  | [download](http://bit.ly/w2v_extrinsic)  | [download](http://bit.ly/ft_extrinsic)  |
|  **intrinsic-optimized** |  *available soon* | *available soon* |
|  **globally-optimized** |  *available soon* | *available soon*  |



## word2vec vs. fastText training times

We compare the training times for Skip-Gram word2vec and fastText as implemented in gensim, and as a function of the different hyper-parameters. As absolute times are dependent on the hardware configuration, we have normalized unit time to the time taken when training word2vec with default parameters. For reference, word2vec with default parameters took 70 minutes when trained on PubMed baseline 2018 corpus, and fastText with default parameters was 7x slower (490 minutes). 

The variation in training time with the different hyper-parameters are shown below for window size, negative sub-sampling, sampling rate, minimum word count, learning rate (alpha), dimensions, and n_char range for fastText. The gensim default values at the date of publishing are (quoted from gensim documentation):

```size=100, alpha=0.025, window=5, min_count=5, sample=0.001, min_alpha=0.0001, negative=5, min_n=3, max_n=6```

![Benchmarks](./benchmarks.png)

*Note: fastText compute time for 500 and 800 dimensions is not available as these were run on different hardware configurations. Performance in terms of accuracy for these hyper-parameter values are still evaluated in the publication.*
