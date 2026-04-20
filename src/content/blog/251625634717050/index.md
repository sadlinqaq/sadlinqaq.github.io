---
title: 'markdown基础教程'
description: '一些markdown常用的基本语法,帮助快速定位并解决问题..'
publishDate: '2026-04-10 12:11:29'
tags:
  - markdown
  - markdown语法
heroImage: { src: './thumbnail.png', alt: 'an image targeting my article', color: '#7fa8de' }
---

### 前言
建议直接看[速查表](https://markdown.com.cn/cheat-sheet.html#%E6%80%BB%E8%A7%88)

### 普通文本
直接写内容即可
```md
这里是内容abc
```
##### <span style="color:red">文本呈现效果:</span>
这里是内容abc

---
### 高亮
```md
这里是==内容==abc
```
##### <span style="color:red">文本呈现效果:</span>
这里是==内容==abc

---
### 加粗文本
```md
**这里是内容abc**
__这里是内容abc__
```
##### <span style="color:red">文本呈现效果:</span>
**这里是内容abc**

---
如果希望部分内容加粗
```md
这里是**内容**abc
这里是 __内容__ abc
<!-- 注意下划线要空一格 -->
```
##### <span style="color:red">文本呈现效果:</span>
这里是**内容**abc
这里是 __内容__ abc

---
### 斜体
下划线要空格
```md
这里是*内容*abc
这里是 _内容_ abc
```
##### <span style="color:red">文本呈现效果:</span>
这里是*内容*abc
这里是 _内容_ abc

---
### 斜体加粗共用
```md
这里是***内容***abc
这里是 ___内容___ abc
```
##### <span style="color:red">文本呈现效果:</span>
这里是***内容***abc
这里是 ___内容___ abc

---
### 删除线
```md
这里是~~内容~~abc
```
##### <span style="color:red">文本呈现效果:</span>
这里是~~内容~~abc

---
### 分割线
三个或以上都可以
```md
---
****
_____
```
##### <span style="color:red">文本呈现效果:</span>
⬇分割线效果(顺带分割一下内容)⬇

---
### 标题
```md
一级标题
=
二级标题
-
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```

##### <span style="color:red">文本呈现效果:</span>
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题

---
### 无序列表
注意符号不能混用
```md
* 第一项
* 第二项
+ 第一项
+ 第二项
- 第一项
- 第二项 
```

##### <span style="color:red">文本呈现效果:</span>
* 第一项
* 第二项

---
### 有序列表
```md
至少空三格空格
1. 一级列表第一项
   1. 二级列表第一项
   2. 二级列表第二项
      1. 三级列表第一项
2. 一级列表第二项
```

##### <span style="color:red">文本呈现效果:</span>
1. 一级列表第一项
   1. 二级列表第一项
   2. 二级列表第二项
      1. 三级列表第一项
2. 一级列表第二项
  
---
### 勾选框
```md
* [ ] 第一项任务
* [x] 第二项任务
* [ ] 第三项任务
```

##### <span style="color:red">文本呈现效果:</span>
* [ ] 第一项任务
* [x] 第二项任务
* [ ] 第三项任务

---
### 代码块
<span style="color:green">{data-source-line="151"}</span>这段<span style="color:red">删掉</span>

    ```java
    // ⬆对应的语言可替换
    public class Test {
        public static void main(String[] args) {
            System.out.println("hello world");
        }
    }
    ```


##### <span style="color:red">文本呈现效果:</span>
```java
public class Test {
    public static void main(String[] args) {
        System.out.println("hello world");
    }
}
```

### 部分代码块
```md
用`equals()`方法比较两字符串对象
```

##### <span style="color:red">文本呈现效果:</span>
用`equals()`方法比较两字符串对象

---
### 引用文本
<span style="color:green">{data-source-line="151"}</span>这段<span style="color:red">删掉</span>
```md
> 第一行
> 第二行
>
> 第三行
> * 第四行
> * 第五行
> ```c
> int main(){
>  return 0;
>}//可以嵌套
> ```
```

##### <span style="color:red">文本呈现效果:</span>
> 第一行
> 第二行
>
> 第三行
> * 第四行
> * 第五行
> ```c
> int main(){
>  return 0;
>}//可以嵌套
> ```

---
### 超链接

```md
www.baidu.com
[百度](https://www.baidu.com)官网

[百度][a]官网

[a]: https://www.baidu.com
```

##### <span style="color:red">文本呈现效果:</span>
www.baidu.com
[百度](https://www.baidu.com)官网

---
### 脚注
```md
脚注1[^1],脚注2[^aa]

[^1]: 这是脚注1
[^aa]: 这是脚注2
```

##### <span style="color:red">文本呈现效果:</span>
脚注1[^1],脚注2[^aa]

[^1]: 这是脚注1
[^aa]: 这是脚注2

---
### 图片插入
```md
<!-- 图片名字可以省略 -->
 ![初音未来](https://web-uni-oss.oss-cn-hangzhou.aliyuncs.com/blog/img/%E3%80%90%E5%93%B2%E9%A3%8E%E5%A3%81%E7%BA%B8%E3%80%91%E5%88%9D%E9%9F%B3%E6%9C%AA%E6%9D%A5-%E5%8A%A8%E6%BC%AB%E8%A7%92%E8%89%B2.png)
```

##### <span style="color:red">文本呈现效果:</span>
 ![初音未来](https://web-uni-oss.oss-cn-hangzhou.aliyuncs.com/blog/img/%E3%80%90%E5%93%B2%E9%A3%8E%E5%A3%81%E7%BA%B8%E3%80%91%E5%88%9D%E9%9F%B3%E6%9C%AA%E6%9D%A5-%E5%8A%A8%E6%BC%AB%E8%A7%92%E8%89%B2.png)

---
### 嵌入自定义html内容
```md
<img src="https://web-uni-oss.oss-cn-hangzhou.aliyuncs.com/blog/img/%E3%80%90%E5%93%B2%E9%A3%8E%E5%A3%81%E7%BA%B8%E3%80%91%E5%88%9D%E9%9F%B3%E6%9C%AA%E6%9D%A5-%E5%8A%A8%E6%BC%AB%E8%A7%92%E8%89%B2.png" alt="初音未来"
style="height:200px">
```

##### <span style="color:red">文本呈现效果:</span>
<img src="https://web-uni-oss.oss-cn-hangzhou.aliyuncs.com/blog/img/%E3%80%90%E5%93%B2%E9%A3%8E%E5%A3%81%E7%BA%B8%E3%80%91%E5%88%9D%E9%9F%B3%E6%9C%AA%E6%9D%A5-%E5%8A%A8%E6%BC%AB%E8%A7%92%E8%89%B2.png" alt="初音未来"
style="height:200px">

---
### 表格
 注意第二行的冒号在哪边，往哪边对齐，冒号包裹为居中
```md
 |姓名|年龄|性别|
 |---:|:---|:---:|
 |xiaomin|133|man|
 |lihua|18|woman|
```

##### <span style="color:red">文本呈现效果:</span>
|姓名|年龄|性别|
|---:|:---|:---:|
|xiaomin|133|man|
|lihua|18|woman|

---
### Emoji
可以从[Emojipedia](https://emojipedia.org/)复制
也可以使用[表情符号简码列表](https://gist.github.com/rxaviers/7360908)
```md
去露营了！ :tent: 很快回来。
真好笑！ :joy:
```
##### <span style="color:red">文本呈现效果:</span>
去露营了！ :tent: 很快回来。
真好笑！ :joy:



---
### 数学公式
##### 1. 上标
```md
x^2^
```
##### <span style="color:red">文本呈现效果:</span>
x^2^

##### 2. 下标
```md
O~2~
```
##### <span style="color:red">文本呈现效果:</span>
O~2~

##### 3.数学公式符号($包裹)
```md
$X=1+y$

$$
x^2  \\
x_2  \\
C_3^1  \\
\frac{x}{y} 分号\\
\sqrt[3]{4} 根号\\
\not= 不等于\\
\approx 约等于\\
\leq 小于等于\\
\geq 大于等于\\
\times 乘号\\
\div 除号\\
\pm 正负号\\
\sum_{i=1}^{10} 求和\\
\prod_{i=1}^{10} 累乘\\
\coprod_{i=1}^{10} 累除\\
90^\circ 度数\\
\sin\pi 三角函数 \\
\cos\pi \\
\tan\pi \\
\infty 无穷\\
\int 定积分\\
\iint双重积分\\
y\prime 求导\\
\lim 极限\\
\emptyset 空集\\
\in 属于\\
\notin 不属于\\
\supset 包含\\
\supseteqq 真包含\\
$$
```
##### <span style="color:red">文本呈现效果:</span>
$X=1+y$

$$
x^2  \\
x_2  \\
C_3^1  \\
\frac{x}{y} 分号\\
\sqrt[3]{4} 根号\\
\not= 不等于\\
\approx 约等于\\
\leq 小于等于\\
\geq 大于等于\\
\times 乘号\\
\div 除号\\
\pm 正负号\\
\sum_{i=1}^{10} 求和\\
\prod_{i=1}^{10} 累乘\\
\coprod_{i=1}^{10} 累除\\
90^\circ 度数\\
\sin\pi 三角函数 \\
\cos\pi \\
\tan\pi \\
\infty 无穷\\
\int 定积分\\
\iint双重积分\\
y\prime 求导\\
\lim 极限\\
\emptyset 空集\\
\in 属于\\
\notin 不属于\\
$$
