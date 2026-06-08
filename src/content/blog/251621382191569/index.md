---
title: '机器学习'
description: '机器学习的一些笔记...'
publishDate: '2026-06-08 19:37:34'
tags:
  - 机器学习
heroImage: { src: './thumbnail.png', alt: 'an image targeting my article', color: '#8BFFAE' }
---

# <span style="color:#666600">机器学习</span>

赋予计算机学习的能力

## <span style="color:#9999ff">常用术语</span>
<a id="table"></a>
**示例表格：**

| id | sepal length 花萼长度 (cm) | sepal width 花萼宽度 (cm) | petal length 花瓣长度 (cm) | petal width 花瓣宽度 (cm) | label（鸢尾花种类） |
| :-: | :-: | :-: | :-: | :-: | :-: |
| 1 | 5.1 | 3.5 | 1.4 | 0.2 | setosa |
| 2 | 4.9 | 3.0 | 1.4 | 0.2 | setosa |
| 3 | 7.0 | 3.2 | 4.7 | 1.4 | versicolor |
| 4 | 6.4 | 3.2 | 4.5 | 1.5 | versicolor |
| 5 | 6.3 | 3.3 | 6.0 | 2.5 | virginica |
| 6 | 5.8 | 2.7 | 5.1 | 1.9 | virginica |

### 样本

一行数据就是一个样本，多个样本组成***数据集***

### 特征/属性（x_*）

一列数据一个特征，如表格中有四个特征，分别是花萼长宽和花瓣长宽

### 标签/目标（y_*）

模型要预测的那一列数据(特征)，也就是表格中的label标签，即鸢尾花种类

### 训练集（*_train）

用来训练模型的数据集

### 测试集（*_test）

用来测试模型的数据集

> 我们可以把编号（1-4）的数据作为训练集，编号（5-6）作为测试集，把训练集的特征(x_train)与标签(y_train)放入模型训练；训练完毕后，把测试集的特征(x_test)放入模型预测出标签(y_test),接着可以比对原来的标签(模型评估)

## <span style="color:#9999ff">机器学习算法分类</span>

### <span style="color:#99ccff">有监督学习</span>

