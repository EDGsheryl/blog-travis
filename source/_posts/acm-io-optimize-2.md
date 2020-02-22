title: ACM 输入输出优化技巧——故事的后来
date: 2018-06-15 07:21:39
desc: 
tags: [ACM] 
index_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/acm-io-optimize-2/title.jpg
banner_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/acm-io-optimize-2/title.jpg
---
作为一个蒟蒻，整天被各种 ACM 大神吊着打，他们不仅喜欢出难题考到你，甚至连简单题都不让你 AC ——故意出数据卡你。

比如说构造一个 spfa 过不去的图，或者卡那些不打读入优化的懒家伙。

<!-- more -->

在很久很久以前，在我还是刚刚学 OI 的时候，学弟（没错，你没有看错，就是学弟！）就教我用 scanf 了。

“哇，这是什么垃圾，还要记什么占位符”

直到我看了某白色的竞赛书，居然可以有 cin cout 这种不用记占位符神操作？！

我靠 ，我就跟发现新大陆了一样，之后一直使用 cin cout 过我的模拟题生活。

## 后来的后来

他们出了一道裸的线段树，然后我读入炒鸡慢，他们把我卡掉了！

甚至上了大学，还有个不知道菜到哪里去（误）的人嘲笑我，说垃圾 cin 肯定跑不过 scanf。

## 直到了今天！

故事终于发生了转机。

我想说的是，你们<del>辣鸡</del> scanf 终于跑不过我大 cin 啦，哼哼哼哼~~

当然是关同步的，不关同步别想了(那份代码 TLE 了。。。)

## 测试现场

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/acm-io-optimize-2/QQ%E6%88%AA%E5%9B%BE20180615062851.png)

### 测试用题目

[http://codeforces.com/contest/984/problem/C](http://codeforces.com/contest/984/problem/C)

### 测试用代码

```cpp
#include <bits/stdc++.h>

using namespace std;

using ll = long long;
ll p, q, b;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);

    int T;
    cin >> T;
    while (T--) {
        cin >> p >> q >> b;
        p %= q;
        ll e = __gcd(p, q);
        p /= e;
        q /= e;

        while (b != 1) {
            while (q % b == 0) q /= b;
            b = gcd(q, b);
        }
        if (q == 1)
            cout << "Finite\n";
        else
            cout << "Infinite\n";
    }
}

```

所有测试用代码从本代码的基础上加以修改，或替换读入，或者替换gcd。

### 测试结果

| 代码编号 | 编译器 | 区别 | 时间 |
| :----: |:----:| :----:| :----: |
| 39253502 | GNU C++17 | 关同步cin std::gcd | 358 ms |
| 39253484 | GNU C++17 | 按字符读入优化 std::gcd | 499 ms |
| 39253554 | GNU C++17 | 按字符读入优化 std::gcd | 483 ms |
| 39253582 | GNU C++14 | 关同步cin std::__gcd | 358 ms |
| 39253589 | GNU C++11 | 关同步cin std::__gcd | 436 ms |
| 39253603 | GNU C++98 | 关同步cin std::__gcd | 436 ms |
| 39253617 | GNU C++17 | 关同步cin 手写gcd | 389 ms |
| 39253661 | GNU C++17 | scanf std::gcd | 374 ms |

因为 std::gcd() 是 C++17 有的，所以其他使用了 std::__gcd()

由于 C++17 测试版本和 C++14 测试版本所耗费时间相同，暂时排除标准 gcd 函数的影响。

按字符读入优化是你们最喜欢的按字符读入，然后处理成数字返回。其中有两个版本的，39253484是我写的，39253554是 @Xris 写的，两份只是为了证明 <del>我手写的东西比叶姐姐写的常数大</del> 排除影响。

手写 gcd() 来自 @Xris [http://xr1s.me/](http://xr1s.me/)

```cpp
// Stein's algorithm, find the greatest common divisor (GCD) of m and n.
// The result will always be non-negative.
// If m or n is zero, the result will be the bigger one.
// This implementation is 1 time faster than GNU STL std::gcd (C++17).
// @param m: m above.
// @param n: n above.
// @return: GCD(m, n), always positive.
template <typename T>
T gcd(T m, T n) {
  if (!m || !n) return m | n;
  if (m < 0) m = -m;
  if (n < 0) n = -n;
  int p = 0;
  while (!(m & 1) && !(n & 1))
    m >>= 1, n >>= 1, ++p;
  while (n) {
    while (!(m & 1)) m >>= 1;
    while (!(n & 1)) n >>= 1;
    if (m >= n) std::swap(m, n);
    n = (n - m) >> 1;
  }
  return m << p;
}

```

### 测试分析

在 C++14 及之后版本的 iostream 明显在时间上占优势。

手写的 gcd 函数不占有优势（叶姐姐的那个应该会比递归版本的快）

## 理性对待测试结果

测试只是测了一次，但是我觉得应该不会有太大的问题。

由于参加各类竞赛的时候并不知道具体的编译选项，所以还是推荐使用其他读入方法。但是对于 Codeforces 平台上的题，用关同步的 iostream + C++17 效果更佳。其实前两天我看到某群里就说同一份代码 c++17 没过 c++14 过了。甚是玄学。

由于 Codeforces 是 Windows 的，我们也不知道跨平台后是不是也是有相同结果。

根据个人经验，C++98，在 Linux 下读写文件时 fstream 的速度比 stdio 快。在 Windows 下旗鼓相当。

## 后来的最后

本文对所有情况不具有普遍性，但仍具有一定参考价值 =w=

代码也在 Codeforces 上，可以直接查看，欢迎其他小伙伴加入测试或者讨论。
