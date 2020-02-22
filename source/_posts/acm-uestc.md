title: ACM 校赛初赛 Writeup
date: 2017-03-30 01:57:02
desc: 
tags: [ACM] 
index_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/acm-uestc.jpg
banner_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/acm-uestc.jpg
---

心疼叶姐姐五点睡九点起来，一起约晚饭的时候都要吃睡去了，队友们很给力，配合得也不错 2333。希望决赛混个末等奖哈哈哈（逃）

<!-- more -->

# C

There are infinite coins with values 1,2,5,10.

What's the minimum numbers of coins should be picked that XX and YY can be made change for?

## Input
Two integers X and Y. (1≤X,Y≤10^9)

## Output
The minimum numbers of coins should be picked.

手动打表，然后发现 9 和 31 之类的数据需要特判什么的

大家都说第 24 个点有毒。

```cpp
#include<cstdio>
#include<algorithm>
using namespace std;

int a[112][112];
const int c[5] = {0, 1, 2, 5, 10};
int i, j, k, l, x, y, xx, yy, minans;
int ans[10]; 
int main()
{
    for (i = 0; i <= 100; i++)
        for (j = i; j <= 100; j++)
            a[i][j] = 1000000000;
    a[0][0] = 0;
    for (i = 0; i <= 100; i++)
        for (j = i; j <= 100; j++)
        {
            for (k = 0; k < 5; k++)
                if (i >= c[k])
                    for (l = 0; l < 5; l++)
                        if (j >= c[l])
                        {
                            x = i - c[k]; y = j - c[l];
                            if (x > y) swap(x, y);
                            if (k == l || k * l == 0) a[i][j] = min(a[i][j], a[x][y] + 1);
                            else a[i][j] = min(a[i][j], a[x][y] + 2);
                        }
        }
    scanf("%d%d", &x, &y);
    if (x > y) swap(x, y);
    if (x <= 100 && y <= 100)
        printf("%d", a[x][y]);
    else {
        minans = 1000000000;
        for (i = 1; i <= 2; i++)
            for (j = 1; j <= 2; j++)
            {
                xx = x % 10;
                yy = y % 10;
                if (i == 2 && x > 20) xx += 10;
                if (j == 2 && y > 20) yy += 10;
                k = max((x - xx) / 10, (y - yy) / 10);
                if (xx > yy) swap(xx, yy);
                k += a[xx][yy];
                if (k < minans) minans = k;
            }
        
        printf("%d", minans);
    }
    return 0;
}
```

# D

Alice want to build n cities on a plane. A city can be regarded as a point. In order to keep communication between cities, the distance between each pair of cities must NOT greater than DD.

Bob has a weapon which can destroy all the cities in a circle with radius RR. After Alice building all the cities, Bob will select a city as the center and use his weapon once, and he will choose a way such that can destroy as many cities as possible.

To prevent the cities from being destroyed, Alice want choose a way to build her cities such that the number of cities will be destroyed by Bob can be as little as possible, can you tell her how to build these cities?

In order to make the problem easier, you can assume that D=2√RD=2R is always established, so the specific values of DD and RR will not affect the answer.

## Input
Only one line contains an integer n.

1≤n≤10^18.

## Output
The number of cities will be destroyed by Bob if Alice choose the optimal scheme to build her cities.

猜测将点分成三份就行，猜测正确。

```cpp
#include <iostream>
#include <string>
#include <cmath>
#include <stack>
#include <queue>
#include <map>
#include <set>
#include <cstring>
#include <iomanip>
#include <cstdlib>
using namespace std;

long long n; 

int main() 
{
	cin>>n;
	cout << (n+2)/3;
	return 0;
}
```

# J

You are given two numbers n and k.

You are required to construct a permutation p1,p2,...,pn of numbers 1,2,...,n such that there are exactly kk different numbers in |p1−p2|, |p2−p3|, ..., |pn−1−pn|.

## Input
Only one line contains two integers n and k.

1≤k<n≤100000.

## Output
Print n integers forming the permutation.

If there are multiple answers, print any of them.

If there are no such permutation, print -1.

