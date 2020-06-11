# Bigram-based Hybrid Attack (BHA)

This repository contains Keras implementations of the paper: Bigram-based Hybrid Attack for Crafting Natural
Language Adversarial Samples.

## Overview
* `data_set/aclImdb/` , `data_set/ag_news_csv/`and`data_set/yahoo_10` are placeholder directories for the IMDB Review, AG's News and Yahoo! Answer, respectively.
* `word_level_process.py`and`char_level_process.py` contain two different prepressing methods of dataset for word-level and char-level, respectively.
* `neural_networks.py` contain implementations of four neural networks(word-based CNN, Bi-directional LSTM, char-based CNN, LSTM) used in paper.
* Use `training.py`to train four NN in `neural_networks.py`.
* `fool.py`, `evaluate_word_saliency.py`, `get_NE_list.py`,`adversarial_tools.py`and`paraphrase.py`build the experiment pipeline.
* Use `evaluate_fool_results.py` to evaluate classification accuracy and word replacement rate of adversarial examples generated by PWWS.

## Dependencies
* Python 3.7.1.
* Versions of all depending libraries are specified in `requirements.txt`. To reproduce the reported results, please make sure that the specified versions are installed.
* If you did not download WordNet(a lexical database for the English language), use `nltk.download('wordnet')` to do so.(Cancel the code comment on line 14 in `paraphrase. py`) 


## Usage

* Download dataset files from [google drive](https://drive.google.com/open?id=1YdndNH0RE6BEpg04HtK6VWemYrowWzvA) , which include
    - IMDB: `aclImdb.zip`. Decompression and place the folder`aclImdb` in`data_set/`.
    - AG's News: `ag_news_csv.zip`. Decompression and place the folder `ag_news_csv` in`data_set/`.
    - Yahoo Answers: `yahoo_10.zip`. Decompression and place the folder `yahoo_10` in`data_set/`.
* Download `glove.6B.100d.txt`from [google drive](https://drive.google.com/open?id=1YdndNH0RE6BEpg04HtK6VWemYrowWzvA) and place the file in `/`.
* Run `training.py` or use command like`python3 training.py --model word_cnn --dataset imdb --level word`. You can reset the model hyper-parameters in `neural_networks.py` and `config.py`.Note that neither this repository nor the paper provides an implementation of char_cnn on IMDB and Yahoo! Answers datasets.
* Run `fool.py` or use command like`python3 fool.py --model word_cnn --dataset imdb --level word`to generate adversarial examples using PWWS.
* Run`evaluate_fool_reaults.py`to evaluate adversarial examples. 
* If you want to train or fool different models, reset the argument in `training.py`and`fool.py`.
### Result on pretrained model

`runs/`contains some pretrained NN models, the information of these models are showed as the following table. 

We use these pretrained models to generate 1000 adversarial examples with PWWS.

- `test_set` means classification accuracy on test set.
- `clean_1000` means classification accuracy on the 1000 clean samples(from test set).
- `adv_1000` means classification accuracy on the adversarial examples corresponding to the 1000 clean samples.
- `sub_rate` means word replacement rate defined in `Section 4.4`.
- `NE_rate` means  (number of $NE_{adv}$)/(number of substitute word).

If you want to use this model, rename the them or modify the paths to model in the `.py` files.

| data_set       | neural_network | test_set | clean_1000 | adv_1000  | sub_rate | NE_rate |
| -------------- | -------------- | -------- | ---------- | --------- | -------- | ------- |
| IMDB           | word_cnn       | 88.792%  | 86.2%      | 5.7% | 3.933%   | 21.395% |
|                | word_bdlstm    | 87.472%  | 86.8%      | 2.0%      | 4.206%   | 11.094% |
|                | word_lstm      | 88.420%  | 89.8%      | 10.4%     | 6.816%   | 6.548%  |
| AG's News      | word_cnn       | 90.526%  | 89.0%      | 13.2%     | 12.308%  | 30.877% |
|                | word_bdlstm    | 90.711%  | 89.3%      | 12.9%     | 13.494%  | 27.227% |
|                | word_lstm      | 91.829%  | 91.4%      | 18.1%     | 18.102%  | 27.374% |
|                | char_cnn       | 88.224%  | 88.5%      | 20.0%     | 11.979%  | 23.241% |
| Yahoo! Answers | word_cnn       | 88.427%  | 96.1%      | 8.7%      | 33.067%  | 12.768% |
|                | word_bdlstm    | 88.876%  | 94.4%      | 9.4% | 20.752% | 7.016% |

## Contact

* If you have any questions regarding the code, please create an issue or contact the [owner](https://github.com/RenShuhuai-Andy) of this repository.

##  Acknowledgments

- Code refer to: textfool ([Zenodo](https://zenodo.org/record/831638)/[Github](https://github.com/bogdan-kulynych/textfool)).
