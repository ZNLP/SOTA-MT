# SOTA-MT
This project attempts to maintain the SOTA performance on various sub-tasks in machine translation. We also give a detailed review of recent progress and potential research trends for NMT, available at https://arxiv.org/abs/2004.05809. Any comments and suggestions are welcome.

# 1. Introduction
Machine translation has entered the era of neural methods, which attracts more and more researchers. Currently, hundreds of MT papers are published each year and it is a bit difficult for researchers to know the SOTA models in each research direction. Accordingly, we try to record the SOTA performance in this project.

There are several research directions in neural machine translation, including architecture design, multimodal translation, speech and simultaneuous translation, document translation, multilingual translation, semi-supervised translation, unsupervised translation, domain adaptation, non-autoregressive translation and etc. It is a pity that there is no widely used benchmark datasets in many research tasks such as document translation, multilingual translation and domain adaptation. Thus, we try our best to record the SOTA performance for the tasks in which there is dataset employed by several papers.

Note that we would definitely miss some new SOTA models and please remind us if you know. Furthermore, it is the best way to employ SacreBLEU (Post, 2018) to report BLEU scores for fair comparison on widely used datasets. However, many papers do not apply it.

# 2. Architecture Design

We report architecture exploration starting from Transformer with nearly the same scale of network parameters. We use the widely used dataset WMT14 en-de and detokenized case-sensitive BLEU for comparison.

| Architecture            | WMT14 en-de | BLEU-tool   |
| ----------------------- | ----------- | ----------- |
| Transformer (Vaswani et al., 2017)          | 28.4        | \*multi-bleu |
| Relative Transfromer (Shaw et al., 2018) | 29.2        | \*multi-bleu |
| DynamicConv (Wu et al., 2019)          | 29.7        | multi-bleu  |
| Evolved Transformer (So et al., 2019)  | 29.8        | multi-bleu  |
| PRIME (Zhao et al., 2019)  | 29.9        | multi-bleu  |
| Macaron Net (Lu et al., 2019)          | 30.2        | \*multi-bleu |

\* means that it is not mentioned in the paper and we guess from their codes.

Yiping Lu, Zhuohan Li, Di He, Zhiqing Sun, Bin Dong, Tao Qin, Liwei Wang and Tie-Yan Liu. 2019. Understanding and Improving Transformer From a Multi-Particle Dynamic System Point of View. arXiv:1906.02762\
Matt Post. A Call for Clarity in Reporting BLEU Scores. In Proc. of WMT 2018.\
Peter Shaw, Jakob Uszkoreit and Ashish Vaswani. 2018. Self-Attention with Relative Position Representations. In Proc. of NAACL 2018.\
David R. So, Chen Liang and Quoc V. Le. 2019. The Evolved Transformer. In Proc. of ICML 2019.\
Ashish Vaswani , Noam Shazeer, Niki Parmar, Jakob Uszkoreit, Llion Jones, Aidan N. Gomez, Łukasz Kaiser and Illia Polosukhin. 2017. Attention Is All You Need. In Proc. of NIPS 2017.\
Felix Wu, Angela Fan, Alexei Baevski, Yann N. Dauphin and Michael Auli. 2019. Pay Less Attention with Lightweight and Dynamic Convolutions. In Proc. of ICLR 2019.\
Guangxiang Zhao, Xu Sun, Jingjing Xu, Zhiyuan Zhang and Liangchen Luo. 2019. MUSE: Parallel Multi-Scale Attention for Sequence to Sequence Learning. arXiv:1911.09483


# 3. Document-level Neural Machine Translation
In general, document-level machine translation aims at exploiting the useful document-level information (multiple sentences around the current sentence or the whole document) to improve the translation quality of the current sentence as well as the coherence and cohension of the translated document. Unfortunately, there is no widely used dataset in document-level translation.

### 3.1. Evaluation on BLEU
In 2019, Maruf et al. evaluated their method on three diverse datasets on English-German translation including TED, NEWS and Europarl. Below we show the training/development/test corpora statistics of the datasets (Docuemnt Length denotes average sentence number in each document).

| Domain  | #Sentences      | Document Length    |
| ------- | --------------- | ------------------ |
| TED     | 0.21M/9K/2.3K   | 120.89/96.42/98.74 |
| News    | 0.24M/2k/3k     | 38.93/26.78/19.35  |
| Europal | 1.67M/3.6K/5.1K | 14.14/14.95/14.06  |

