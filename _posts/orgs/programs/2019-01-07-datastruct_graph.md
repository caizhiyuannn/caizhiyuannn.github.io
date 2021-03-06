---
title: "数据结构-图01"
date: <span class="timestamp-wrapper"><span class="timestamp">&lt;2019-01-07 Mon 05:15&gt;</span></span>
layout: post
categories: 
- programming
tags: 
- datastruct
---

# Table of Contents

1.  [图](#org8e194ba)
    1.  [抽象数据类型定义](#org3608071)
    2.  [常见术语](#orgf79a569)
    3.  [图在程序中表示方法](#orgd11f247)
        1.  [邻接矩阵](#orgbb8aeae)
        2.  [邻接表](#org4cfdae5)
    4.  [图的遍历](#org77dfebe)
        1.  [深度优先搜索（Depth First Search, DFS）](#org2248ee0)


<a id="org8e194ba"></a>

# 图

-   表示 多对多 的关系
-   描述：
    1.  图包含一组顶点： 通常用V(Vertex)表示顶点的集合
    2.  一组边： 通常用E (Edge) 表示边的集合
        -   边是顶点对： (v, w) -> E, 其中v, w 属于V, 两个顶点可以互通
        -   有向边： <v, w> 表示从v指向w的边(单行线)
        -   不考虑重复边和自回路


<a id="org3608071"></a>

## 抽象数据类型定义

-   类型名称： 图(Graph)
-   数据对象集：G(V, E)由一个非空有限顶点集合V和一个有限边集合E组成
-   操作集：
    -   Graph Create(): 建立并返回空图
    -   Graph InsertVertex(Graph G, Vertex v): 将v插入G
    -   Graph InsertEdge(Graph G, Edge e): 将e插入G
    -   void DFS(Graph G, Vertex v): 从顶点v深度优先遍历图g
    -   void BFS(Graph G, Vertex v): 从顶点v宽度优先遍历图G
    -   void ShortestPath(Graph G, Vertex v, int Dist[]): 计算图g中顶点v到任意其它顶点的最短距离
    -   void MST(Graph G): 计算图G的最小生成树


<a id="orgf79a569"></a>

## 常见术语

1.  无向图： 图中的边是没有方向规定的
2.  有向图： 图中的边是有方向指定的， 可能是单向，可能是双向
3.  稀疏图： 点很多但是边很少，有大量无效的元素，容易浪费空间
4.  稠密图： 点很多但是边也很多。


<a id="orgd11f247"></a>

## 图在程序中表示方法


<a id="orgbb8aeae"></a>

### 邻接矩阵

用二维数组表示一个图： G[N][N] N个顶点从0到N-1编号

-   如果G[i][j] 为1： 表示 <Vi, Vj> 是G中的边， 为0：表示无边
    ![img](./images/graph01.png)

1.  邻接矩阵优点

    1.  直观，简单比较容易理解
    2.  方便检查任意一对顶点之间是否存在边
    3.  方便查找任意一顶点的所有邻接点（有边直接相连的顶点）
        -   无向图：直接扫描一行所有顶点，结果不为0的都是邻接点
        -   有向图：扫描行和列， 结果不为0的都是邻接点
    4.  方便计算任意一顶点的度。从该点发出的所有边为出度， 指向该边的边为入度
        -   无向图：扫描行或列， 非零的元素的个数为度
        -   有向图：扫描行所有非零的元素为出度， 扫描列所有非零的元素为入度。

2.  邻接矩阵缺点

    1.  浪费空间： 稀疏图点很多但是边很少，存储很多0元素，造成空间浪费
    2.  浪费时间： 统计稀疏图中一共多少条边需要遍历所有元素


<a id="org4cfdae5"></a>

### 邻接表

用G[N]指针数组， 对应矩阵中每一个链表，只存储非零的元素

1.  优点

    1.  方便查找任意一顶点的所有邻接点
    2.  节约稀疏图的空间：需要N个指针头 + 2E个结点（每个结点至少2个域）
    3.  计算任意顶点的度
        -   有向图： 方便计算
        -   无向图： 只能计算出度，入度需要构建一个逆邻接表存储指向自己的边

2.  缺点

    1.  计算任意顶点的度不方便
    2.  计算任意顶点间是否存在边比较苦难


<a id="org77dfebe"></a>

## 图的遍历


<a id="org2248ee0"></a>

### 深度优先搜索（Depth First Search, DFS）
