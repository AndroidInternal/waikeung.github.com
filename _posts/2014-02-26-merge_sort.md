---
layout: post
title: "浅酌算法:归并排序"
description: "关于归并排序的一些事"
category: 数据结构与算法
tags: [算法, 排序]
---

今天的算法课上讲到分治法(Divide and Conquer)，归并排序(Merge sort)是一个非常典型的应用。

归并排序的算法思想是将待排序的序列分成相同大小的两个子序列，然后依次对这两个子序列进行递归归并排序，之后再按照顺序进进行合并。在对子序列排序时，其长度为1时递归结束。单个元素为认为是已经排好序了。

举个最通俗的扑克牌例子，比如现在有两堆牌，每一堆都排序好了，最小的牌在最上面。现在要做的把这两堆牌合并成一堆牌，最小的在最上面这种排序。取顶上两张较小的一张放在手里，两堆牌又有两张牌在最上面，继续取较小的那张放入手中。如此反复，直到所有牌都在手中，那么手中的牌就都有序了。这就是归并排序。

下面的算法中，`p`,`q`,`r`都是代表数组的下标。将int类型的数组array进行归并排序。

合并过程：

```c
void Merge(int array[], int p, int q, int r)
{
    int n1 = q-p+1;
    int n2 = r-q;
    int *L = malloc(n1 * sizeof(int));    /*左数组*/
    int *R = malloc(n2 * sizeof(int));    /*右数组*/
    int i, j, k;
    for (i = 0; i < n1; i++)
        L[i] = array[p+i];
    for (j = 0; j < n2; j++)
        R[j] = array[q+j+1];
    i = j = 0;
    k = p;
    while ((i < n1) && (j < n2)) {
        if (L[i] <= R[j]) {
            array[k++] = L[i++];
        }
        else {
            array[k++] = R[j++];
        }
    }
    while (i < n1) {
        array[k++] = L[i++];
    }
    while (j < n2) {
        array[k++] = L[j++];
    }
    free(L);
    free(R);
}
```

递归过程：

```c
void MergeSort(int array[], int p, int r)
{
    /*array数组下标p到下标r，排序*/
    int q;
    if (p < r) {
        q = (p + r) / 2;
        MergeSort(array, p, q);
        MergeSort(array, q+1, r);
        Merge(array, p, q, r);
    }
}
```

上面的算法中，每一基本步骤都需要判断，每个子序列是否为空了。解决这个问题的想法是放一个**哨兵**，避免检查子序列是否为空。用于简化代码，这里用`MAXNUM`作为哨兵的值,可以在之前就宏定义为一个比较大的数值`#define MAXNUM 100000`。当露出哨兵的时候，不可能是两个值中的较小的值，除非另一个哨兵也出现了，但这时所有非哨兵的数值已经排序好了。

```c
void Merge(int array[], int p, int q, int r)
{
    int n1 = q-p+1;
    int n2 = r-q;
    int *L = malloc((n1 + 1) * sizeof(int));    /*左数组*/
    int *R = malloc((n2 + 1) * sizeof(int));    /*右数组*/
    int i, j, k;
    for (i = 0; i < n1; i++)
        L[i] = array[p+i];
    for (j = 0; j < n2; j++)
        R[j] = array[q+j+1];
    L[n1] = R[n2] = MAXNUM;
    i = j = 0;
    for (k = p; k <= r; k++) {
        if (L[i] <= R[j]) {
            array[k] = L[i];
            i++;
        }
        else {
            array[k] = R[j];
            j++;
        }
    }
    free(L);
    free(R);
}

递归过程也之前的一样。