We list several recent BLEU results on these datasets as follows.

| Model                | TED   | News  | Europarl |
| -------------------- | ----- | ----- | -------- |
| *Transformer-Doc (Zhang et al., 2018) | 24.00 | 23.08 | 29.32    |
| *HAN-Doc (Miculicich et al., 2018)         | 24.58 | 25.03 | 28.60    |
| SAN-Doc (Maruf et al., 2019)          | 24.42 | 24.84 | 29.75    |
| Capsule-Doc (Yang et al., 2019)      | 25.19 | 22.37 | 29.82    |
| Global-Context (Zheng et al., 2020)      | 25.10 | 24.91 | 30.40    |
| Flat-Transformer +BERT (Ma et al., 2020)      | 26.61 | 24.52 | 31.99    |

\* means that the resutls are not reported in the original paper but are reimplemented by Maruf et al. (2019).

### 3.2. Evaluation on Discourse Phenomena
In 2019, Voita et al. use En-Ru OpenSubtitles2018 corpus, and create hand-crafted test sets to evaluate discourse phenomena. The performances of differentm methods on various discourse phenomena are listed in the following table.

| Model         | BLEU  | Deixis(%) | Lexical cohesion(%) | Ellipsis inflection(%) | Ellipsis VP(%) |
| ------------- | ----- | --------- | ------------------- | ---------------------- | -------------- |
| Transformer   | 32.40 | 50.0      | 45.9                | 53.0                   | 28.4           |
| CADec (Voita et al., 2019a)     | 32.38 | 81.6      | 58.1                | 72.2                   | 80.0           |
| DocRepair (Voita et al., 2019b) | 34.60 | 91.8      | 80.6                | 86.4                   | 75.2           |
| Layer-Wise Weighting (Xu et al., 2020)     | 32.75 | 85.4      | 64.3                | 77.1                  | 81.3           |


Sameen Maruf, Andr´e FT Martins and Gholamreza Haffari. 2019. Selective attention for context-aware neural machine translation. In Proc. of NAACL 2019.\
Lesly Miculicich, Dhananjay Ram, Nikolaos Pappas and James Henderson. 2018. Document-level neural machine translation with hierarchical attention networks. In Proc. of EMNLP 2018.\
Elena Voita, Rico Sennrich and Ivan Titov. 2019a. When a good translation is wrong in context: Context-aware machine translation improves on deixis, ellipsis, and lexical cohesion. In Proc. of ACL 2019.\
Elena Voita, Rico Sennrich and Ivan Titov. 2019b. Context-Aware Monolingual Repair for Neural Machine Translation. In Proc. of EMNLP 2019.\
Zhengxin Yang, Jinchao Zhang, Fandong Meng, Shuhao Gu, Yang Feng and Jie Zhou. 2019. Enhancing context modeling with a query-guided capsule network for document-level translation. In Proc. of EMNLP 2019.\
Jiacheng Zhang, Huanbo Luan, Maosong Sun, FeiFei Zhai, Jingfang Xu, Min Zhang and Yang Liu. 2018. Improving the transformer translation model with document-level context. In Proc. of EMNLP 2018.\
Zaixiang Zheng, Xiang Yue, Shujian Huang, Jiajun Chen and Alexandra Birch. 2020. Toward Making the Most of Context in Neural Machine Translation. arXiv:2002.07982.\
Hongfei Xu, Deyi Xiong, Josef van Genabith and Qiuhui Liu. 2020. Efficient Context-Aware Neural Machine Translation with Layer-Wise Weighting and Input-Aware Gating. In Proc. of IJCAI 2020.\
Shuming Ma, Dongdong Zhang, Ming Zhou. 2020. A Simple and Effective Unified Encoder for Document-level Machine Translation. In Proc. of ACL 2020.

# 4. Non-autoregressive Transformer
Different from autoregressive left-to-right decoding, non-autoregressive Transformer (NAT), which is firstly proposed by Gu et al. (2018), generates the target language sentence by outputting all the target words simultaneously in parallel. Thanks to the significant decoding speedup, NAT has drawn more and more attention in recent research. Here, we list some SOTA methods that achieve similar or higher inference efficiency compared to Gu et al. (2018) while using single model without rescoring. The comparisons are also conducted on WMT14 en-de dataset. Transformer employs the base model.

