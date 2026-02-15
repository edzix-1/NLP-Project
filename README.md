# Comparing Multilanguage Models for Similar Language translation
The project collab notebook is located at https://colab.research.google.com/drive/1qUXn9rluOBpVrSKaIvWSokChnhFlX7Fc

The video presentation can be found here https://youtu.be/pcACMnDs1Vo
## Abstract
Multilingual language models allow for translations between languages that have a small amount of direct training data. However, for languages from the same language family, this type of model may prove to be less accurate than a model focusing only on translating between those languages. In this project I would like to focus on analyzing different multilingual models and their weak points, in particular looking into Croatian and Polish translations. The BLEU score will be used for evaluation, as well as back and-forward and cycle translations will be examined to compare the result with the original. After the analysis, I will also look into finding possible improvements for those translations.
## Model
There are two models used in the project: Helsinki-NLP's MarianMT, specifically the Slavic-to-Slavic translation model and Facebook's mBART-50, which is a many-to-many multilingual transformer.
## Dataset
The dataset is taken from the MultiParaCrawl v7.1 corpus provided by OPUS. In the project 300 Polish-Croatian sentence pairs were used.
## Evaluation
The translations are evaluated using the BLEU scores using the implementation from the NLTK package. The scores are calculated for each sentence and then averaged across all samples.
## Experiments
### Multilingual model
1. Forward Translation
   - pl -> hr
   - hr -> pl
2. Back Translation
   - pl -> hr -> pl
   - hr -> pl -> hr
3. Indirect Translation
   - hr -> en -> pl
### Slavic model
1. Forward Translation
   - pl -> hr
   - hr -> pl
2. Back Translation
   - pl -> hr -> pl
   - hr -> pl -> hr
## Installation
```
pip install unzip transformers pandas nltk
```
## How to Run
1. Install the dependencies
2. Create a secret token from HuggingFace.
3. Run the code or the Jupyter notebook
