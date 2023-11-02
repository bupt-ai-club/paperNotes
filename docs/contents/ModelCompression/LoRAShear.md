# LoRAShear: Efficient Large Language Model Structured Pruning and Knowledge Recovery


**作者** Tianyi Chen  Tianyu Ding  Badal Yadav  Ilya Zharkov  Luming Liang 

**发表刊物/会议：**

**发表年份：**

**论文地址：**

**代码地址：**

## 内容概要

这篇论文提出了一种名为LoRAShear的新颖方法，用于在有限资源条件下对大型语言模型（LLMs）进行高效结构化剪枝和知识恢复。LoRAShear具有以下三个主要特点：

1. 自动发现LLMs与LoRA模块中的最小可移除结构。
2. 通过一种名为LoRA Half-Space Projected Gradient（LHSPG）的新型结构稀疏优化器进行渐进式结构化剪枝，利用LoRA模块中存储的信息在原始变量上产生结构稀疏。
3. 配备动态知识恢复阶段，以便从预训练和有指导的微调数据集恢复知识。
   
实验结果表明，LoRAShear在20%的剪枝比例下，性能仅下降1%，而在50%的剪枝比例下，性能保持在82%。这表明LoRAShear在剪枝和知识恢复方面具有显著优势。


## 主要解决问题/应用



## 主要使用方法/模型



## 主要实验手段/数据集



## 创造性思考



## 批判式思考


## 讨论 







