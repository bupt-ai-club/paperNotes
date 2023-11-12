# Paper Notes {docsify-ignore-all}

&nbsp;&nbsp;本仓库用来记录论文笔记和总结，阅读时将作者观点和结论记录为自己的笔记，是一种对文献的理解和提炼过程，这有助于更好地理解和记忆文献。**艾宾浩斯遗忘曲线**告诉我们，
我们记下来的信息，一个月之后大约会忘掉79%。大脑的记忆功能分为短时记忆和长时记忆，它们分别像是计算机的内存和硬盘。短时记忆容量小，长时记忆靠不住，这是我们大脑在记忆这个层面的局限性。
通过写下来，把信息从短时记忆中卸载，让大脑聚焦于更为重要的思考和创造；通过写下来，然后加上定期的回顾，我们也可以解决长期记不住的问题。
我们作笔记的过程，也即是将我们接受到的信息写下来的过程。通过记笔记，让昨天的自己，为未来的自己增益。通过记笔记，让自己有一个外挂，让自己的人生“开挂”。



## 环境安装
### Node.js版本
Node v16

### 安装docsify
```shell
npm i docsify-cli -g
```


### 启动docsify
```shell
docsify serve ./docs
```

## BASE



## NLP

| 名字 | 简介 | 地址 | 会议/期刊 | 年份 | 笔记 | 代码 |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- |
|   Improving Language Understanding by Generative Pre-Training   |   GPT1   | [paper](https://cdn.openai.com/research-covers/language-unsupervised/language_understanding_paper.pdf)   | arXiv |  2018  |  [note](contents/NLP/Improving%20Language%20Understanding%20by%20Generative%20Pre-Training.md)  |  |   
|   Language Models are Unsupervised Multitask Learners   |   GPT2   |   [paper](https://insightcivic.s3.us-east-1.amazonaws.com/language-models.pdf)   |  arXiv |  2019 |   [note](contents/NLP/Language%20Models%20are%20Unsupervised%20Multitask%20Learners.md)   |      |  
|    Language Models are Few-Shot Learners   |   GPT3   |   [paper](https://arxiv.org/abs/2005.14165)   |  arXiv |  2020 |   [note](contents/NLP/Language%20Models%20are%20Few-Shot%20Learners.md)   |      |  
|     BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding   |   BERT   |   [paper](https://arxiv.org/abs/1810.04805)   |  NAACL |  2018 |   [note](contents/NLP/BERT.md)   |   [code](https://github.com/codertimo/BERT-pytorch)  |  
|     XLNet: Generalized Autoregressive Pretraining for Language Understanding  |   XLNet   |   [paper](https://arxiv.org/abs/1906.08237)   |  NeurIPS |  2019 |   [note](contents/NLP/XLNet.md)   |   [code](https://github.com/zihangdai/xlnet)  |



## CV


| 名字 | 简介 | 地址 | 会议/期刊 | 年份 | 笔记 | 代码 | 
| ---- | ---- | ---- | ---- | ---- | ---- | ---- |
|      |      |      |      |      |      |      | 


## LLM

| 名字 | 简介 | 地址 | 会议/期刊 | 年份 | 笔记 | 代码 | 
| ---- | ---- | ---- | ---- | ---- | ---- | ---- |
|      |      |     |     |      |      |      | 


## Model Compression

| 名字 | 简介 | 地址 | 会议/期刊 | 年份 | 笔记 | 代码 | 
| ---- | ---- | ---- | ---- | ---- | ---- | ---- |
|   DepGraph: Towards Any Structural Pruning   |   DepGraph   |  [paper](https://arxiv.org/abs/2301.12900)   |  CVPR   |  2023    |  [note](contents/ModelCompression/DepGraph.md)    |  [code](https://github.com/VainF/Torch-Pruning)    | 
| LLM-Pruner: On the Structural Pruning of Large Language Models  |  LLM-Pruner   |  [paper](https://arxiv.org/abs/2305.11627) |  NeurIPS   |  2023    |  [note](contents/ModelCompression/LLM-Pruner.md)  |  [code](https://github.com/horseee/LLM-Pruner) | 
| Structural Pruning for Diffusion Models  |  Diff-Pruning   |  [paper](https://arxiv.org/abs/2305.10924) |  NeurIPS   |  2023    |  [note](contents/ModelCompression/Structural%20Pruning%20for%20Diffusion%20Models.md)  |  [code](https://github.com/VainF/Diff-Pruning) | 
| LoRAShear: Efficient Large Language Model Structured Pruning and Knowledge Recovery  |  LoRAShear   |  [paper](https://arxiv.org/abs/2310.18356) |  arXiv   |  2023    |  [note](contents/ModelCompression/LoRAShear.md)  |   | 