先打表看看对应输出的解有什么特点，如果k=n-1的时候
发现是

1 n 2 (n-1) 3 (n-2) ……之类的形式，

考虑前面构造（k-1）个差值，最后差值为1，把没输出的输出了

```cpp

#include <iostream>
#include <string>
#include <cmath>
#include <stack>
#include <queue>
#include <map>
#include <set>
#include <cstring>
#include <iomanip>
#include <cstdlib>
#include <algorithm>
using namespace std;

int n,k;
int l,r;

int main() 
{
	cin>>n>>k;
	
/*	if (k==1) 
	{
		for (int i=1;i<=n;i++) cout<<i<<" ";
		return 0;
	}*/
	
	if (k<1 || k>=n) 
	{
		cout<<-1;
		return 0;
	}
	l=1;
	r=n;
	for (int i=1;i<=k;i++)
	{
		if (i%2) cout<<(l++)<<" ";
		else cout<<(r--)<<" ";
	}
	
	if (k%2==0) 
	{
		for (l=l-1;r>l;r--) cout<<r<<" ";
	}
	else 
	{
		for (r=r+1;r>l;l++) cout<<l<<" ";
	}
}


# K

There are 10 tests.

For the ith test, you should output i.

## Input
No input.

## Output
For the ith test, you should output i.

一看，神题，我去翻了翻卿学姐的博客，嗯，他暂时不会

然后 C 和 C++ time 都被封锁了，第一反应是 java 写，不过没想到是 java 时间函数没被锁掉

```java

import java.io.*; 
import java.util.*;  

public class Main { 
    public static void main(String[] args) throws Exception {
            long t = System.currentTimeMillis();
            while (t % 1000 > 900) {
                t = System.currentTimeMillis();
            }
            t = t / 1000 % 10;
            if (t == 0) t = 10;
            System.out.println (t);
            t = System.currentTimeMillis();
            while (t % 1000 < 900) {
                t = System.currentTimeMillis();
            }
    }  
}

```

# M

There are N numbers where the ith is Ai.

In order to make the sum of them changed to S, you can make some numbers increased by one or decreased by one.

But you should spend Ci dollars to increase or decreased Ai by one, and the new Ai should satisfies Li≤Ai≤Ri.

Any number can be operated any times. What's the minimum cost to make the sum of all numbers changed to S?

## Input
The first line contains two integers N,S,

Next NN lines each line contains four integers Ai,Ci,Li,Ri.

1≤N≤1000,1≤S≤106,1≤Ci≤1000,0≤Li≤Ai≤Ri≤1000
## Output
If there is no solutions, print impossible.

Otherwise, print one integer indicates the minimum cost to make the sum of all numbers changed to S.

转化为有限装包问题

```cpp

#include <iostream>
#include <string>
#include <cmath>
#include <stack>
#include <queue>
#include <map>
#include <set>
#include <cstring>
#include <iomanip>
#include <cstdlib>
using namespace std;

int n; 
int subnum;
long long ans;
int a[2020];

int main() 
{
	int x,y,z,zz;
	cin>>n>>subnum;
	for (int i=1;i<=n;i++)
	{
		cin>>x>>y>>z>>zz;
		a[1010+y]+=zz-x;
		a[1010-y]+=x-z;
		subnum-=x;
	}
	
	if (subnum>0)
	{
		for (int i=1;i<=1000;i++)
		{
			int addnum=min(subnum,a[1010+i]);
			ans+=i*addnum;
			subnum-=addnum;
		}
		if (subnum)
		{
			cout<<"impossible"<<endl;
			return 0;
		}
		else 
		{
			cout<<ans<<endl;
			return 0;
		} 
	} 
	else
	{
		subnum=-subnum;
		for (int i=1;i<=1000;i++)
		{
			int addnum=min(subnum,a[1010-i]);
			ans+=i*addnum;
			subnum-=addnum;
		}
		if (subnum)
		{
			cout<<"impossible"<<endl;
			return 0;
		}
		else 
		{
			cout<<ans<<endl;
			return 0;
		} 
	}
}

```
