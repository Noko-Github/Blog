---
title: "Bipartite_graph_tutorial"
date: 2021-01-30T13:27:10+09:00
draft: false
---

# 二部グラフについてのまとめ

二部グラフに関する問題を解いていたときに、自分の理解が足りていないと感じたので改めて二部グラフについてその性質や問題を解くにあたってのポイントを整理してみた。時間が経つと忘れる点も多いので、備忘録も兼ねて整理した内容を共有します。

# 1. 二部グラフとは

二部グラフとは、連結されたグラフにおいてN個の頂点を２つの任意の集合に分けた際、各集合内のノード間に辺を持たないグラフのことです。
![This is a image](./img/_P1.png)

# 2. 二部グラフになる条件と判定方法

二部グラフの特徴はDFSを用いることで二部グラフかどうかを判定できます。UnionFindでも判定できますが、その分のコード量が多くなるので個人的にはDFSが簡単かつ単純でオススメです。

```python
def dfs(u, color):
    nodes[u] = color

    for v in range(G[u]):
        # 隣接する頂点が同じ色で塗られていれば二部グラフではない
        if nodes[u] == nodes[v]:
            return False

        # まだ色が塗られていない場合は再帰的に着色
        if nodes[v] == -1 and not dfs(v, 1^color):
            return False
    
    return True
```

# 3. 二部グラフの特徴

- ２頂点間の辺の長さが偶数か奇数かを判定できる。隣接する頂点の色は異なるため、同じ色同士の辺長さは偶数、異なる任意の２頂点間の辺の長さは奇数であると判定できます。
- 二部グラフにおける辺の最大数を計算できる。二部グラフの特徴から、各隣接ノードにおいては色の異なる頂点間のみに辺が貼られます。そのため、辺の最大数は白の頂点数をw、黒の頂点数をbとしたときにw*bで計算できます。
- 二部グラフでは奇数長のサイクルが存在しません。存在するとどこかで同じ色が隣接するためです。
※逆に二部グラフでない場合は奇数長のサイクルが存在することになります。補足ですが、奇数長のサイクルをもつ連結グラフは、全ての頂点間に奇数長で辿り着くことができます。

# 4. 二部グラフを使った問題例

ここではCODE FESTIVAL 20178 qualBのC問題「3 Steps」例題として取り上げます。グラフ問題の解法に二部グラフの判定を盛り込んだ、面白い問題です。問題の内容は下記の通りです。

> M本の辺をもつN頂点 の連結な無向グラフが存在する。
頂点uから辺を3本辿ることによって頂点vに辿り着けるようなu,v(u≠v)をとり、
頂点uと頂点vの間に辺を追加する（ただし、すでに頂点uと頂点vの間に辺が存在する場合は辺を追加することはできない。）
追加できる辺の本数の最大値を求めて下さい。

この問題の解法のポイントは3章で説明した、「二部グラフは奇数長のサイクルを持たないが」活用できます。問題で与えられた連結グラフが二部グラフかを判定することで、グラフ全体に貼られる辺の数がもとまります。最後に全体の辺の数から、最初に与えられたグラフの本数を除くことで答えが算出できます。2つ目のポイントとしては任意の奇数長の頂点間は必ず連結できるということです。これは距離が3以上の奇数長の頂点間を連結することで、その他の奇数頂点間のとの距離が2ずつ縮まるためです。

全体のソースコードを記載します。

```python
from collections import defaultdict
import math
import sys
sys.setrecursionlimit(10**7)

N, M = map(int, input().split())
colors = [-1 for _ in range(N)]

G = defaultdict(lambda: [])
for i in range(M):
    u, v = map(int, input().split())
    u -= 1
    v -= 1
    G[u].append(v)
    G[v].append(u)

def dfs(u, color):

    colors[u] = color
    for v in G[u]:
        if colors[u] == colors[v]:
            return False
        if colors[v] == -1 and not dfs(v, 1^color):
            return False

    return True

ans = 0
is_bipartie = dfs(0, 1)
if is_bipartie:
    w_count = len([color for color in colors if color == 1])
    b_count = len([color for color in colors if color == 0])
    ans = w_count * b_count  - M
else:
    ans = N * (N-1) // 2 - M
print(ans)
```

# 5. その他二部グラフの問題

- [https://atcoder.jp/contests/abc126/tasks/abc126_d](https://atcoder.jp/contests/abc126/tasks/abc126_d)
- [https://atcoder.jp/contests/code-festival-2017-qualb/tasks/code_festival_2017_qualb_c](https://atcoder.jp/contests/maximum-cup-2018/tasks/maximum_cup_2018_c)
- [https://atcoder.jp/contests/arc041/tasks/arc041_d](https://atcoder.jp/contests/arc041/tasks/arc041_d)
- [http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=2370](http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=2370)

