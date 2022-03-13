# Let's go HAM
Simple spam or ham assignment.

## Dataset
The dataset can be downloaded from [here](https://archive.ics.uci.edu/ml/machine-learning-databases/00228/smsspamcollection.zip). It should be unziped into the `data` folder.

## Notebooks
* [data\_analysis\_and\_splitting.ipynb](data_analysis_and_splitting.ipynb): Initial data overview/cleaning, feature engineering and dataset splitting. **This notebook needs to be run first, since it splits the dataset to expected partitions.**
* [dummy\_classifier.ipynb](dummy_classifier.ipynb): Dummy classifier, which always chooses the most common class, used as a performance baseline. 
* [multinomialNB\_classifier.ipynb](multinomialNB_classifier.ipynb): Contains a few experimental pipelines, using MultinomialNB as the classifier.
* [svm\_classifier.ipynb](svm_classifier.ipynb): Slightly more complext pipelines (including POS tags/custom features) using SVM.

## Install and run
First install dependencies

```
$ pipenv install
```

Serve the notebooks:

```
$ pipenv run jupyter notebook
```

## Results


| Model                           | Features                                                                                                      | F1 score (macro avg) | Training Time (s)     | Prediction Time (s)   |
|---------------------------------|---------------------------------------------------------------------------------------------------------------|----------------------|-----------------------|-----------------------|
| DummyClassifier                 | -                                                                                                             | 0.464                | 0.0013 | 0.0003 |
| MultinomialNB (CountVectorizer) | `lemmas_without_punct`                                                                                        | 0.951                | 0.4200   | 0.0234  |
| MultinomialNB (TfidfVectorizer) | `lemmas_without_punct`                                                                                        | 0.952                | 0.1103   | 0.0130  |
| MultinomialNB (CountVectorizer) | `lemmas_without_puct_and_stop_words`                                                                          | 0.957                | 0.2253   | 0.0177  |
| MultinomialNB (TfidfVectorizer) | `lemmas_without_puct_and_stop_words`                                                                          | 0.949                | 0.0784   | 0.0081  |
| SVC(CountVectorizer)            | `lemmas_without_punct`                                                                                        | 0.942                | 0.9401    | 0.1049   |
| SVC(CountVectorizer)            | `lemmas_without_puct_and_stop_words`                                                                          | 0.941                | 0.6900    | 0.0716   |
| **SVC(CountVectorizer)**            | `lemmas_without_puct_and_stop_words` `pos_without_puct_and_stop_words`                                        | **0.970**              | 0.6734    | 0.0760   |
| SVC(CountVectorizer)            | `lemmas_without_puct_and_stop_words` `pos_without_puct_and_stop_words` `number_of_punct_tokens` `text_length` | 0.970                | 0.7124    | 0.084    |

## Improvements to be done
* More preprocessing: e.g. regex for special characters, replace phone numbers with special tag, replace long numbers with a tag, replace prices with a special tag, etc..
* Try out more pipeline permuations
* Gridsearch on a wider parameter space
* Try out RandomForest
* Refactor (oh boy 😬)
* Convert to scripts and save results to files for later evaluation
