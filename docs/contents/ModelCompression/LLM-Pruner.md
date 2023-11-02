# LLM-Pruner: On the Structural Pruning of Large Language Models

**作者：** Xinyin Ma Gongfan Fang Xinchao Wang∗

**发表刊物/会议：** NeurIPS 

**发表年份：** 2023

**论文地址：** https://arxiv.org/abs/2305.11627

**代码地址：** https://github.com/horseee/LLM-Pruner





## 内容概要

这篇文章介绍了一种名为LLM-Pruner的新型结构化剪枝方法，用于压缩大型语言模型（LLMs）。LLM-Pruner旨在以任务无关的方式压缩LLMs，同时最小化对原始训练数据集的依赖，并保留LLMs的多任务解决和语言生成能力。文章提出了一种依赖检测算法，用于识别模型中的所有依赖结构，并在任务无关设置下选择最佳剪枝组。然后，通过快速恢复阶段对剪枝后的模型进行后训练，使用有限的数据。

文章在三个LLMs（LLaMA-7B、Vicuna-7B和ChatGLM-6B）上验证了LLM-Pruner的有效性，并展示了压缩后的模型在零样本分类和生成方面仍具有令人满意的能力。实验结果表明，即使删除了20%的参数，剪枝后的模型仍保持了原始模型94.97%的性能。

## 主要解决问题/应用



## 主要使用方法/模型




## 主要实验手段/数据集



## 创造性思考



## 批判式思考


## 讨论 


- 怎么裁剪？大模型的裁剪和其他模型的裁剪有何区别？
  
- 怎么保证裁剪后的模型在较小的数据集上微调性能提升？

- 恢复的时候P和Q指的是什么？
  
