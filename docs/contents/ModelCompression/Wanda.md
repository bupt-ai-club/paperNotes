# A Simple and Effective Pruning Approach for Large Language Models

**作者：** Mingjie Sun, Zhuang Liu, Anna Bair, J. Zico Kolter

**发表刊物/会议：** arXiv

**发表年份：** 2023

**论文地址：** https://arxiv.org/abs/2306.11695

**代码地址：** https://github.com/locuslab/wanda

## 内容概要


这篇论文介绍了一种名为Wanda的新型剪枝方法，专门针对大型语言模型（LLMs）。Wanda方法通过在每个输出的基础上，根据权重的幅度和相应的输入激活值来剪除最小的权重，从而在不重新训练模型的情况下实现模型的稀疏化。这种方法不需要权重更新，并且能够在单个前向传递中快速执行，具有较低的内存开销。

## 主要解决问题/应用

 这篇论文主要解决了大型语言模型（LLMs）的压缩问题，特别是在不牺牲模型性能的前提下，如何有效地减少模型的参数数量和计算资源消耗。

## 主要使用方法/模型

 Wanda（Pruning by Weights and activations）方法是一种针对大型语言模型（LLMs）的剪枝技术，其主要特点和使用方法如下：

1. **剪枝度量**：Wanda提出了一种新的剪枝度量，它结合了权重的幅度（magnitude）和输入激活的ℓ2范数（norm）。对于每个权重，其重要性得分由权重的幅度和输入激活的ℓ2范数的乘积计算得出。这种方法能够考虑到输入激活的动态范围，从而更准确地评估权重的重要性。

2. **剪枝策略**：Wanda在每个输出神经元上进行局部比较，而不是在整个层上进行比较。这意味着对于每个输出神经元，它只考虑连接到该神经元的权重，并根据它们的得分进行剪枝。这种方法在LLMs上特别有效，因为它能够更好地平衡不同输出特征的剪枝比例。

3. **无需权重更新**：与一些需要迭代权重更新的剪枝方法不同，Wanda不需要对剪枝后的网络进行任何权重更新。这意味着剪枝后的模型可以直接使用，无需进一步的调整。

4. **单次前向传递**：Wanda可以在单个前向传递中完成剪枝，这使得它在计算上非常高效，尤其适合实时剪枝的场景。


## 主要实验手段/数据集

 在这篇论文中，Wanda方法的实验手段和使用的数据集主要包括以下几个方面：

1. **模型系列**：实验主要在两个广泛采用的大型语言模型系列上进行，即LLaMA（7B/13B/30B/65B）和LLaMA-2（7B/13B/70B）。这些模型系列代表了不同规模的LLMs，用于评估Wanda方法在不同大小模型上的效果。

2. **语言任务**：为了评估剪枝后模型的性能，使用了多种语言任务，包括零样本任务和语言建模任务。零样本任务包括从EleutherAI LM Harness（Gao et al., 2021）中选取的七个任务，用于评估模型在没有额外训练的情况下的性能。语言建模任务则通过在WikiText验证集（Merity et al., 2016）上的困惑度（perplexity）来衡量。

3. **剪枝配置**：实验中考虑了不同的剪枝配置，包括无结构剪枝、结构化4:8和2:4剪枝。这些配置允许研究者评估在不同稀疏度下Wanda方法的表现。

4. **剪枝速度和推理速度**：为了评估Wanda方法的效率，论文还测量了在NVIDIA A6000 GPU上计算剪枝度量的时间，以及在剪枝后的模型上进行矩阵乘法的推理速度。这些实验有助于理解Wanda方法在实际应用中的性能。

5. **对比实验**：为了展示Wanda方法的优势，论文还与现有的剪枝方法进行了对比，包括基于幅度的剪枝（Magnitude Pruning）和SparseGPT。这些对比实验有助于理解Wanda方法在不同条件下的相对性能。

6. **数据集**：实验中使用的数据集包括用于模型训练的原始数据集，以及用于评估剪枝效果的验证集。这些数据集的选择对于确保实验结果的可靠性和泛化能力至关重要。

7. **随机种子的鲁棒性分析**：为了评估Wanda方法对随机种子变化的鲁棒性，论文在不同的随机种子下进行了实验，并报告了结果的均值和标准差。


## 创造性思考

 Wanda方法的提出展示了在大型语言模型剪枝领域的创造性思考。以下是一些关键的创新点：

1. **权重与激活的结合**：Wanda方法创新性地结合了权重的幅度和输入激活的ℓ2范数来评估权重的重要性。这种方法考虑到了输入激活的动态范围，这对于理解权重在模型输出中的实际影响至关重要，尤其是在大型语言模型中，输入特征的尺度可能存在显著差异。

2. **局部剪枝策略**：Wanda采用了一种局部剪枝策略，即在每个输出神经元的连接权重中进行剪枝。这种方法与传统的全局或层级剪枝策略不同，它允许模型在保持整体性能的同时，对每个输出特征进行更精细的剪枝。

3. **无需权重更新**：Wanda方法的一个显著特点是它不需要对剪枝后的模型进行权重更新。这与传统的剪枝方法形成对比，后者通常需要通过迭代过程来调整剩余权重，以保持模型性能。Wanda的这一特性使得剪枝过程更加高效，且易于集成到现有的模型训练流程中。

4. **计算效率**：Wanda方法能够在单个前向传递中完成剪枝，这大大减少了计算复杂度和时间开销。这种高效性使得Wanda方法特别适合于实时剪枝场景，如在线服务和资源受限的环境。

5. **模型泛化**：Wanda方法不仅在LLaMA和LLaMA-2模型上表现良好，而且在其他大型语言模型上也显示出了泛化能力。这表明Wanda的方法可能适用于多种类型的LLMs，具有广泛的应用潜力。

6. **稀疏训练的潜在应用**：论文还提出了Wanda方法在稀疏训练环境中的潜在应用，这为未来研究提供了新的方向，特别是在需要频繁剪枝和调整模型结构的场景中。



## 批判式思考

泛化性：虽然Wanda在LLaMA和LLaMA-2模型上表现出色，但其在其他类型的大型语言模型或不同领域任务上的泛化能力尚未充分验证。未来的研究需要在更广泛的模型和任务上评估Wanda的有效性。

## 讨论 

### 该算法在代码里具体是怎么实现的？


```python
# W: 权重矩阵，形状为 (C_out, C_in)，其中 C_out 是输出通道数，C_in 是输入通道数。
# X: 输入矩阵，形状为 (N * L, C_in)，其中 N * L 是样本总数，C_in 是输入通道数。
# s: 期望的稀疏度，是一个介于 0 和 1 之间的值，表示权重矩阵中将被置零的元素的比例。
def prune(W, X, s):  # 定义一个名为 prune 的函数，接受权重矩阵 W，输入矩阵 X 和稀疏度 s 作为输入。
    metric = W.abs() * X.norm(p=2, dim=0)  # 计算重要性度量矩阵，W 中的元素取绝对值后与 X 矩阵的 L2 范数（按列计算）相乘。
    _, sorted_idx = torch.sort(metric, dim=1)  # 对重要性度量矩阵按行进行排序，保留排序后的索引。
    pruned_idx = sorted_idx[:, :int(C_in * s)]  # 根据排序结果，选择每行中重要性最低（即值最小）的前 C_in * s 个索引。
    W.scatter_(dim=1, index=pruned_idx, src=0)  # 使用这些索引，在 W 的相应位置上填充 0，实现稀疏化。
    return W  # 返回稀疏化后的权重矩阵 W。

```



