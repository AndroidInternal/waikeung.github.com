---
layout: post
title: "浅酌算法:希尔排序"
description: "关于希尔排序的一些事"
category: 数据结构与算法
tags: [算法, 排序]
---

希尔排序是插入排序的扩展，通过允许非相邻的元素进行交换来提高执行效率。

希尔排序的基本思路是，将待排序的序列分成几个区域。插入排序的间隔是1,而希尔排序以更大的间隔来比较和交换元素，这样最大的元素就能更快的到达序列的结尾。

1. 选取一个步长序列，
2. 按步长序列的个数k，对序列进行k糖排序
3. 每趟排序跟据对应的步长gap，将待排序的序列分割若干段子序列，分别对各子序列进行插入排序。
4. 最后一趟的步长为1,就是直接插入排序。

```c
void shellsort(int array[], int n)
{
    int i, j, k, gap;
    int key;

    for (gap = n/2; gap > 0; gap /= 2) {    /* step */
        for (i = 0; i < gap; i++) {         /* gap insert sort*/
            for (j = i+gap; j < n; j += gap) {  /* one insert sort*/
                if (array[j] < array[j-gap]) {
                    key = array[j];
                    k = j - gap;
                    while (k >= 0 && array[k] > key) {
                        array[k+gap] = array[k];
                        k -= gap;
                    }
                    array[k+gap] = key;
                }
            }
        }
    }
}
```

希尔排序的步长选择是重要的部分。可以参照[维基百科](http://zh.wikipedia.org/wiki/%E5%B8%8C%E5%B0%94%E6%8E%92%E5%BA%8F)。
