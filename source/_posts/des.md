title: DES 算法学习笔记
date: 2018-03-18 01:36:21
desc: 
tags: [crypto] 
index_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/des.jpg
banner_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/des.jpg
---

DES全称为Data Encryption Standard，即数据加密标准，是一种使用密钥加密的块算法，

<!-- more -->

1977年被美国联邦政府的国家标准局确定为联邦资料处理标准（FIPS），并授权在非密级政府通信中使用，随后该算法在国际上广泛流传开来。需要注意的是，在某些文献中，作为算法的DES称为数据加密算法（Data Encryption Algorithm,DEA），已与作为标准的DES区分开来。

## 算法流程

算法流程可以参考百度百科的算法流程图

[![](https://gss3.bdstatic.com/7Po3dSag_xI4khGkpoWK1HF6hhy/baike/c0%3Dbaike80%2C5%2C5%2C80%2C26/sign=bf7cb45b367adab429dd1311eabdd879/adaf2edda3cc7cd9ca7533aa3901213fb80e916c.jpg)](https://gss3.bdstatic.com/7Po3dSag_xI4khGkpoWK1HF6hhy/baike/c0%3Dbaike80%2C5%2C5%2C80%2C26/sign=bf7cb45b367adab429dd1311eabdd879/adaf2edda3cc7cd9ca7533aa3901213fb80e916c.jpg)

## 算法详解

DES算法在《图解密码技术》这本书上一笔带过了，比较好奇书上说的 f() 函数是什么，于是就找了 DES 的源码来看。

DES算法有三个参数：data，key，mode。

- data 要加密的信息
- key  加密的密钥
- mode 加密还是解密

DES算法还使用到了很多置换，搞清楚置换表的作用是非常重要的。

我们通过 key 置换，循环左移的操作得到 subkey，记为 k1，k2，...，kn。

首先将 data 置换，并且平分成两半，记为 L0 和 R0。

第 N 次操作的时候，我们需要将 Ln = R(n-1)，而 Rn = f(L(n-1), R(n-1), kn) 三个参数去计算，计算过程也相当复杂。

首先我们需要将 R(n-1) 通过拓展表拓展成 48 位的，然后跟 subkey 进行异或，然后根据 s 盒表的规则，将对应每 6 位变换成 4 位，重新变成 32 位，再和 L(n-1) 进行异或操作。

最最重要的是！千万不能搞错谁和谁异或，用谁去操作，不然 bug 就找不到了。

## 代码实现

最后恬不知耻地贴上自己的代码 诶嘿

```cpp
#include <bits/stdc++.h>

using namespace std;

class DES {
private:

//const table

    const char IP_Table[64] = {
            58, 50, 42, 34, 26, 18, 10, 2, 60, 52, 44, 36, 28, 20, 12, 4,
            62, 54, 46, 38, 30, 22, 14, 6, 64, 56, 48, 40, 32, 24, 16, 8,
            57, 49, 41, 33, 25, 17, 9, 1, 59, 51, 43, 35, 27, 19, 11, 3,
            61, 53, 45, 37, 29, 21, 13, 5, 63, 55, 47, 39, 31, 23, 15, 7
    };
    const char IPR_Table[64] = {
            40, 8, 48, 16, 56, 24, 64, 32, 39, 7, 47, 15, 55, 23, 63, 31,
            38, 6, 46, 14, 54, 22, 62, 30, 37, 5, 45, 13, 53, 21, 61, 29,
            36, 4, 44, 12, 52, 20, 60, 28, 35, 3, 43, 11, 51, 19, 59, 27,
            34, 2, 42, 10, 50, 18, 58, 26, 33, 1, 41, 9, 49, 17, 57, 25
    };
    const char PC1_Table[56] = {
            57, 49, 41, 33, 25, 17, 9, 1, 58, 50, 42, 34, 26, 18,
            10, 2, 59, 51, 43, 35, 27, 19, 11, 3, 60, 52, 44, 36,
            63, 55, 47, 39, 31, 23, 15, 7, 62, 54, 46, 38, 30, 22,
            14, 6, 61, 53, 45, 37, 29, 21, 13, 5, 28, 20, 12, 4
    };
    const char PC2_Table[48] = {
            14, 17, 11, 24, 1, 5, 3, 28, 15, 6, 21, 10,
            23, 19, 12, 4, 26, 8, 16, 7, 27, 20, 13, 2,
            41, 52, 31, 37, 47, 55, 30, 40, 51, 45, 33, 48,
            44, 49, 39, 56, 34, 53, 46, 42, 50, 36, 29, 32
    };
    const char LOOP_Table[16] = {
            1, 1, 2, 2, 2, 2, 2, 2, 1, 2, 2, 2, 2, 2, 2, 1
    };
    const char E_Table[48] = {
            32, 1, 2, 3, 4, 5, 4, 5, 6, 7, 8, 9,
            8, 9, 10, 11, 12, 13, 12, 13, 14, 15, 16, 17,
            16, 17, 18, 19, 20, 21, 20, 21, 22, 23, 24, 25,
            24, 25, 26, 27, 28, 29, 28, 29, 30, 31, 32, 1
    };

    const char S_Box[8][4][16] = {
            // S1
            14, 4, 13, 1, 2, 15, 11, 8, 3, 10, 6, 12, 5, 9, 0, 7,
            0, 15, 7, 4, 14, 2, 13, 1, 10, 6, 12, 11, 9, 5, 3, 8,
            4, 1, 14, 8, 13, 6, 2, 11, 15, 12, 9, 7, 3, 10, 5, 0,
            15, 12, 8, 2, 4, 9, 1, 7, 5, 11, 3, 14, 10, 0, 6, 13,
            // S2
            15, 1, 8, 14, 6, 11, 3, 4, 9, 7, 2, 13, 12, 0, 5, 10,
            3, 13, 4, 7, 15, 2, 8, 14, 12, 0, 1, 10, 6, 9, 11, 5,
            0, 14, 7, 11, 10, 4, 13, 1, 5, 8, 12, 6, 9, 3, 2, 15,
            13, 8, 10, 1, 3, 15, 4, 2, 11, 6, 7, 12, 0, 5, 14, 9,
            // S3
            10, 0, 9, 14, 6, 3, 15, 5, 1, 13, 12, 7, 11, 4, 2, 8,
            13, 7, 0, 9, 3, 4, 6, 10, 2, 8, 5, 14, 12, 11, 15, 1,
            13, 6, 4, 9, 8, 15, 3, 0, 11, 1, 2, 12, 5, 10, 14, 7,
            1, 10, 13, 0, 6, 9, 8, 7, 4, 15, 14, 3, 11, 5, 2, 12,
            // S4
            7, 13, 14, 3, 0, 6, 9, 10, 1, 2, 8, 5, 11, 12, 4, 15,
            13, 8, 11, 5, 6, 15, 0, 3, 4, 7, 2, 12, 1, 10, 14, 9,
            10, 6, 9, 0, 12, 11, 7, 13, 15, 1, 3, 14, 5, 2, 8, 4,
            3, 15, 0, 6, 10, 1, 13, 8, 9, 4, 5, 11, 12, 7, 2, 14,
            // S5
            2, 12, 4, 1, 7, 10, 11, 6, 8, 5, 3, 15, 13, 0, 14, 9,
            14, 11, 2, 12, 4, 7, 13, 1, 5, 0, 15, 10, 3, 9, 8, 6,
            4, 2, 1, 11, 10, 13, 7, 8, 15, 9, 12, 5, 6, 3, 0, 14,
            11, 8, 12, 7, 1, 14, 2, 13, 6, 15, 0, 9, 10, 4, 5, 3,
            // S6
            12, 1, 10, 15, 9, 2, 6, 8, 0, 13, 3, 4, 14, 7, 5, 11,
            10, 15, 4, 2, 7, 12, 9, 5, 6, 1, 13, 14, 0, 11, 3, 8,
            9, 14, 15, 5, 2, 8, 12, 3, 7, 0, 4, 10, 1, 13, 11, 6,
            4, 3, 2, 12, 9, 5, 15, 10, 11, 14, 1, 7, 6, 0, 8, 13,
            // S7
            4, 11, 2, 14, 15, 0, 8, 13, 3, 12, 9, 7, 5, 10, 6, 1,
            13, 0, 11, 7, 4, 9, 1, 10, 14, 3, 5, 12, 2, 15, 8, 6,
            1, 4, 11, 13, 12, 3, 7, 14, 10, 15, 6, 8, 0, 5, 9, 2,
            6, 11, 13, 8, 1, 4, 10, 7, 9, 5, 0, 15, 14, 2, 3, 12,
            // S8
            13, 2, 8, 4, 6, 15, 11, 1, 10, 9, 3, 14, 5, 0, 12, 7,
            1, 15, 13, 8, 10, 3, 7, 4, 12, 5, 6, 11, 0, 14, 9, 2,
            7, 11, 4, 1, 9, 12, 14, 2, 0, 6, 10, 13, 15, 3, 5, 8,
            2, 1, 14, 7, 4, 10, 8, 13, 15, 12, 9, 0, 3, 5, 6, 11
    };
    const char P_Table[32] = {
            16, 7, 20, 21, 29, 12, 28, 17, 1, 15, 23, 26, 5, 18, 31, 10,
            2, 8, 24, 14, 32, 27, 3, 9, 19, 13, 30, 6, 22, 11, 4, 25
    };


    int l[20][40], r[20][40];
    int keyl[40], keyr[40];
    int key[20][70];
    int ext[50];

public:
    DES() {}

    ~DES() {}

    void crypt(int *data, int *key, int *ret, int mode = 0) {
        for (int i = 0; i <= 64; i++) ret[i] = 0;

        if (!mode) { //encrypt
            memset(l, 0, sizeof l);
            memset(r, 0, sizeof r);

//initialize the L0,R0
            for (int i = 1; i <= 32; i++) {
                l[0][i] = data[IP_Table[i - 1]];
            }
            for (int i = 33; i <= 64; i++) {
                r[0][i - 32] = data[IP_Table[i - 1]];
            }

//initialize the subkey
            for (int i = 1; i <= 28; i++) {
                keyl[i] = key[PC1_Table[i - 1]];
            }
            for (int i = 29; i <= 56; i++) {
                keyr[i - 28] = key[PC1_Table[i - 1]];
            }

            for (int i = 1; i <= 16; i++) {
                for (int o = 1; o <= LOOP_Table[i]; o++) {
                    for (int j = 1; j < 28; j++) {
                        keyl[j] = keyl[j + 1];
                    }
                    keyl[28] = keyl[1];
                    for (int j = 1; j < 28; j++) {
                        keyr[j] = keyr[j + 1];
                    }
                    keyr[28] = keyr[1];
                }

                for (int o = 1; o <= 48; o++) {
                    this->key[i][o] = (PC2_Table[o - 1] <= 28 ? keyl[PC2_Table[o - 1]] : keyr[PC2_Table[o - 1] - 28]);
                }
            }

// Feistal network
            for (int i = 1; i <= 16; i++) {
                for (int o = 1; o <= 48; o++) ext[o] = r[i - 1][E_Table[o - 1]]; //extend the R(n-1)
                for (int o = 1; o <= 48; o++) ext[o] ^= this->key[i][o];//xor the subkey
                for (int o = 0; o < 8; o++) { //core algorithm of f()
                    int row = ext[6 * o + 1] * 2 + ext[6 * o + 6];
                    int col = ext[6 * o + 2] * 8 + ext[6 * o + 3] * 4 + ext[6 * o + 4] * 2 + ext[6 * o + 5];

                    int midresult = S_Box[o][row][col];
                    for (int j = 1; j <= 4; j++) {
                        ext[32 - 6 * o - j + 1] = midresult % 2;
                        midresult /= 2;
                    }
                }
                for (int o = 1; o <= 32; o++) {
                    r[i][o] = ext[P_Table[o - 1]] ^ l[i - 1][o];//xor the L(n-1)
                }
                for (int o = 1; o <= 32; o++) {
                    l[i][o] = r[i - 1][o];
                }

            }
            for (int i = 1; i <= 64; i++) {
                ret[i] = IPR_Table[i - 1] <= 32 ? r[16][IPR_Table[i - 1]] : l[16][IPR_Table[i - 1] - 32];
            }

        } else { //decrypt
            memset(l, 0, sizeof l);
            memset(r, 0, sizeof r);

            for (int i = 1; i <= 32; i++) {
                l[0][i] = data[IP_Table[i - 1]];
            }
            for (int i = 33; i <= 64; i++) {
                r[0][i - 32] = data[IP_Table[i - 1]];
            }

            for (int i = 1; i <= 28; i++) {
                keyl[i] = key[PC1_Table[i - 1]];
            }
            for (int i = 29; i <= 56; i++) {
                keyr[i - 28] = key[PC1_Table[i - 1]];
            }

            for (int i = 1; i <= 16; i++) {
                for (int o = 1; o <= LOOP_Table[i]; o++) {
                    for (int j = 1; j < 28; j++) {
                        keyl[j] = keyl[j + 1];
                    }
                    keyl[28] = keyl[1];
                    for (int j = 1; j < 28; j++) {
                        keyr[j] = keyr[j + 1];
                    }
                    keyr[28] = keyr[1];
                }

                for (int o = 1; o <= 48; o++) {
                    this->key[i][o] = (PC2_Table[o - 1] <= 28 ? keyl[PC2_Table[o - 1]] : keyr[PC2_Table[o - 1] - 28]);
                }
            }

            for (int i = 1; i <= 16; i++) {
                for (int o = 1; o <= 48; o++) ext[o] = r[i - 1][E_Table[o - 1]];
                for (int o = 1; o <= 48; o++) ext[o] ^= this->key[17 - i][o];
                for (int o = 0; o < 8; o++) {
                    int row = ext[6 * o + 1] * 2 + ext[6 * o + 6];
                    int col = ext[6 * o + 2] * 8 + ext[6 * o + 3] * 4 + ext[6 * o + 4] * 2 + ext[6 * o + 5];

                    int midresult = S_Box[o][row][col];
                    for (int j = 1; j <= 4; j++) {
                        ext[32 - 6 * o - j + 1] = midresult % 2;
                        midresult /= 2;
                    }
                }
                for (int o = 1; o <= 32; o++) {
                    r[i][o] = ext[P_Table[o - 1]] ^ l[i - 1][o];
                }
                for (int o = 1; o <= 32; o++) {
                    l[i][o] = r[i - 1][o];
                }

            }
            for (int i = 1; i <= 64; i++) {
                ret[i] = IPR_Table[i - 1] <= 32 ? r[16][IPR_Table[i - 1]] : l[16][IPR_Table[i - 1] - 32];
            }
        }

        return;
    }
};

int main() { //take a test
    DES des = *(new DES());
    int a[100]{};
    for (int i = 1; i <= 64; i+=2) a[i] = 1;
    int b[100]{};
    int c[100]{};
    int d[100]{};

    des.crypt(a, b, c, 0);
    des.crypt(c, b, d, 1);
    for (int i = 1; i <= 64; i++) cout << d[i];
}


```

## 算法改进

在 1999 年的 DES Challenge III 中，破译 DES 密文只用了 22 小时 15 分钟，所以提出了三重 DES(triple-DES)。

三重 DES 并不是运行三次 DES 加密，而是加密解密加密的形式

虽然听上去非常不可思议，但是这样做可以兼容普通的 DES（三次都使用同一个 key）。

我们称使用两个 key 的 TDEA 为 DES-EDE2，使用三个 key 的为 DES-EDE3。

对应的，解密过程为：解密加密解密。


