# 卷积神经网络——从计算机视觉到自然语言处理
## 什么是卷积神经网络

### 首先明白卷积运算。CNNS 本质上就是多层卷积运算，外加对每层的输出用非线性激活函数转换。

### 前馈神经网络到卷积神经网络
传统前馈神经网络中，每个输入神经元与下一层的输出神经元相连接。（又叫作全连接层/仿射层）

CNNs中，用输入层的卷积结果来计算输出，这相当于是局部连接，每块局部的输入区域与输出的一个神经元相连接。
对每一层应用不同的滤波器，往往是成百上千个，然后汇总结果。（这里涉及到池化层降采样）

### CNN 模型自动学习滤波器的权重值。
举个例子：在图像分类问题中，第一层模型或许能学会从原始像素点检测到一些边缘线条，
然后根据线条在第二层检测出一些简单形状，然后基于这些形状检测出更高级的特征，比如脸部轮廓。
最后一层是利用这些高级特征的一个分类器。

## 这种计算方式有两点值得注意：** 位置不变性 ** 和 ** 组合性 **
### 位置不变性
比如，想对图片中是否包含大象做分类。因为滤波器实在全图范围内平移，所以不用关心图片大象在什么位置。
事实上，池化也有助于平移、旋转和缩放的不变性，它对克服缩因素的效果特别好。

### 第二个关键因素是局部组合性。
每个滤波器对一小块局部区域的低级特征组合成更高级的特征表示。这也是CNNs对计算机视觉作用巨大的原因。
我们可以很直观地理解，线条由像素点构成，基本形状又由线条构成，更复杂的物体又源自于基本的形状

## 那么如何将其运用于NLP呢？
### NLP的输入不再是像素点，大多数情况下是以矩阵表示的句子或者文档。
矩阵的每一行对应于一个个分词元素：一个单词或者是一个字符
每一行是表示一个单词的向量。通常这些向量都是 `word embeddings`的形式（一种低维度的表示）
但也可以是`one-hot`（独热码）向量的形式，也即根据词在词表中的索引（误？）
若是用100维的词向量表示一句10个单词的句子，我们将得到一个10x100维的矩阵作为输入。这个矩阵相当于一幅图像。