| Model            | BLEU  | Speedup |
| ---------------- | ----- | ------- |
| Transformer   | 27.30 | 1.0×   |
| NAT (Gu et al., 2018)          | 17.69 | 15.6×  |
| *ENAT (Guo et al., 2019)        | 20.65 | 25.3×  |
| *NAT-REG (Wang et al., 2019)     | 20.65 | 27.6×  |
| *NAT-Hint (Li et al., 2019)    | 21.11 | 30.2×  |
| #Imitate-NAT (Wei et al., 2019) | 22.44 | 18.6×  |
| *ReorderNAT (Ran et al., 2019)  | 22.79 | 16.1×  |

\* denotes that the authors did not report the performance of their NAT reimplementation on test sets. # denotes that the authors reported their NAT reimplementation and the BLEU score is 19.69 on WMT14 en-de.


Jiatao Gu, James Bradbury, Caiming Xiong, Victor OK Li and Richard Socher. 2018. Non-autoregressive Neural Machine Translation. In Proc. of ICLR 2018. \
Junliang Guo, Xu Tan, Di He, Tao Qin, Linli Xu and Tie-Yan Liu. 2019. Non-autoregressive Neural mMchine Translation with Enhanced Decoder Input. In Proc. of AAAI 2019. \
Zhuohan Li, Zi Lin, Di He, Fei Tian, Tao Qin, Liwei Wang and Tie-Yan Liu. 2019. Hint-based training for non-autoregressive machine translation. In Proc. of EMNLP 2019. \
Qiu Ran, Yankai Lin, Peng Li and Jie Zhou. 2019. Guiding Non-Autoregressive Neural Machine Translation Decoding with Reordering Information. arXiv:1911.02215.\
Yiren Wang, Fei Tian, Di He, Tao Qin, ChengXiang Zhai and Tie-Yan Liu. 2019. Non-Autoregressive Machine Translation with Auxiliary Regularization. In Proc. of AAAI 2019. \
Bingzhen Wei, Mingxuan Wang, Hao Zhou, Junyang Lin and Xu Sun. 2019. Imitation Learning for Non-autoregressive Neural Machine Translation. In Proc. of ACL 2019. 

# 6. Unsupervised Neural Machine Translation
Unsupervised neural machine translation (UNMT) addresses a very chellenging scenario in which we are required to build a NMT model using only massive source- and target-side monolingual data. It was firstly proposed by Artetxe et al. (2018a) and Lample et al. (2018a). UNMT has quickly become one of the most popular research task in NMT. We list some recent models achieving SOTA performance. Most studies did experiments on WMT16 en-de test sets and we list model performance (BLEU scores) on these test sets.

| Model                  | de-en | en-de |
| ---------------------- | ----- | ----- |
| Lample et al. (2018a)  | 13.3  | 9.6   |
| Artetxe et al. (2018b) | 23.1  | 18.2  |
| Lample et al. (2018b)  | 25.2  | 20.2  |
| Lample et al. (2019)   | 34.3  | 26.4  |
| Artetxe et al. (2019)  | 34.4  | 26.9  |
| Song et al. (2019)     | 35.2  | 28.3  |
| Ren et al. (2019)      | 35.5  | 27.9  |
| Li et al. (2020)       | 35.6  | 28.4  |


