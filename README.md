# chinese-poem-search
输入现代白话或古文，找到意思接近的古诗

举例
```
    输入 你看那长江的水从天上来
      1: 李白 [鼓吹曲辞将进酒]
      君不见黄河之水天上来，奔流到海不复回．．．
      2: 马之纯 [新亭其二]
      新亭见说在山头，看见江河衮衮流．．．
      3: 释善果 [偈其五]
      苏州有，常州有，吸尽西江只一口．．．


    输入：忆长安
      1: 宋祁 [农阁]
      ...看云记巫峡，望日省长安。...
      2: 徐凝 [寄白司马]
      ...争遣江州白司马，五年风景忆长安。
      3: 崔涂 [春晚怀进士韦澹]
      ...二年春怅望，不似在长安。
```

简介

*   简单来说就是用预训练的语言模型来得到诗句的向量，放到scaNN里面索引，然后输入查询语句也得到向量并查询scaNN的最近邻居。
*   Based on [guwenBERT](https://huggingface.co/ethanyt/guwenbert-base) (an ancient chinese pre-trained [RoBERTa](https://arxiv.org/abs/1907.11692) language model), [HF Transformers](https://github.com/huggingface/transformers) (model inference), and [Google sanNN](https://github.com/google-research/google-research/tree/master/scann) (approximate nearest neighbor search)
*   We fetch chinese poems from this [chinese-poetry github project](https://github.com/chinese-poetry/chinese-poetry), and divide to sentence pieces
*   Converted to simplified Chinese input using [chinese-converter package](https://github.com/zachary822/chinese-converter), please skip if you prefer traditional Chinese
*   Use the last layer hidden output as embedding to balance quality and memory constraints, [literature](http://jalammar.github.io/illustrated-bert/) recommends last 4 layers but cannot afford memory
*   Note the colab runs successfully with high RAM GPU colab instance (paid class, Tesla P100 GPU with 16G GPU ram, 2 core CPU with 24G ram). If you encourter with OOM issue, reduce the `SAMPLE_SIZE` value will help, or consider to upgrade to paid colab class ($9.99 per month with awesome GPU!!).
*   Colab takes about 1 hour to fully load/transform/initialize, after that, the inference should take <100ms per call.
