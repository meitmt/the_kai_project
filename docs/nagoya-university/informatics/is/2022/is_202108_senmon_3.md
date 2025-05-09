---
sidebar_label: "2021年8月実施 専門 問3"
tags:
  - Nagoya-University
  - Median-Of-Medians
---
# 名古屋大学 情報学研究科 情報システム学専攻 2021年8月実施 専門 問3

## **Author**
祭音Myyura

## **Description**
自然数の有限列のうち、含まれている要素が重複しないものを考える。
そのような列 $S$ に含まれる要素のうちで $k$ 番目に小さい数（小さい方から数えて $k$ 番目の数）を求める再帰的アルゴリズム select（図1）について以下の問いに答えよ。
なお、$|X|$ は有限列 $X$ の要素数を表し、$\lceil \ \rceil$ は天井関数を表す。
天井関数は引数として受け取る実数 $r$ に対して、$x$ 以上の最小の整数を返す。
さらに、有限列 $X$ の中位数は $X$ の中で $\lceil \frac{|X|}{2} \rceil$ 番目に小さい要素とする。

(1) $S$ を以下の列、$k$ を $10$ とする。

$$
11, 12, 16, 33, 2, 18, 39, 15, 21, 7, 37, 29, 40, 6, 25, 27, 14, 4, 35, 28, 22, 20, 17, 3, 1
$$

- (a) このような $S、k$ に対して図 1 の手順の 1. から 5. を順に実行したときに求められる手順の中の列 $M$、自然数 $x$、列 $A$ を示せ。なお、列 $A$ の要素の並び順についてはアルゴリズムでは言及していないので、解答では並び順を問わない。

- (b) このような $S、k$ に対して select($S$,$k$) を実行したときの出力を答えよ。

(2) $n = |S|$ とし、$n$ を $10$ の倍数としたときに列 $A$ に含まれる得る要素の数の最小値と最大値それぞれをnを用いた式で表せ。

(3) $n = |S|$ とする。図 1 の手順において、2. における列 $G_1, \ldots, G_N$ を得る操作、5. における列 $A, B$ を得る操作の最大時間計算量をそれぞれ $O(n)$ とする。このとき、select($S$,$k$)（ただし、$0 < k \leq n$ ）を実行したときの最大時間計算量をオーダー記法で示せ。解答では $|S|$ でない $n$ を用いること。

(4) 以下の整列アルゴリズムを考える。

```text
(a) バブルソート        (b) マージソート        (c) ヒープソート
(d) クイックソート      (e) 挿入ソート          (f) バケットソート
```

(a)〜(f) のうち、入力として与えられる列の要素数を $n$ としたときに以下の条件をすべて満たすものを1つ選択せよ。

- 最大時間計算量が $O(n^2)$ である。
- 図 1 のアルゴリズムを利用することで最大時間計算量を $O(n \log n)$ に改善できる。

---------------------------

<u> 再帰的アルゴリズム select </u>

**入力** 重複する要素を持たない自然数の有限列 $S$、正整数 $k$（ただし、$k \leq |S|$）

**出力** 列 $S$ に含まれる要素のうちで $k$ 番目に小さいもの

**手順**

1. $N$ を $\lceil \frac{|S|}{5} \rceil$ とする。
2. 列 $S$ を先頭から順に要素5つずつの列 $G_1, \ldots, G_N$ に分ける。つまり、列 $G_1$ から列 $G_N$ を順に連結すると列 $S$ に一致する。さらに、列 $G_1, \ldots, G_{N-1}$ それぞれに含まれる要素数は5であり、$|S|$ が $5$ の倍数ではないときに列 $G_N$ の要素数は5に満たない。
3. $M$ を列 $G_1, \ldots, G_N$ それぞれの中央値からなる列とする。なお、列 $M$ の要素の並び順は先頭から順に列 $G_1, \ldots, G_N$ の中央値が並んでいるとする。
4. $x$ を列 $M$ の中央値、すなわち、select($M$, $\lceil \frac{|M|}{2} \rceil$) の返り値とする。
5. 列 $A, B$ を以下を満たす列とする。

$$
\{a \mid a \text{ は列 } A \text{ に含まれる要素 }\} = \{y \in S \mid y < x\}
$$

$$
\{b \mid b \text{ は列 } B \text{ に含まれる要素 }\} = \{y \in S \mid x < y\}
$$

6. $|A| = k - 1$ のときは $x$ を返して終了し、そうでないときは次に進む。
7. $|A| \geq k$ のときは select($A$, $k$) の返り値を返して終了し、そうでないときは次に進む。
8. select($B$, $k - |A| - 1$) の返り値を返して終了する。

---------------------------

#### <center> 図 1: $k$ 番目に小さい要素を求めるアルゴリズム


## **Kai**
図１の再帰的アルゴリズム select は「中央値の中央値 (median of medians)」と呼ばれ、クイックセレクトに基づく選択アルゴリズムである。

### (1)
#### (a)
```text
S = [11, 12, 16, 33, 2, 18, 39, 15, 21, 7, 37, 29, 40, 6, 25, 27, 14, 4, 35, 28, 22, 20, 17, 3, 1]

M = [12, 18, 29, 27, 17]

x = 18

A = [11, 12, 16, 2, 15, 7, 6, 14, 4, 17, 3, 1]
```

#### (b)
15

### (2)
$\frac{n}{5}$ 個の小配列に分割した時、その小配列のうち半数 ($\frac{n}{5} \times \frac{1}{2} = \frac{n}{10}$ 個) の小配列では、各小配列の中央値が $x$ の値（中央値の中央値）以下である。

また、各小配列の中には、必ず各中央値以下である要素が $3$ 個存在する。
よって、全体としては、$\frac{3n}{10}$ 個の要素が $x$ の値以下である。

同様に、もう半数の小配列には、$x$ の値以上の要素が少なくとも $3$ 個以上存在するはずなので、全体としては、$\frac{3n}{10}$ 個の要素が $x$ の値以上である。

従って、列 $A$ に含まれ得る要素の数の最大値が $\frac{7n}{10}$ であり、最小値は $\frac{3n}{10} - 1$ ($x$ 自身を除く) である。

### (3)
**（$n$ を $10$ の倍数としたときの計算量を証明する。一般的の場合は、CLRS を参照してください。）**

select($S$, $k$) の最大時間計算量を $T(n)$ とすると、$T(n) \leq cn \ (c > 0)$ が満たすことを $n$ の大きさに関する帰納法で示す。

$n$ が十分大きいとき、(2) より

$$
\begin{aligned}
T(n) &\leq T \left (\frac{1}{5}n \right) + \Theta(n) + T \left( \frac{7}{10}n \right) \\
&\leq c \frac{n}{5} + c\frac{7n}{10} + an \qquad (\text{帰納法の仮定、} a > 0 \text{ は定数}) \\
&= c\frac{9n}{10} + an
\end{aligned} 
$$

であり、$c = 10a$ とおくと、

$$
c\frac{9n}{10} + an = 10an \leq cn
$$

であるので、$T(n) = O(n)$ がわかる。

### (4)
(d) クイックソート