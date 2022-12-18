```
Source: 汤姆喜欢和他的朋友们踢足球。
Target: Tom likes to play soccer with his friends.

Translations:
    [RNN]: Tom likes to study friends with his friends.
    [TF]: Tom and his friends like soccer.
```

# Neural Machine Translation

In this notebook, machine translation is implemented using two deep learning approaches: a Recurrent Neural Network (RNN) and Transformer. Specifically, Sequence to Sequence models for Chinese Mandarin to English translation are trained using [anki data](http://www.manythings.org/anki/). All language models and associated data can be accessed in `languages` directory. Alternative pre-processing approaches were necessary for languages with different scripts. The notebook demonstrates a unique approach for Chinese Mandarin, but other language groups such as latin script based languages (e.g., English, French, Portuguese, etc.) required alternative pre-processing criteria. For instance, the `hgtk` package was used to pre-process Hangul script for Korean. Semitic languages such as Arabic and Hebrew required special steps to flip sentence direction prior to model training, and after model inference. Other languages such as Russian were processed more conservatively.

The original NMT notebook and an interactive demo translator can be accessed in the following links.
* NMT Notebook: [![Open Notebook In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/wjonasreger/neural_machine_translation/blob/main/neural_machine_translation.ipynb)
* Demo Translator: [![Neural Translate](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1FNUle-E1SuLS3ciRT6pLgjspLibaTejj?usp=sharing)

---

Encoder and Decoder models for Recurrent Neural Networks and Transformers are implemented in this notebook. The notebook shows a demonstration of data pre-processing, model training, model inference, and model evaluation on predicted sentence translations from Chinese Mandarin to English. The data contains 29371 example bilingual pairs from Anki. 

Here are some examples of predicted English sentences compared with actual English sentences from a given Chinese Mandarin sentence for the two approaches. BLEU scores are also shown below.

1. Recurrent Neural Network

```
----------------
Source sentence: <START> 我 在 等 他 。 <END>
Target sentence: <START> i m waiting for him . <END>
Predicted sentence: <START> i m waiting for him . <END>
----------------
Source sentence: <START> 我 寧 願 工 作 也 不 願 閒 著 。 <END>
Target sentence: <START> i prefer working to doing nothing . <END>
Predicted sentence: <START> i d rather stay than i have to lose weight . <END>
----------------
Source sentence: <START> 他 來 自 波 士 頓 。 <END>
Target sentence: <START> i m from boston . <END>
Predicted sentence: <START> he came in boston . <END>
----------------
Source sentence: <START> 湯 姆 買 了 張 機 票 。 <END>
Target sentence: <START> tom bought a plane ticket . <END>
Predicted sentence: <START> tom bought a ticket . <END>
----------------
Source sentence: <START> 我 相 信 他 會 成 功 。 <END>
Target sentence: <START> i m sure that he ll succeed . <END>
Predicted sentence: <START> i believe he ll succeed . <END>
----------------
Loss 1.1556
BLEU 1-gram: 0.236252
BLEU 2-gram: 0.062643
BLEU 3-gram: 0.043685
BLEU 4-gram: 0.039369
----------------
```

2. Transformer

```
----------------
Source sentence: <START> 我 做 得 好 到 不 能 再 好 了 。 <END>
Target sentence: <START> i can t do any better . <END>
Predicted sentence: <START> i can t do it anymore . <END>
----------------
Source sentence: <START> 我 和 汤 姆 说 了 ， 我 觉 得 这 个 主 意 很 好 。 <END>
Target sentence: <START> i told tom that i thought that it was a good idea . <END>
Predicted sentence: <START> i told tom i thought that it was a good idea . <END>
----------------
Source sentence: <START> 汤 姆 已 经 结 婚 了 。 <END>
Target sentence: <START> tom s married . <END>
Predicted sentence: <START> tom has already married . <END>
----------------
Source sentence: <START> 請 你 鎖 門 好 嗎 ？ <END>
Target sentence: <START> would you please lock the door ? <END>
Predicted sentence: <START> would you please close the door ? <END>
----------------
Source sentence: <START> 請 告 訴 我 該 怎 麼 做 。 <END>
Target sentence: <START> please tell me what to do . <END>
Predicted sentence: <START> please tell me what to do . <END>
----------------
Loss 2.4514
BLEU 1-gram: 0.230886
BLEU 2-gram: 0.060984
BLEU 3-gram: 0.042378
BLEU 4-gram: 0.038043
----------------
```
