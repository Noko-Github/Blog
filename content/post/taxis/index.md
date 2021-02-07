---
title: "Taxis"
date: 2021-02-07T17:42:24+09:00
draft: false
---

# 解説 Taxis

# はじめに

BFSとDijkstra法を組み合わせた教育的な問題があったため解説

問題は下記の通り。

> N個のノードがあり、K本の双方向の辺で結ばれている。各ノードからCiのコストでRiまでのノードに移動できる。ノード1からノードNまでに移動に必要な最小コストを求めよ。

# 解法

## グラフの貼り直し

この問題のポイントは特定のノードiから、Riまでの範囲であれば同じコストで移動できる点です。そのため、bfsによって特定ノードiからどこまで移動できるかのグラフを再構築することができます。そうすることで何が嬉しいかというと、「各辺をノード間の距離としたグラフ」を、「各辺を重みとしたコストCiで到達できるグラフ」に変換できるので、後段のdijsktra法を簡単に適用できます。イメージは下のような感じ。

![./img/Untitled.png](./img/Untitled.png)

```python
def bsf(node, limit):

    is_used = [False] * N
    is_used[node] = True
    que = deque([])
    que.append((node, 0))

    while que:
        u, cost = que.popleft()
        for v in G[u]:
            if is_used[v]:
                continue
            is_used[v] = True
            if cost + 1 <= limit:
                short_G[node].append(v)
                que.append((v, cost + 1))
```

## 最短経路の算出

ある特定のノードからその他のノードへの最短経路の算出はdijkstra法で求めることができます。ノードに関する問題の基本的なアルゴリズムですので、押さえておきましょう。

```python
def dijkstra(start):
    hq = [(0, start)]
    heapq.heapify(hq)
    while hq:
        prev_cost, u = heapq.heappop(hq)
        is_used[u] = True # 確定処理: この時点でuは更新されなくなる
        for v in short_G[u]:
            if is_used[v]:
                continue
            if cost[v] >= prev_cost + C[u]:
                heapq.heappush(hq, (prev_cost + C[u], v))
                cost[v] = prev_cost + C[u]
```

# コード

```python
import heapq
from collections import deque

N, K = map(int, input().split())

R = []
C = []
for i in range(N):
    c, r = map(int, input().split())
    R.append(r)
    C.append(c)

G = [[] for _ in range(N)]
for i in range(K):
    A, B = map(int, input().split())
    A -= 1
    B -= 1
    G[A].append(B)
    G[B].append(A)

# bfsにより各ノードの連結を修正する
def bsf(node, limit):

    is_used = [False] * N
    is_used[node] = True
    que = deque([])
    que.append((node, 0))

    while que:
        u, cost = que.popleft()
        for v in G[u]:
            if is_used[v]:
                continue
            is_used[v] = True
            if cost + 1 <= limit:
                short_G[node].append(v)
                que.append((v, cost + 1))

short_G = [[] for _ in range(N)]
for i in range(N):
    bsf(i, R[i]) # 各タクシーでどこまでいけるかを計算

cost = [float('inf')] * N
is_used = [False] * N
cost[0] = 0
def dijkstra(start):
    hq = [(0, start)]
    heapq.heapify(hq)
    while hq:
        prev_cost, u = heapq.heappop(hq)
        is_used[u] = True # 確定処理: この時点でuは更新されなくなる
        for v in short_G[u]:
            if is_used[v]:
                continue
            if cost[v] >= prev_cost + C[u]:
                heapq.heappush(hq, (prev_cost + C[u], v))
                cost[v] = prev_cost + C[u]
dijkstra(0)
print(cost[N-1])
```

# 最後に

今回の問題のキーワード：

bfs→到達可能経路の貼り直し

ダイクストラ法