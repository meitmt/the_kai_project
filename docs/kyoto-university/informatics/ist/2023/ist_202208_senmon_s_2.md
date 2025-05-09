---
sidebar_label: "2022年8月実施 専門科目 S-2"
tags:
  - Kyoto-University
---
# 京都大学 情報学研究科 知能情報学専攻 2022年8月実施 専門科目 S-2

## **Author**
[Isidore](https://github.com/heacsing)

## **Description**
### 設問1

確率変数 $X$ は下の確率密度変数 $f(x)$ をもつ確率分布に従うとする。

$$
f(x) = 
\left \{
\begin{aligned}
-\frac{1}{2}x + \frac{1}{2} \quad &(|x| \le 1) \\
0 \quad &(|x| > 1)
\end{aligned}
\right.
$$

$X$ の平均と分散を求めよ。

### 設問2

独立な確率変数 $X$ と $Y$ が、それぞれパラメータ $\lambda_1,\lambda_2$ のポアソン分布に従うとする。このとき、$Z = X + Y$ がパラメータ $(\lambda_1 + \lambda_2)$ のポアソン分布に従うことを示せ。パラメータ $\lambda$ のポアソン分布は下の確率質量関数で与えられる。

$$
P(X = k) = \frac{\lambda^k e^{-\lambda}}{k!}
$$

### 設問3

モデル $y_i = \beta x_i + \epsilon_i(i = 1,2,\dots,n;\epsilon_i \text{は誤差項})$　から生成されるデータ $(x_1,y_1),(x_2,y_2),\dots,(x_n,y_n)$ に、切片がゼロの回帰直線 $y = \hat{\beta}x$ を最小二乗法でフィッティングする。

(1) $\hat{\beta}$ 求めよ。

(2) $\hat{\epsilon_i} = y_i - \hat{\beta}x_i$ とおくと、$\sum_{i = 1}^n x_i\hat{\epsilon_i}$ が成り立つことを示せ。

### 設問4 

ある研究分野における全統計的仮説の中で、真の仮説 (帰無仮説が誤り) と偽の仮説 (帰無仮説が正しい) の数の比が $R:1$ であることがわかっているとする。

(1) ある仮説について実験を実施し、有意水準 $\alpha$ 、検出力 $1 - \beta$ で検定を行う。検定結果が有意であった場合にこの仮説が真である確率を、$R,\alpha,\beta$ を用いて表せ。また、$R = 0.1,\alpha = 0.05,\beta = 0.2$ のときの値を計算せよ。

(2) ある仮説について $k$ 回の独立な実験を実施し、それぞれについて(1)と同様の検定を行う。$k$ 回全ての実験について検定結果が有意であった場合にこの仮説が真である確率を、$R,\alpha,\beta,k$ を用いて表せ。また、$R = 0.1,\alpha = 0.05,\beta = 0.2,k = 2$ のときの値を計算せよ。


## **Kai**
### 設問1

$$
E[X] = \int^{1}_{-1}x(-\frac{1}{2}x+\frac{1}{2})\mathrm{d}x = -\frac{1}{3}
$$

$$
E[X^2] = \int^{1}_{-1}x^2(-\frac{1}{2}x+\frac{1}{2})\mathrm{d}x = \frac{1}{3} \\
$$

$$
\text{Var}[X] = E[X^2] - E^2[X] = \frac{2}{9}
$$

### 設問2
By the convolution Rule, we have

$$
\begin{align}
    f_{Z}(z) &= P(Z=z) = \sum^{z}_{i=0}f_{X}(i)f_{Y}(z-i) \\
    & = \sum^{z}_{i=0} \frac{\lambda_1^{i}e^{-\lambda_1}}{i!} \frac{\lambda_2^{z - i}e^{-\lambda_2}}{(z - i)!} \\
    & = \frac{e^{-(\lambda_1 + \lambda_2)}}{z!}\sum^{z}_{i=0}\frac{z!}{(z-i)!i!}\lambda_1^{i}\lambda_2^{z - i}
\end{align}
$$

By the Binomial Theorem, we can insert $\sum^{z}_{i=0}\frac{z!}{(z-i)!i!}\lambda_1^{i}\lambda_2^{z - i} = (\lambda_1 + \lambda_2)^z$

$$
f_{Z}(z) = \frac{e^{-(\lambda_1 + \lambda_2)}}{z!}(\lambda_1 + \lambda_2)^z
$$

So is the PMF for a Poisson Distribution with the parameter $(\lambda_1 + \lambda_2)$

**PS**: A easier solution is to use Moments Generating Function.

### 設問3

#### (1)
By the Least Square Method, we have the sum of square residuals,

$$
S(\hat{\beta}) = \sum^{n}_{i=1}(y_i - \hat{\beta}x_i)^2
$$

Calculate its derivative with the root

$$
\begin{align}
    S'(\hat{\beta}) &= \sum^{n}_{i=1}(-2x_i)(y_i-\hat{\beta}x_i) \\
    &= 2(\sum^{n}_{i=1}\hat{\beta}x_i^2 - \sum^{n}_{i=1}x_iy_i) \\
    \hat{\beta} &= \frac{\sum^{n}_{i=1}x_iy_i}{\sum^{n}_{i=1}x_i^2}
\end{align}
$$

#### (2)

By the equation ($5$) and ($6$), we immediately have

$$
\begin{align}
    0 &= (\sum^{n}_{i=1}\hat{\beta}x_i^2 - \sum^{n}_{i=1}x_iy_i) \\
    &= \sum^{n}_{i=1}x_i(y_i-\hat{\beta}x_i) \\
    &= \sum^{n}_{i=1}x_i\hat{\epsilon_i} 
\end{align}
$$

### 設問4

#### (1)
Denote the events below:

- The hypothesis is true: $T$
- The hypothesis is false: $F$
- The test results in significance: $S$

Then, what is asked can be represented by the probability as $Pr[T|S]$.
Given the ratio $R:1$, we have

$$
Pr[T] = \frac{R}{R+1} ;\; Pr[F] = \frac{1}{R+1} 
$$

By the definition of Significance Level and Statistic Power, we have

$$
Pr[S|F] = \alpha ;\; Pr[S|T] = 1 - \beta
$$

Therefore, with the Bayes' theorem, we have

$$
\begin{align}
    Pr[T|S] &= \frac{Pr[S\cap T]}{Pr[S]} \\
    &= \frac{Pr[S|T]Pr[T]}{Pr[S|T]Pr[T]+Pr[S|F]Pr[F]} \\
    &=\frac{(1-\beta)R}{\alpha+(1-\beta)R}
\end{align}
$$

Insert the values, the answer is 

$$
Pr[T|S] = \frac{8}{13}
$$

#### (2)
By perform the experiments $k$ times independently, we only need to multiply the probabilities with event $S$ $k$ times in equation ($11$), which means,

$$
\begin{align}
    Pr[T|S^k] &= \frac{Pr[S^k|T]Pr[T]}{Pr[S^k|T]Pr[T]+Pr[S^k|F]Pr[F]} \\
    &= \frac{Pr^k[S|T]Pr[T]}{Pr^k[S|T]Pr[T]+Pr^k[S|F]Pr[F]} \\
    &= \frac{(1-\beta)^kR}{\alpha^k+(1-\beta)^kR}
\end{align}
$$

Insert the values, the answer is

$$
Pr[T|S^2] = \frac{128}{133}
$$