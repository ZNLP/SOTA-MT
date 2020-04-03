# SOTA-MT
This project attempts to maintain the SOTA performance in machine translation.

# Introduction
Machine translation has entered the era of neural methods, which attracts more and more researchers. Currently, hundreds of MT papers are published each year and it is a bit difficult for researchers to know the SOTA models in each research direction. Accordingly, we try to record the SOTA performance in this project.

There are several research directions in neural machine translation, including architecture design, multimodal translation, speech and simultaneuous translation, document translation, multilingual translation, semi-supervised translation, unsupervised translation, domain adaptation, non-autoregressive translation and etc. It is a pity that there is no widely used benchmark datasets in many research tasks such as document translation, multilingual translation and domain adaptation. Thus, we try our best to record the SOTA performance for the tasks in which there is dataset employed by several papers.

Note that we would definitely miss some new SOTA model and please remind us if you know. Furthermore, it is the best way to employ SacreBLEU[1] to report BLEU scores for fair comparison on widely used datasets. However, many papers do not apply it.

# Architecture Design

We report architecture exploration starting from Transformer with similar scale of network parameters. We use the widely used dataset WMT14 en-de and detokenized case-sensitive BLEU for comparison.

| Architecture            | WMT14 en-de | BLEU-tool   |
| ----------------------- | ----------- | ----------- |
| Transformer[2]          | 28.4        | \*multi-bleu |
| Relative Transfromer[3] | 29.2        | \*multi-bleu |
| DynamicConv[4]          | 29.7        | multi-bleu  |
| Evolved Transformer[5]  | 29.8        | multi-bleu  |
| Macaron Net[6]          | 30.2        | \*multi-bleu |

\* means that it is not mentioned in the paper and we guess from their codes.

[1] Matt Post. A Call for Clarity in Reporting BLEU Scores. In Proc. of WMT 2018.\
[2] Ashish Vaswani , Noam Shazeer, Niki Parmar, Jakob Uszkoreit, Llion Jones, Aidan N. Gomez, Łukasz Kaiser and Illia Polosukhin. 2017. Attention Is All You Need. In Proc. of NIPS 2017.\
[3] Peter Shaw, Jakob Uszkoreit and Ashish Vaswani. 2018. Self-Attention with Relative Position Representations. In Proc. of NAACL 2018.\
[4] Felix Wu, Angela Fan, Alexei Baevski, Yann N. Dauphin and Michael Auli. 2019. Pay Less Attention with Lightweight and Dynamic Convolutions. In Proc. of ICLR 2019.\
[5] David R. So, Chen Liang and Quoc V. Le. 2019. The Evolved Transformer. In Proc. of ICML 2019.\
[6] Yiping Lu, Zhuohan Li, Di He, Zhiqing Sun, Bin Dong, Tao Qin, Liwei Wang and Tie-Yan Liu. 2019. Understanding and Improving Transformer From a Multi-Particle Dynamic System Point of View. arXiv:1906.02762

# Multimodal Translation
Generally speaking, multimodal translation addresses the translation task in which text, image and speech are all available. Currently, multimodal translation specially refers to pair image-text translation.

Given an image and its text description as source language, the task of image-text translation aims at translating the description in source language into the target language, where the translation process can be supported by information from the paired image. It is a task requiring the intergration of natural language processing and computer vison. The dataset Multi30K is widely used in this task and and the English description of each image is translated into German (and other languages in recent years). we report some SOTA models on Multi30K en-de 2016 testset below (case-insensitive tokenized BLEU).

| Model                   | Multi30K    |
| ----------------------- | ----------- |
| Double Attention[7]     | 36.5        |
| Imagination[8]          | 36.8        |
| VariationalMMT[9]       | 37.7        |


[7] Iacer Calixto, Qun Liu, and Nick Campbell. 2017. Doubly-Attentive Decoder for Multi-modal Neural Machine Translation. In Proc. of ACL 2017.\
[8] Desmond Elliott and Akos Kadar. 2017. Imagination Improves Multimodal Translation. In Proc. of IJCNLP 2017.\
[9] Iacer Calixto, Miguel Rios, and Wilker Aziz. 2019. Latent Variable Model for Multi-modal Translation. In Proc. of ACL 2019.




