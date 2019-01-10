---
title: "数据结构-哈夫曼树"
date: <span class="timestamp-wrapper"><span class="timestamp">&lt;2019-01-07 Mon 02:54&gt;</span></span>
layout: post
categories: 
- programming
tags: 
- datastruct
---

# Table of Contents

1.  [哈夫曼树](#org6864b74)
    1.  [哈夫曼树的构造方法](#org5819d1f)
    2.  [哈夫曼树的特点](#orgea1e1bc)
    3.  [哈夫曼编码](#org3d34d4a)


<a id="org6864b74"></a>

# 哈夫曼树

给定n个权值作为n个叶子结点，构造一棵二叉树，若该树的带权路径长度达到最小，称这样的二叉树为最优二叉树，也称为哈夫曼树(Huffman Tree)。 \\
哈夫曼树是带权路径长度最短的树，权值较大的结点离根较近。


<a id="org5819d1f"></a>

## 哈夫曼树的构造方法

每次把权值最小的两颗二叉树合并

{% highlight c %}
typedef struce TreeNode *HuffmanTree;

struct TreeNode{
  int Weight;
  HuffmanTree Left, Right;
};

HuffmanTree Huffman( MinHeap H ) {
  // 假设 H->Size 个权值已经存在 H->Elements[]->Weight里
  int i; HuffmanTree T;
  BuildMinHeap(H); //将 H->Elements[]按权值调整为最小堆
  for (i = 1; i < H->Size; i++) {
    T = malloc(sizeof(struct TreeNode)); // 建立新的结点
    T->Left = DeleteMin(H); // 从最小堆中删除一个结点，作为新T的左子结点
    T->Right = DeleteMin(H); // 从最小堆中删除一个结点， 作为新t的右子结点
    T->Weight = T->Left->Weight+T->Right->Weight; // 计算新的权值

    Insert(H, T); // 将新T 插入最小堆
  }
  T = DeleteMin(H);
  return T;
}
{% endhighlight %}


<a id="orgea1e1bc"></a>

## 哈夫曼树的特点

1.  没有度为1 的结点
2.  如果n个叶子结点的哈夫曼树共2n-1 个结点
3.  哈夫曼树的任意非叶结点的左右子树交换后仍是哈夫曼树
4.  对同一组{w1, w2, w3,&#x2026;,wn}, 存在不同构的两颗哈夫曼树， WPL值一样。


<a id="org3d34d4a"></a>

## 哈夫曼编码

-   前缀码（prefix code）：任何字符的编码都不是另一个字符编码的前缀， 可以达到无二义地解码
-   权值： 权值就是定义的路径上面的值。可以这样理解为节点间的距离。通常指字符对应的二进制编码出现的概率。