Mikel Artetxe, Gorka Labaka, Eneko Agirre, and Kyunghyun Cho. 2018a. Unsupervised Neural Machine Translation.  In Proc. of ICLR 2018.\
Mikel Artetxe, Gorka Labaka, and Eneko Agirre. 2018b. Unsupervised Statistical Machine Translation. In Proc. of EMNLP 2018.\
Guillaume Lample, Alexis Conneau, Ludovic Denoyer, Marc’Aurelio Ranzato. 2018a. Unsupervised Machine Translation using Monolingual Corpora Only.  In Proc. of ICLR 2018.\
Guillaume Lample, Myle Ott, Alexis Conneau, Ludovic Denoyer, Marc’Aurelio Ranzato. 2018b. Phrase-Based & Neural Unsupervised Machine Translation. In Proc. of EMNLP 2018.\
Guillaume Lample and Alexis Conneau. 2019. Cross-lingual language model pretraining.  In Proc. of NeurIPS 2019.\
Mikel Artetxe, Gorka Labaka, Eneko Agirre. 2019. An Effective Approach to Unsupervised Machine Translation. In Proc. of ACL 2019.\
Shuo Ren, Yu Wu, Shujie Liu, Ming Zhou and Shuai Ma. 2019. Explicit Cross-lingual Pre-training for Unsupervised Machine Translation. In Proc. of EMNLP 2019.\
Kaitao Song, Xu Tan, Tao Qin, Jianfeng Lu and Tie-Yan Liu. 2019. MASS: Masked Sequence to Sequence Pre-training for Language Generation. In Proc. of ICML 2019.\
 Zuchao Li, Rui Wang, Kehai Chen, Masao Utiyama, Eiichiro Sumita, Zhuosheng Zhang, and Hai Zhao. 2020. Data-dependent Gaussian Prior Objective for Language Generation. In Proc. of ICLR 2020.

# 6. Multimodal Translation
Generally speaking, multimodal translation addresses the translation task in which text, image and speech are all available. Currently, multimodal translation specially refers to pair image-text translation.

Given an image and its text description as source language, the task of image-text translation aims at translating the description in source language into the target language, where the translation process can be supported by information from the paired image. It is a task requiring the intergration of natural language processing and computer vison. The dataset Multi30K is widely used in this task and and the English description of each image is translated into German (and other languages in recent years). we report some SOTA models on Multi30K en-de 2016 testset below (case-insensitive tokenized BLEU). 

| Model                   | Multi30K    |
| ----------------------- | ----------- |
| Double Attention (Calixto et al., 2017)     | 36.5        |
| Imagination (Elliott and Kadar, 2017)          | 36.8        |
| VariationalMMT (Calixto et al., 2019)       | 37.7        |
| DistillingMMT (Ive et al., 2019)       | 38.0        |


Iacer Calixto, Qun Liu, and Nick Campbell. 2017. Doubly-Attentive Decoder for Multi-modal Neural Machine Translation. In Proc. of ACL 2017.\
Iacer Calixto, Miguel Rios, and Wilker Aziz. 2019. Latent Variable Model for Multi-modal Translation. In Proc. of ACL 2019.\
Desmond Elliott and Akos Kadar. 2017. Imagination Improves Multimodal Translation. In Proc. of IJCNLP 2017.\
Julia Ive, Pranava Madhyastha and Lucia Specia. Distilling Translations with Visual Awareness. In Proc. of ACL 2019.

# 7. Speech Translation

Speech translation is to translate a speech in one language into a text or a speech in another language, corresponding to speech-to-text translation and speech-to-speech translation, respectively. For the sake of evaluation convenience, we only consider speech-to-text translation here.

The traditional approach of speech translation is in a pipeline paradigm with the components of ASR, MT, and TTS. Recently, more and more researchers pay attention to the end-to-end methods to solve this task. Given a speech as input, the task of speech translation aims at directly translating the speech in source language into the target language. It is a task requiring the intergration of natural language processing and speech processing. 

We report some SOTA models of speech translation on Fisher en-es testset and Augmented Librispeech en-fr testset (case-insensitive tokenized BLEU).

| Method     | Fisher |
| :-:                  | :-:    |
| LSTM ST (Bansal et al., 2018)  | 29.4   |
| RNN ST (Stoian et al., 2020)| 34.6|
|+pretrained+augmented | 37.8|
| Multi-task+pre-trained word embedding (Chuang et al., 2020)| 36.32
| Attention-passing model (Sperber et al., 2019) | 36.7   |
| Phone Segmentation (Salesky et al., 2019) | 38.8   |
|Hybrid cascade (Salesky et al., 2020) | 45.0   |
| LSTM+multi-task(Weiss et al., 2017)   | 47.3   |
| LSTM ST+pre-train+SpecAugment (ESPet*)         | 48.39  |

