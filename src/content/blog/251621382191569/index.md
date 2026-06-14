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

## <span style="color:#9999ff">机械学习库（python-scikit-learn）</span>

```shell
pip install sklearn
```

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

> 可以把编号（1-4）的数据作为训练集，编号（5-6）作为测试集，把训练集的特征(x_train)与标签(y_train)放入模型训练；训练完毕后，把测试集的特征(x_test)放入模型预测出标签(y_test),接着可以比对原来的标签(模型评估)

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

获取经验数据，包括图像数据，文本数据...

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

**描述：** [KNN算法](#knn)，基于距离度量，找出离待测样本最近的 K 个邻居，通过投票（分类）或平均（回归）决定结果。

**解决问题：** 小规模、低维度的分类与回归，无需训练过程。

**优点：** 简单直观，无需训练，无假设前提，易实现。
**缺点：** 计算量大，内存消耗高，对高维数据效果差，对异常值敏感。

#### * 线性回归

**描述：** [线性回归](#xxhg)，拟合特征与目标之间的线性关系 y=wx+b，最小化均方误差求解权重。

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

基于训练集/测试集的特征和标签，进行重新预测评分

## <span style="color:#9999ff">模型拟合</span>
<img src="https://i-blog.csdnimg.cn/direct/31fe17696bd8425d95393cfec1607219.png" alt="初音未来"
style="height:500px">

### <span style="color:#99ccff">拟合</span>

模型在**训练集**和**测试集**表现都**好**

#### 示例代码

```py
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error

#生成数据
np.random.seed(666)
x = np.random.uniform(-3.0,3.0,size=100)
y = 0.5 * x**2 + x + 3 + np.random.normal(0,1,size=100)

#创建模型
estimator = LinearRegression()
# 数据集的形状 [1,2,3]->[[1],[2],[3]]
X=x.reshape(-1,1)
# 数据集的形状 [[1],[2],[3]]->[[1,2],[2,4],[3,9]]
X2=np.hstack([X,X**2])
estimator.fit(X2,y)

#预测
y_predict = estimator.predict(X2)

#计算均方误差
myret = mean_squared_error(y,y_predict)
#print(f'均方误差{myret}')

plt.scatter(x,y)
# 对x排序，然后取x排序后的y值
plt.plot(np.sort(x),y_predict[np.argsort(x)],c='r')
plt.show()
```

### <span style="color:#99ccff">欠拟合</span>

模型过于简单，模型在**训练集**和**测试集**表现都**不好**

#### 示例代码

```py
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error

#生成数据
np.random.seed(666)
x = np.random.uniform(-3.0,3.0,size=100)
y = 0.5 * x**2 + x + 3 + np.random.normal(0,1,size=100)

#创建模型
estimator = LinearRegression()
# 数据集的形状 [1,2,3]->[[1],[2],[3]]
X=x.reshape(-1,1)
estimator.fit(X,y)

#预测
y_predict = estimator.predict(X)

#计算均方误差
myret = mean_squared_error(y,y_predict)
#print(f'均方误差{myret}')

plt.scatter(x,y)
plt.plot(x,y_predict,c='r')
plt.show()
```

#### 解决方案

增加模型复杂度（添加其他**特征**，添加**多项式特征**）

### <span style="color:#99ccff">过拟合</span>

模型在**训练集**表现**好**但**测试集**表现**不好**

#### 示例代码

```py
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error

#生成数据
np.random.seed(666)
x = np.random.uniform(-3.0,3.0,size=100)
y = 0.5 * x**2 + x + 3 + np.random.normal(0,1,size=100)

#创建模型
estimator = LinearRegression()
# 数据集的形状 [1,2,3]->[[1],[2],[3]]
X=x.reshape(-1,1)
# 数据增加高次项
X2=np.hstack([X,X**2,X**3,X**4,X**5,X**6,X**7,X**8,X**9,X**10])
estimator.fit(X2,y)

#预测
y_predict = estimator.predict(X2)

#计算均方误差
myret = mean_squared_error(y,y_predict)
#print(f'均方误差{myret}')

plt.scatter(x,y)
# 对x排序，然后取x排序后的y值
plt.plot(np.sort(x),y_predict[np.argsort(x)],c='r')
plt.show()
```

#### 解决方法

原始特征过多，存在一些嘈杂特征，模型过于复杂是因为模型尝试取兼顾各个测试数据点

* 重新清洗数据
* 增大数据量的训练量
* 正则化
* 减少维度特征

**正则化**

训练模型中，某些特征影响模型复杂度、或者某个特征的异常值较多，所有要尽可能减少这个特征值的影响，即调整该特征的**权重W**

##### L1正则化

**在损失函数中添加L1正则化项：**
$$
J(w)=MSE(w)+α\sum^{n}_{i=1}|w_i|
$$

* α：叫做惩罚系数，该值越大，对权重调整幅度越大，即惩罚力度越大

* L1 正则化会趋向于0，甚至等于0，使得某些特征失效，达到筛选的目的

**回归模型(Lass回归模型)**

```py
from sklearn.linear_model import Lasso
estimator = Lasso(alpha=0.1) #alpha惩罚系数
```

##### L2正则化

**在损失函数中添加L2正则化项：**
$$
J(w)=MSE(w)+α\sum^{n}_{i=1}|w_i^2|
$$

* L2正则化会趋向于0，一般不等于0

**回归模型(Lass回归模型)**

```py
from sklearn.linear_model import Ridge
estimator = Ridge(alpha=10) #alpha惩罚系数
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
<a id="xxhg"></a>
## <span style="color:#9999ff">线性回归</span>

利用回归方程(函数)对一个或多个自变量(特征值)和因变量(目标值)之间的关系

### <span style="color:#99ccff">数学公式</span>

#### 一元线性回归

即一个特征
$$
y=wx+b(weight(权重),bias(偏置))
$$

#### 多元线性回归

即多个特征
$$
y=W^TX+b(X=(x_1,x_2...)^T,W=(w_1,w_2...)^T)
$$

### <span style="color:#99ccff">损失函数</span>

衡量每个样本的**预测值**和**真实值**之间效果的函数，让损失函数最小，就是让误差和小，线性回归效率，评估就越高

#### 损失函数分类

##### 均方误差(Mean-Square Error,MSE)

每个样本的点的误差的平方和
$$
J(w,b) = \frac{1}{m}\sum^m_{i=0}(h(x_i)-y_i)^2
$$

##### 平均绝对误差(Mean Absolute Error,MAE)

每个样本点的误差绝对值和
$$
J(w,b) = \frac{1}{m}\sum^m_{i=0}|h(x_i)-y_i)|
$$

##### 均方根误差(Root Mean Squared Error,RMSE)

$$
J(w,b) = \sqrt{\frac{1}{m}\sum^m_{i=0}(h(x_i)-y_i)^2}
$$



### <span style="color:#99ccff">求解损失函数最小</span>

#### 正规方程法

通过一次计算，可以直接得出方程解，即权重W和偏置b，以一元线性回归为例

##### 回归损失函数:

$$
J(k,b) =\sum^m_{i=0}(h(x_i)-y_i)^2=\sum^m_{i=0}(kx_i+b-y_i)^2
$$
先对k求偏导
$$
①\frac{\partial J(k,b)}{\partial  k}=k\sum^m_{i=1}x_i^2+b\sum^m_{i=1}x_i-\sum^m_{i=1}x_iy_i
$$
再对b求偏导
$$
②\frac{\partial J(k,b)}{\partial b}=k\sum^m_{i=1}x_i+bm-\sum^m_{i=1}y_i
$$
将①式 和② 式联立方程，将x特征值带入，y标签值代入，求解二元一次方程权重k和偏置b。

##### 示例代码

```py
import pandas as pd
import numpy as np
from sklearn.linear_model import LinearRegression
from sklearn.metrics import root_mean_squared_error, mean_absolute_error, mean_squared_error
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler

#加载波士顿房价数据
data_url = "http://lib.stat.cmu.edu/datasets/boston"
raw_df = pd.read_csv(data_url,sep="\\s+",skiprows=22,header=None)
data = np.hstack([raw_df.values[::2,:],raw_df.values[1::2,:2]])
target = raw_df.values[1::2,2]

#print(f'特征值数据{ data[:5]}')
#print(f'标签数据{ target[:5]}')

#划分数据集
x_train, x_test, y_train, y_test = train_test_split(data,target,test_size=0.2,random_state=23)

#数据标准化
transfer = StandardScaler()
x_train = transfer.fit_transform(x_train)
x_test = transfer.transform(x_test)

#创建模型 正规方程模型对象
estimator = LinearRegression(fit_intercept= True) # 设置有截距项
estimator.fit(x_train,y_train)
# 打印权重和截距
print(f'参数{estimator.coef_}')
print(f'截距{estimator.intercept_}')

# 预测
y_predict = estimator.predict(x_test)
# print(f'预测结果{y_predict[:5]}')

#评估
print(f'均方误差{mean_squared_error(y_test,y_predict)}')
print(f'均方根误差{root_mean_squared_error(y_test,y_predict)}')
print(f'平均绝对误差{mean_absolute_error(y_test,y_predict)}')
```



#### 梯度下降算法

循环迭代求当前点的梯度，沿着梯度下降的方向求解极小值

##### 梯度

* 单变量函数中，梯度就是某一点切线的斜率（导数）
* 多变量函数中，梯度就是某一个点的偏导数

##### 梯度下降公式

$$
θ_{i+1}=θ_i-α\frac{\partial}{\partial θ_i}J(θ)
$$

α：学习率，不能太大也不能太小，一般在0.001~0.01

θ：权重w

**以多元线性回归均方差作为损失函数为例**
$$
\frac{\partial}{\partial θ_i}J(θ)=\frac{1}{m}\sum^m_{i=1}(h_θ(x_i)-y_i)x_i
$$
一般以正态分布（0，1）生成所有θ值为初始值，通过迭代不断优化θ取值

##### 梯度下降分类

* **全梯度下降算法 FGD(Ful Gradient Descent)**

  每次迭代使用全部样本求梯度值，有m个样本，求梯度时用了所有m个样本

* **随机梯度下降算法 SGD**

  每次迭代时，随机选择使用一个样本求梯度值

* **小批量下降算法 mini-batch**

  使用小批量样本求梯度值

* **随机平均梯度下降算法 SAG**

  随机选择一个样本的梯度值和以往样本的梯度值的均值

##### 示例代码

```py
import pandas as pd
import numpy as np
from sklearn.linear_model import SGDRegressor
from sklearn.metrics import root_mean_squared_error, mean_absolute_error, mean_squared_error
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler

#加载波士顿房价数据
data_url = "http://lib.stat.cmu.edu/datasets/boston"
raw_df = pd.read_csv(data_url,sep="\\s+",skiprows=22,header=None)
data = np.hstack([raw_df.values[::2,:],raw_df.values[1::2,:2]])
target = raw_df.values[1::2,2]

#print(f'特征值数据{ data[:5]}')
#print(f'标签数据{ target[:5]}')

#划分数据集
x_train, x_test, y_train, y_test = train_test_split(data,target,test_size=0.2,random_state=23)

#数据标准化
transfer = StandardScaler()
x_train = transfer.fit_transform(x_train)
x_test = transfer.transform(x_test)

#创建模型 随机梯度下降 线性回归模型对象
estimator = SGDRegressor(fit_intercept= True,learning_rate='constant',eta0=0.01) # 设置有截距项,学习率不改变,为0.01
estimator.fit(x_train,y_train)
# 打印权重和截距
print(f'参数{estimator.coef_}')
print(f'截距{estimator.intercept_}')

# 预测
y_predict = estimator.predict(x_test)
# print(f'预测结果{y_predict[:5]}')

#评估
print(f'均方误差{mean_squared_error(y_test,y_predict)}')
print(f'均方根误差{root_mean_squared_error(y_test,y_predict)}')
print(f'平均绝对误差{mean_absolute_error(y_test,y_predict)}')
```



