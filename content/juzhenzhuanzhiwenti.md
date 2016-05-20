Title: 矩阵转置问题
Date: 2011-07-13 08:17
Author: lmatt wang
Slug: juzhenzhuanzhiwenti

如果可以使用额外空间，编程实现矩阵转置是十分简单的，这里就不再做过多的讨论。如何在不使用额外空间的条件下转置矩阵呢？下面会分两种情况来进行讨论。\
**1.方阵的转置**\
方阵是N\*N的矩阵，通过交换m[i][j]与m[j][i]的值，就可以实现方阵的转置。\
**2.非方阵的转置**\
假设有N\*M的矩阵，其中N!=M，怎么来实现[in-place的transposition](http://en.wikipedia.org/wiki/In-place_matrix_transposition)呢？\
考虑有如下的矩阵\
|1,2|\
|3,4|\
|5,6|\
该矩阵在内存中是按[1,2,3,4,5,6]的顺序存放。\
转置之后则有\
|1,3,5|\
|2,4,6|\
该矩阵在内存中是按[1,3,5,2,4,6]的顺序存放。\
2，3，5，4这四个数的位置绕着一个环进行了一位旋转，1和6则保持位置不变。\
按照这样的思路，可以把矩阵分为多个环，然后将环进行旋转，最后就可以得到转置的矩阵。但这里存在一个问题，如何把矩阵分成多个环？貌似没有很直接的方法算出来。

(1)\
for(int i = 0; i \< m \* n; i++)\
{\
   int tobe = trans(i);\
   while(tobe \< i) tobe = trans(i);\
   swap(m[i], m[tobe]);\
}

(2)\
先转置正方形中的元素，再将其他的元素移位过去。

(3)\
只移位一次的算法，好像需要额外的空间。待进一步研究。