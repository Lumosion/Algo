# 虚拟世界

## 题目



**时间限制：1000ms**

**内存限制：256MB**

$Rin$ 是一首[音乐MV](https://music.163.com/#/mv?id=5372069)的主角，在 $Rin$ 很小的时候，地球即将被彗星撞击，她的父亲为了拯救 $Rin$，启动了一个名为 ***project-505*** 的项目，提前将她送出了地球，并为她建立了一个虚拟世界 ， $Rin$ 可以在这个世界中创造一切。

$Rin$ 可以在其中生成多种多样的物品，但是虚拟世界的存储大小是有限的，为了节省存储大小，设定虚拟世界所配置的单个物品的最大占用大小为 $n$ （物品占用大小可以和 $n$ 相等），每个物品有一个编号值 $x$，每个物品所占用的大小为 $size=\left\lceil \sum \limits_{i=1}^{x}\dfrac{i^2}{x+1} \right\rceil$ ，即 $size=\left\lceil \dfrac{1^2}{x+1}+\dfrac{2^2}{x+1}+\dots +\dfrac{x^2}{x+1} \right\rceil$ 。

其中 $\left\lceil x \right\rceil$ 代表向上取整，例如 $\left\lceil 1.2 \right\rceil=2$ ，$\left\lceil 2.0 \right\rceil=2$ ，$\left\lceil 2.7 \right\rceil=3$ 。

现在 $Rin$ 有一个物品，它的编号值为 $m$ ，能想知道这个物品能否在虚拟世界中生成出来，如果可以，请输出 "YES"，不可以，请输出 "NO"，注意输出时不带双引号。

## 输入格式

输入两个数，分别代表虚拟世界单个物品的最大占用大小 $n$ 和物品编号值 $m$ ；

$1 \le n,m \le 10^9$，其中 $n,m$ 均为整数

## 输出格式

这个物品可以在虚拟世界中生成，请输出 "YES"，不可以，请输出 "NO"，注意输出时不带双引号。

## 样例输入

```
4 3
```

## 样例输出

```
YES
```

## 提示

样例中 $n=4$，编号值为 $3$ ；

当物品编号值为 $3$ 时，这个物品所占用大小为 $size=\left\lceil \dfrac{1^2}{3+1}+\dfrac{2^2}{3+1} +\dfrac{3^2}{3+1} \right\rceil =\left\lceil \dfrac{14}{4} \right\rceil=4$，不超过 $4$ ，所以可以生成 ；

# 题解

## 思路

设 $a_n=n^2$ 

则 $S_n=1^2+2^2+\dots+n^2=\dfrac{1}{6}n(n+1)(2n+1)$

因此 $size=\dfrac{S_n}{n+1}=\dfrac{1}{6}n(2n+1)$；

由于 $\left\lceil size \right\rceil \ge size$

所以直接将 $size$ 和 $n$ 比较大小即可；



对于**暴力方法**，可以做，但是需要缩小 $m$ 的范围。

当 $m \ge 10^5$ 时，他的 $size$ 已经大于 $10^9$ 了，因为输入的 $1 \le n \le 10^9$，所以 $m \ge 10^5$ 时，不论 $n$ 为多少，直接输出“NO”； 

所以暴力循环累加到 $10^5$ ，不会超时。 

## 代码

```C++
#include <iostream>
using namespace std;

int main()
{
    int n, m;
    cin >> n >> m;
    double f = 1.0 * m * (2 * m + 1) / 6;
    if (n >= f)
        cout << "YES" << endl;
    else
        cout << "NO" << endl;
}
```