| Method  | Enc pre-train | Dec pre-train | Augmented Librispeech |
| :-:  | :-: |    :-:      |      :-:         |
| LSTM ST (Berard et al., 2018) |  |  | 12.90  |
| +pre-train+multitask | ✔ | ✔   | 13.40 |
| LSTM ST+pretrain (ESPnet*)| ✔| ✔ |16.68 |
| Transformer+pre-train (Liu et al., 2019) | ✔| | 14.30|
| +knowledge distillation |✔ |  | 17.02 |
| TCEN-LSTM (Wang et al., 2020a) | ✔| ✔ | 17.05 |
|Transformer + ASR pre-train (Wang et al., 2020b) | ✔| ✔ | 15.97|
| +curriculum pre-train | ✔| | 17.66 |
| LSTM+pre-train+SpecAugment (Bahar et al., 2019)| ✔(236h)| ✔ | 17.00                  |
| Multilingual ST+pre-train(Inaguma et al., 2019) | ✔(472h)| | 17.60 |
| Transformer+ASR pre-train (Wang et al., 2020b)| ✔(960h)| |16.90 |
| +curriculum pre-train | ✔(960h)| |18.01 |
| VGGTransformer(Pino et al. 2019)    |   ✔(960h)   | ✔(WMT14)   | 21.65 |
 ---

*The results of ESPnet are copied from [https://github.com/espnet/espnet/blob/master/egs/libri_trans/st1/RESULTS.md][1] \
Parnia Bahar, Albert Zeyer, Ralf Schlter, and Hermann Ney. 2019. On Using Specaugment for End-to-End Speech Translation. arXiv preprint arXiv:1911.08876.\
Sameer Bansal, Herman Kamper, Karen Livescu, Adam Lopez, and Sharon Goldwater. 2018. Low-resource Speech-to-Text Translation. In Proc. of Interspeech 2018.\
Alexandre Berard, Laurent Besacier, Ali Can Kocabiyikoglu, and Olivier Pietquin. 2018. End-to-End Automatic Speech Translation of Audiobooks. In Proc. of ICASSP 2018.\
Yuchen Liu, Hao Xiong, Jiajun Zhang, Zhongjun He, Hua Wu, Haifeng Wang, and Chengqing Zong. 2019. End-to-End Speech Translation with Knowledge Distillation. In Proc. of Interspeech 2019.\
Juan Pino, Liezl Puzon, Jiatao Gu, Xutai Ma, Arya D. McCarthy, and Deepak Gopinath. 2019. Harnessing Indirect Training Data for End-to-End Automatic Speech Translation: Tricks of the Trade. In Proc. of IWSLT 2019.\
Elizabeth Salesky, Matthias Sperber, and Alan W Black. 2019. Exploring Phoneme-level Speech Representations for End-to-End Speech Translation. In Proc. of ACL 2019.\
Matthias Sperber, Graham Neubig, Jan Niehues, and Alex Waibel. 2019. Attention-passing Models for Robust and Data-efficient End-to-End Speech Translation. Transactions of ACL, 7:313–325.\
Ron J. Weiss, Jan Chorowski, Navdeep Jaitly, Yonghui Wu, and Zhifeng Chen. 2017. Sequence-to-Sequence Models can Directly Translate Foreign Speech. In Proc. of Interspeech, 2017.\
Chengyi Wang, Yu Wu, Shujie Liu, Zhenglu Yang, and Ming Zhou. 2020a. Bridging the Gap between Pretraining and Fine-tuning for End-to-End Speech Translation. In Proc. of AAAI 2020.\
Chengyi Wang, Yu Wu, Shujie Liu, Ming Zhou and Zhenglu Yang. 2020b. Curriculum Pre-training for End-to-End Speech Translation. In Proc. of ACL 2020 (arXiv:2004.10093).\
Mihaela C Stoian, Sameer Bansal, and Sharon Goldwater. 2020. Analyzing ASR pretraining for low-resource speech-to-text translation. Proc. of ICASSP. \
Salesky, Elizabeth, and Alan W. Black. 2020. Phone Features Improve Speech Translation. In Proc. of ACL 2020. \
Chuang, Shun-Po, et al. 2020. Worse WER, but Better BLEU? Leveraging Word Embedding as Intermediate in Multitask End-to-End Speech Translation. In Proc. of ACL.


[1]: https://github.com/espnet/espnet/blob/master/egs/libri_trans/st1/RESULTS.md


## Notes
This project is launched by Jiajun Zhang and maintained by the MT team members (Yuchen Liu, Xiaomian Kang, Long Zhou and et al.) in CASIA. If you have questions or comments, please drop an email to jjzhang@nlpr.ia.ac.cn or jiajunzhangwing@gmail.com.