训练集的数据是有特征，有标签的，如[表格](#table)的数据

#### 分类问题

标签是不连续，是分类的，如[表格](#table)的数据

#### 回归问题

目标值(标签)是连续的，如下表格，price是连续的

| id | area | bedrooms | bathrooms | age | distance_to_city | price |
| :-: | :-: | :-: | :-: | :-: | :-: |:-: |
| 1 | 120 | 3 | 2 | 5 | 3.2 | 350 |
| 2 | 80 | 2 | 1 | 15 | 8.5 | 160 |
| 3 | 150 | 4 | 2 | 1 | 1.8 | 520 |
| 4 | 95 | 3 | 1 | 10 | 6.0 | 210 |
| 5 | 200 | 5 | 3 | 3 | 2.5 | 680 |
| 6 | 60 | 1 | 1 | 20 | 12.0 | 105 |

### <span style="color:#99ccff">无监督学习</span>

训练的数据有特征，没有标签

### <span style="color:#99ccff">半监督学习</span>

1. 让专家标注少量数据，利用已经标记的数据（即带有标签）训练出一个模型。
2. 利用训练好的模型去套用未标记的数据
3. 通过询问领域专家分类结果与模型分类做结果对比

## <span style="color:#9999ff">机器学习建模流程</span>

### <span style="color:#99ccff">获取数据</span>

获取经验数据，包括图像数据，文本数据...可以利用已有的官方或三方的数据集

### <span style="color:#99ccff">数据基本处理</span>

处理缺失/异常数据

### <span style="color:#99ccff">特征工程</span>

利用**专业**知识处理数据，让机器学习算法效果最好

#### * 特征提取

提取原始数据中与任务（标签）相关的特征，构成特征向量

#### * 特征预处理

处理量纲（单位）问题

##### 归一化

通过数据变换把数据映射到【mi,mx】(默认[0,1])之间
$$
x\prime=\frac{x-min}{max-min}
$$

$$
x\prime\prime=x\prime*(mx-mi)+mi
$$

**示例**

```py
from sklearn.preprocessing import MinMaxScaler #归一化对象

#训练数据
x_train = [[90,2,10,40], [60,4,15,45], [75,3,13,46]]

# 创建归一化对象
scaler = MinMaxScaler()

# 归一化数据
print(scaler.fit_transform(x_train))

```

**输出**

```shell
[[1.         0.         0.         0.        ]
 [0.         1.         1.         0.83333333]
 [0.5        0.5        0.6        1.        ]]
```



##### 标准化

通过对原始数据进行标准化，转化为均值**mean**为0标准差**σ**为1的标准正太分布的数据。
$$
x\prime=\frac{x-mean}{σ}
$$
**示例**

```py
from sklearn.preprocessing import StandardScaler #标准化对象

#训练数据
x_train = [[90,2,10,40], [60,4,15,45], [75,3,13,46]]

# 创建标准化对象
scaler = StandardScaler()

# 标准化数据
print(scaler.fit_transform(x_train))


```

**输出**

```shell
[[ 1.22474487 -1.22474487 -1.29777137 -1.3970014 ]
 [-1.22474487  1.22474487  1.13554995  0.50800051]
 [ 0.          0.          0.16222142  0.88900089]]
```



#### * 特征降维

将原始数据降维

#### * 特征选择

选取与任务直接相关的特征集合

#### * 特征组合

把多个特征合成一个特征

### <span style="color:#99ccff">机器学习（模型训练）</span>

#### * KNN算法(k近邻)

**描述：**  [KNN](#knn)，基于距离度量，找出离待测样本最近的 K 个邻居，通过投票（分类）或平均（回归）决定结果。

**解决问题：** 小规模、低维度的分类与回归，无需训练过程。

**优点：** 简单直观，无需训练，无假设前提，易实现。
**缺点：** 计算量大，内存消耗高，对高维数据效果差，对异常值敏感。

#### * 线性回归

**描述：** 拟合特征与目标之间的线性关系 y=wx+b，最小化均方误差求解权重。

**解决问题：** 预测连续数值，如房价、气温、销售额等。

**优点：** 可解释性强，训练快，有解析解，不易过拟合（特征少时）。
**缺点：** 仅能表达线性关系，对异常值敏感，需特征间独立。

#### * 逻辑回归

**描述：** 在线性回归基础上套一层 Sigmoid 函数，将输出映射到 (0,1) 区间，用于概率估计。

**解决问题：** 二分类问题（可扩展到多分类），如垃圾邮件识别、疾病预测。

**优点：** 输出概率值，可解释性强，训练快，正则化防过拟合。
**缺点：** 本质线性分类器，难以处理非线性边界，对多重共线性敏感。

#### * 决策树

**描述：** 通过递归分裂节点构建树结构，每次选择最优特征划分，直至叶子节点给出预测。

**解决问题：** 分类与回归均可，尤其适合需要可解释规则的场景。

**优点：** 无需归一化，可处理缺失值，可解释性强，天然支持非线性。
**缺点：** 易过拟合，不稳定（微小变化改变树结构），偏向多值特征。

#### * 集成学习

**描述：** 组合多个弱学习器形成强学习器，主要分为 Bagging（并行，如随机森林）和 Boosting（串行，如 XGBoost）。

**解决问题：** 单模型精度不足或过拟合风险高时的分类与回归任务。

**优点：** 精度高，泛化能力强，降低过拟合，Kaggle 竞赛常胜方案。
**缺点：** 计算成本高，可解释性差，参数量大，调参复杂。

#### * K-Means(K 均值)

**描述：** 将数据迭代分配到 K 个聚类中心，最小化簇内距离平方和，直至中心不再变化。

**解决问题：** 无标签数据的聚类分析，如用户分群、图像压缩、异常检测。

**优点：** 简单高效，可扩展性好，适合球形分布数据。
**缺点：** 需预设 K 值，对初始中心敏感，对非球形数据效果差，受异常值影响。

### <span style="color:#99ccff">模型评估</span>



1. 基于训练集的特征和标签，进行重新预测评分

2. 基于测试集的特征和标签，进行重新预测评分

## <span style="color:#9999ff">模型拟合</span>
<img src="https://img.remit.ee/api/file/BQACAgUAAyEGAASHRsPbAAEVMPxqJqyfASdQqQj-Bty0_ShXuNrIwQACrjMAApLWMVWAMwTJWnklXzsE.png" alt="拟合曲线"
style="height:500px">

### 拟合

模型在**训练集**和**测试集**表现都**好**

### 欠拟合

模型在**训练集**和**测试集**表现都**不好**

### 过拟合

模型在**训练集**表现**好**但**测试集**表现**不好**

## <span style="color:#9999ff">机械学习库（python-scikit-learn）</span>

```shell
pip install sklearn
```

<a id="knn"></a>

## <span style="color:#9999ff">KNN算法</span>

k-近邻算法（K Nearest Neighbor），一个样本在特征空间中的k个最相似样本（[欧式距离](#Euc-Dis)）

### <span style="color:#99ccff">分类问题</span>

取最近k个样本，进行多数表决

#### 示例代码

```py
from sklearn.neighbors import KNeighborsClassifier 

# 数据
x_train = [[0], [1], [2], [3]]
y_train = [0, 0, 1, 1]
x_test = [[5]]

# 分类模型
knn = KNeighborsClassifier(n_neighbors=2)

# 训练
knn.fit(x_train, y_train)

# 预测
y_pre = knn.predict(x_test)

print(f'预测值为{y_pre}')
```

#### 输出

```shell
预测值为[1]
```



### <span style="color:#99ccff">回归问题</span>

取最近k个样本，计算其平均值

#### 示例代码

```py
from sklearn.neighbors import KNeighborsRegressor

x_test2=[[1.5]]

# 回归模型
knn2 = KNeighborsRegressor(n_neighbors=2)

# 训练
knn2.fit(x_train, y_train)

# 预测
y_pre2 = knn2.predict(x_test2)

print(f'预测值为{y_pre2}')
```

#### 输出

```shell
预测值为[0.5]
```

## <span style="color:#9999ff">距离度量</span>

<a id="Euc-Dis"></a>

 ### 欧式距离

n维度空间的点 **a(x<sub>11</sub>,x<sub>12</sub>..x<sub>1n</sub>)** 和 **b(x<sub>21</sub>,x<sub>22</sub>..x<sub>2n</sub>)** 的距离计算公式：

$$
d_{ab}=\sqrt[]{\sum_{k=1}^{n}(x_{1k}-x_{2k})^2}
$$

### 曼哈顿距离

n维度空间的点 **a(x<sub>11</sub>,x<sub>12</sub>..x<sub>1n</sub>)** 和 **b(x<sub>21</sub>,x<sub>22</sub>..x<sub>2n</sub>)** 的距离计算公式：
$$
d_{ab}=\sum_{k=1}^{n}|x_{1k}-x_{2k}|
$$

### 切比雪夫距离

n维度空间的点 **a(x<sub>11</sub>,x<sub>12</sub>..x<sub>1n</sub>)** 和 **b(x<sub>21</sub>,x<sub>22</sub>..x<sub>2n</sub>)** 的距离计算公式：
$$
d_{ab}=max(|x_{1k}-x_{2k}|)
$$

## <span style="color:#9999ff">超参数选择方法</span>

通过**交叉验证**和**网格搜索**组合形成一个模型调参的解决方案

### 交叉验证

将训练集划分n份，取其中一份为验证集，其他作为训练集。目的是为了得到更准确可信的模型。

### 网格搜索

是寻找最优超参数的工具！将若干参数传入网格搜索对象，自动帮我们完成不同参数的组合，模型训练与模型评估，最终返回最优的超参数。

### 示例

```py
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split, GridSearchCV
from sklearn.neighbors import KNeighborsClassifier
from sklearn.preprocessing import StandardScaler


iris_data = load_iris()
x_train, x_test, y_train, y_test = train_test_split(iris_data.data, iris_data.target, test_size=0.2, random_state=0)

# 创建标准化对象
scaler = StandardScaler()
# 训练数据 fit_ transform 计算出标准差和均值并转化
x_train = scaler.fit_transform(x_train)
# 测试数据 直接转化
x_test = scaler.transform(x_test)

# 创建分类模型
Classifier = KNeighborsClassifier()

# 超参数
param_dict = {'n_neighbors': [i for i in range(1,11)]}

# 创建网格搜索对象,cv=5是5折交叉验证
Classifier = GridSearchCV(Classifier, param_grid=param_dict, cv=5)
Classifier.fit(x_train, y_train)

print(f'最优评分：{Classifier.best_score_}')
print(f'最优参数：{Classifier.best_params_}')
print(f'最优模型：{Classifier.best_estimator_}')
print(f'测试集准确率：{Classifier.score(x_test, y_test)}')
print(f'预测结果：{Classifier.predict(x_test)}')
print(f'预测概率：{Classifier.predict_proba(x_test)}')
print(f'交叉验证结果：{Classifier.cv_results_}')
```










