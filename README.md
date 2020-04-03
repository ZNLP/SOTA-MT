# SOTA-MT
This project attempts to maintain the SOTA performance in machine translation.

Machine translation has entered the era of neural methods, which attracts more and more researchers. Currently, hundreds of MT papers are published each year and it is a bit difficult for researchers to know the SOTA models in each research direction. Accordingly, we try to record the SOTA performance in this project.

There are several research directions in neural machine translation, including architecture design, multimodal translation, speech and simultaneuous translation, document translation, multilingual translation, semi-supervised translation, unsupervised translation, domain adaptation, non-autoregressive translation and etc. It is a pity that there is no widely used benchmark datasets in many research tasks such as document translation, multilingual translation and domain adaptation. Thus, we try our best to record the SOTA performance for the tasks in which there is dataset employed by several papers.

Note that we would definitely miss some new SOTA model and please remind us if you know. Furthermore, it is the best way to employ SacreBLEU[1] to report BLEU scores for fair comparison on widely used datasets. However, many papers do not apply it.

Architecture Exploration starting from Transformer with similar scale of network parameters. We use the dataset WMT14 en-de and detokenized case-sensitive BLEU for comparison.

| Architecture            | WMT14 en-de | BLEU-tool   |
| ----------------------- | ----------- | ----------- |
| Transformer[1]          | 28.4        | not mention |
| Relative Transfromer[2] | 29.2        | not mention |
| DynamicConv[3]          | 29.7        | multi-bleu  |
| Evolved Transformer[4]  | 29.8        | multi-bleu  |
| Macaron Net[5]          | 30.2        | not mention |

｜Architecture             ｜  WMT14 en-de  ｜    BLEU-tool ｜
｜-------------------------|----------------｜--------------｜
｜Transformer[2]           ｜    28.4       ｜    \*multi-bleu｜
｜Relative Transfromer[3]  ｜    29.2       ｜    \*multi-bleu｜
｜DynamicConv[4]           ｜    29.7       ｜    multi-bleu｜
｜Evolved Transformer[5]   ｜    29.8       ｜    multi-bleu｜
｜Macaron Net[6]           ｜    30.2       ｜    \*multi-bleu｜
\* means that it is not mentioned in the paper and we guess from their codes.

[1] Matt Post. A Call for Clarity in Reporting BLEU Scores. In Proc. of WMT 2018.\
[2] Ashish Vaswani , Noam Shazeer, Niki Parmar, Jakob Uszkoreit, Llion Jones, Aidan N. Gomez, Łukasz Kaiser and Illia Polosukhin. 2017. Attention Is All You Need. In Proc. of NIPS 2017.\
[3] Peter Shaw, Jakob Uszkoreit and Ashish Vaswani. 2018. Self-Attention with Relative Position Representations. In Proc. of NAACL 2018.\
[4] Felix Wu, Angela Fan, Alexei Baevski, Yann N. Dauphin and Michael Auli. 2019. Pay Less Attention with Lightweight and Dynamic Convolutions. In Proc. of ICLR 2019.\
[5] David R. So, Chen Liang and Quoc V. Le. 2019. The Evolved Transformer. In Proc. of ICML 2019.\
[6] Yiping Lu, Zhuohan Li, Di He, Zhiqing Sun, Bin Dong, Tao Qin, Liwei Wang and Tie-Yan Liu. 2019. Understanding and Improving Transformer From a Multi-Particle Dynamic System Point of View. arXiv:1906.02762
