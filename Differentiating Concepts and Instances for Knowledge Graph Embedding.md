# Differentiating Concepts and Instances for Knowledge Graph Embedding

## 摘要

大多数传统知识嵌入方法将实体（概念和实例）和关系编码为低维语义空间中的向量，同样忽略了概念和实例之间的差异。在本文中，我们通过区分概念和实例提出了一种名为TransC的新型知识图嵌入模型。具体而言，TransC将知识图中的每个概念编码为一个球体，将每个实例编码为同一语义空间中的一个矢量

## 介绍

以往的方法都忽略了区分概念和实例，并将两者都视为实现简化的实体。因此，以前工作将导致以下两个缺点：

+ 缺乏有效的概念表示
+ 缺乏传递性

为了解决这些问题，文中提出了一种名为TransC的新型翻译嵌入模型。在TransC中，每个概念被编码为球体，并且每个实例被编码为同一语义空间中的向量，并且相对位置被用于对概念和实例之间的关系进行建模。更具体地说，instanceOf关系自然地通过检查实例向量是否在概念领域内来表示。

## 相关工作

+ Translation-based Model： TransE TransH TransR/CTransR TransD  其他
+  Bilinear Model  ： RESCAL DisMult HolE ComplEx

+ External Information Learning Model : TEKE DKRL 

## 问题

$$ Kg= \{ C,I,R,S\} $$

 C和I分别表示概念和实例集。关系集R可以形式化为 $$ R= \{ r_e,r_c\}  \bigcup R_l $$,其中 $$r_e$$是instanceOf关系。$$r_e$$ 是subClassOf关系。$$R_l$$是实例关系集，因此三组$$S$$ 可以分为三个不相交的子集。

![1564037461438](C:\Users\99597\AppData\Roaming\Typora\typora-user-images\1564037461438.png)



对于每个概念$$ c \in C$$  学习 $$ s(p,m)$$球体  p是中心 m是半径

instanceOf-subClassOf transitivity

![1564037680783](C:\Users\99597\AppData\Roaming\Typora\typora-user-images\1564037680783.png)

 subClassOf-subClassOf transitivity 

![1564037703549](C:\Users\99597\AppData\Roaming\Typora\typora-user-images\1564037703549.png)



## 方法

S中有三种三元组，分别为它们定义不同的损失函数

+ 实例

![1564037815564](C:\Users\99597\AppData\Roaming\Typora\typora-user-images\1564037815564.png)

+ 子类   四种情况

+ ![1564038043866](C:\Users\99597\AppData\Roaming\Typora\typora-user-images\1564038043866.png)

  ![1564037983910](C:\Users\99597\AppData\Roaming\Typora\typora-user-images\1564037983910.png)

  ![1564037993370](C:\Users\99597\AppData\Roaming\Typora\typora-user-images\1564037993370.png)

  ![1564038002459](C:\Users\99597\AppData\Roaming\Typora\typora-user-images\1564038002459.png)

  ![1564038009085](C:\Users\99597\AppData\Roaming\Typora\typora-user-images\1564038009085.png)

+ 关系 

  ![1564038025710](C:\Users\99597\AppData\Roaming\Typora\typora-user-images\1564038025710.png)







### 训练

![1564038118619](C:\Users\99597\AppData\Roaming\Typora\typora-user-images\1564038118619.png)



## 实验

数据集  

以前的大多数工作都使用FB15K和WN18（Bordes等，2013）进行评估。但是这两个数据集不适合我们的模型，因为FB15K主要由实例组成，WN18主要包含概念。因此，我们使用另一个流行的知识图YAGO（Suchanek等，2007）进行评估，其中包含来自WordNet的许多概念和来自维基百科的实例。



![1564038563742](C:\Users\99597\AppData\Roaming\Typora\typora-user-images\1564038563742.png)



![1564038881494](C:\Users\99597\AppData\Roaming\Typora\typora-user-images\1564038881494.png)



### 链路预测

![1564039013351](C:\Users\99597\AppData\Roaming\Typora\typora-user-images\1564039013351.png)



### 元组分类



![1564039033413](C:\Users\99597\AppData\Roaming\Typora\typora-user-images\1564039033413.png)

## 未来的工作

（1）球体是一个在语义空间中表示概念的简单模型，但由于它过于幼稚，它仍然有一些限制。我们将尝试找到一个更具表现力的模型而不是球体来表示概念。 （2）概念在不同的三元组中可能有不同的含义。我们将尝试使用几个典型的实例向量作为概念的中心来表示概念的不同含义