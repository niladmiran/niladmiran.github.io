---
layout: post
title: 疯子选座问题
---
## 介绍

问题描述如下：

> 100个人坐飞机，每个人都会根据自己的机票乘坐机票对应的座位。不妨假设第i个乘客坐在第i个座位。
>
> 但是第一个乘客是个疯子，他会在100个座位中随机挑选一个座位坐下。对于第i个乘客($2\leq i\leq100$)，他们会依次执行以下操作：
>
> 1. 如果第i个座位没有被占，则坐在第i个座位
> 2. 如果第i个座位被占，则随机挑选剩下的座位
>
> 问题为：第100名乘客坐在第100个座位上的概率是多少？

## 解法

### 解法1

首先我们看一个比较简单的解法。对于第一个乘客，他有三种可能：

1. 他坐在自己的座位上，那么所有的乘客都可以坐在自己的座位上
2. 他坐在第100个座位上，那么第100个乘客不能坐在自己的座位上
3. 他坐在第i($2\leq i\leq 99$)个座位上

对于第一种和第二种情况，问题已经得到解决，问题是第三种情况。其实这个时候，我们可以认为，第i个乘客成为了疯子：

1. 他如果选择坐在第1个座位上，那么后续所有乘客都可以坐在自己的座位上
2. 他坐在第100个座位上，那么第100个乘客不能坐在自己的座位上
3. 他坐在第j($i+1\leq j\leq 99$)个座位上

我们可以看到，当出现第三种情况时，除了问题的规模减小（$100\to 100-i$）之外，并没有任何改变。因此，这个问题最后就变成了第一个乘客和最后一个乘客的battle：

1. 他坐在自己的座位上，那么所有的乘客都可以坐在自己的座位上
2. 他坐在第100个座位上，那么第100个乘客不能坐在自己的座位上

由于第一个乘客选座位是随机的，因此这两种情况的可能性是一样的，即最后一个乘客坐在自己的座位上的可能性是1/2.

一个比较类似的解释为：将这个模型简化为抛硬币模型，抛到正面和反面的概率各为$\frac{1}{n}$，表示第一个人坐在自己的座位上和坐在最后一个人的座位上。抛到硬币立起来的概率为$\frac{n-2}{n}$, 当硬币立起来时，我们重新抛这枚硬币，但是此时$n$至少会减少1,问结果为反面的概率。

### 解法2

上面的分析可能不是很严谨，接下来我们用概率来解决这个问题：假设现在有$n$个人，第$i$个人的座位被占的概率为$P(i)$.

当$i=2$时，他的座位只会被第一个人占，此时$P(i)=\frac{1}{n}$。

当$i=3$时，他的座位可能被第一个人或者第二个人占，$P(3)=\frac{1}{n}+P(2)\frac{1}{n - 1}$

一般地，对第$i(i\geq2)$个人，他的座位可能会被前$i-1$个人占，我们有：
$$
P(i)=\frac{1}{n}+\sum_{j=2}^{i-1}P(j)\frac{1}{n-(j-1)}
$$
注意到$P(i+1)$和$P(i)$有比较多的相同项，我们有：
$$
P(i+1)-P(i) = P(i)\cdot \frac{1}{n+1-i}\Rightarrow P(i+1)=P(i)\frac{n+2-i}{n+1-i}
$$
故
$$
P(i+1) = P(2)\prod_{j=2}^i\frac{n+2-j}{n+1-j}=\frac{1}{n+1-i},i\geq2
$$
验证可知，$i=1$时也成立，故
$$
P(i)=\frac{1}{n+2-i},i\geq2
$$
故第$n$个座位被占的概率为$\frac{1}{2}$.



## 参考文献

[1]https://www.zhihu.com/question/35950050

[2]https://math.stackexchange.com/questions/5595/taking-seats-on-a-plane

[3]https://leetcode.com/problems/airplane-seat-assignment-probability/
