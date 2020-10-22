# 【关于 Wide&Deep】那些你不知道的事

> 笔者：杨夕
>
> 项目地址：https://github.com/km1994/nlp_paper_study
> 
> 个人介绍：大佬们好，我叫杨夕，该项目主要是本人在研读顶会论文和复现经典论文过程中，所见、所思、所想、所闻，可能存在一些理解错误，希望大佬们多多指正。

## 整体框架图

![](img/微信图片_20201018180302.png)

## 动机

- 协同过滤和矩阵分解存在的劣势：仅利用了用户与物品相互行为信息进行推荐， 忽视了用户自身特征， 物品自身特征以及上下文信息等，导致生成的结果往往会比较片面

## 思路

- 该模型思路

1. 利用GBDT自动进行特征筛选和组合， 进而生成新的离散特征向量；
2. 再把该特征向量当做LR模型的输入， 来产生最后的预测结果；

- 优点：该模型能够综合利用用户、物品和上下文等多种不同的特征， 生成较为全面的推荐结果， 在CTR点击率预估场景下使用较为广泛。



## 逻辑回归模型

- vs 传统协同过滤：逻辑回归模型能够综合利用用户、物品、上下文等多种不同的特征生成较为“全面”的推荐结果。
- 构建方式：逻辑回归是在线性回归的基础上加了一个 Sigmoid 函数（非线形）映射，使得逻辑回归成为了一个优秀的分类算法， 学习逻辑回归模型。 
- 思路：逻辑回归假设数据服从伯努利分布,通过极大化似然函数的方法，运用梯度下降来求解参数，来达到将数据二分类的目的。
- vs 协同过滤和矩阵分解:
    - 协同过滤和矩阵分解：利用用户的物品“相似度”进行推荐;
    - 逻辑回归模型：将问题看成了一个分类问题， 通过预测正样本的概率对物品进行排序。
 
 ### 过程
 
 1. 将用户年龄、性别、物品属性、物品描述、当前时间、当前地点等特征转成数值型向量
 2. 确定逻辑回归的优化目标，比如把点击率预测转换成二分类问题， 这样就可以得到分类问题常用的损失作为目标， 训练模型
 3. 在预测的时候， 将特征向量输入模型产生预测， 得到用户“点击”物品的概率
 4. 利用点击概率对候选物品排序， 得到推荐列表
 
 ![](img/20201022155113.png)
 
 ## GBDT 模型


