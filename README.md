# Comparing Multilingual Models for Similar-Language Translation
Author: Edyta Rozczypała

Course: Natural Language Processing with Deep Learning, School of Applied Mathematics and Computer Science, University Josip Juraj Strossmayer of Osijek, 2025/2026

The project collab notebook is located at https://colab.research.google.com/drive/1-2FlvYBbKq2E_BQ8h3luFyNfbNp3HmfE

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
## Results
In the below table are BLEU scores for cycle translations for the multilingual model. Note that the reverse translations have a lower average BLEU score than the direct translations.
| Hr-Pl | reverse Hr-Pl | Pl-Hr | reverse Pl-Hr |
| :--: | :--: | :-----: | :------: |
| 5% | 3% | 2.2% | 0.6% |

In the below table are BLEU scores for cycle translations for the Slavic model. Note that the reverse translations have a higher average BLEU score than the direct translations, which is surprising considering the results of the multilingual model as well as what one may assume would happen.
| Hr-Pl | reverse Hr-Pl | Pl-Hr | reverse Pl-Hr |
| :--: | :--: | :-----: | :------: |
| 10.8% | 19.5% | 11.8% | 18.8% |

In the below table are BLEU scores for direct and indirect translations for the multilingual model. Note that the translations that go through English have a higher average BLEU score than the direct translations, which may be surprising, but mostly results from the low quality of Polish and Croatian translations. If we compare these results to the results from the Slavic model in the second table, than as expected the direct model does a better job of translating the texts.
| Hr-Pl | Hr-En-Pl |
| :--: | :--: |
| 5% | 8.7% |

Finally, in the below table are BLEU scores for translations for both models. As expected, the specialized model has significantly better results. What is interesting is that the results differ depending on in which direction the text is being translated. For the Slavic model the relative difference is small and may be accidental, but for the multilingual model this difference is bigger and it may be due to the amount of data from each of the language that the model was trained on.
| Multilingual Hr-Pl | Slavic Hr-Pl | Multilingual Pl-Hr | Slavic Pl-Hr |
| :--: | :--: | :-----: | :------: |
| 5% | 10.8% | 2.2% | 11.8% |
## Conclusion
In this work, I evaluated two models based on the quality of their Croatian-Polish translations. Predictably, the more specialized model produced better results. After manual evaluation it can be said that a lot of the translations were correct, even if they got lower BLEU scores, which can be attributed to the way that the BLEU score was constructed. The translations were mostly correct and the ones that had errors were mostly due to choosing the wrong translation of the word, that had a different meaning. 

The multilingual model produced worse results, in some cases even translating into English instead of the target language when there was an English word in the sentence. Besides that the model had some problems with verb tenses and grammatical modes (like subjunctive or conditional). This model definitely has space for improvement, which can be done by finetuning it with a large corpora of parallel data in Polish and Croatian.

Interestingly, there were a few instances of the models creating a word according to word building rules, but producing a non-existent word, which resulted in an incorrect translation.

As mentioned before, only a small amount of available data was used. This was mainly due to the speed of the multilingual model, which was significantly slower than the Slavic model and was not able to process to many sentences at a time. It would be beneficial if in future work the evaluation could happen on a bigger corpora.
## Installation
```
pip install -r requirements.txt
```
## How to Run
1. Install the dependencies
2. Create a secret token from HuggingFace.
3. Run the code or the Jupyter notebook
