# keraslm-models

These are model files for [ocrd_keraslm](https://github.com/OCR-D/ocrd_keraslm), trained on [DTA](http://www.deutsches-textarchiv/download) plaintexts (TCF TextCorpus annotation) on GPU. They can be used on a GPU (Tensorflow with CUDA) or CPU installation.

To achieve best results for prediction, make sure to feed similar formatted input: consecutive UTF-8 plain-text (mostly German, but some Greek, Hebrew etc as well), with newline at line and paragraph boundaries, but not page numbers, form feed or the like.

## parameters and perplexity estimates

Parameters are:
* depth: the number of hidden layers
* width: the number of LSTM elements per hidden layer
* length: the number of bytes per window (preceding context)
* stateful: whether the hidden state gets propagated from one window to the next implicitly (unless controlled explicitly in incremental mode)

During training, 20% of the data were held out for validation to prevent overfitting. On these validation data, the following perplexity was measured (which can be viewed as a noisy estimate of generalization perplexity), byte-wise:

basename | ppl | century | depth | width | length | stateful
-------- | --- | ------- | ----- | ----- | ------ | --------
model_dta17_l2_25bs_128 | 5.49 | 17xy | 2 | 128 | 25| True
model_dta19_l2_15bs_256 | 6.03 | 19xy | 2 | 256 | 15 | True
model_dta19_l3_15b_256 | 5.20 | 19xy | 3 | 256 | 15 | False
model_dta19_l4_256bs_128 | 4.88 | 19xy | 4 | 256 | 128 | True

More to come!
