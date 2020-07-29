---
title: "現代数理統計学の基礎　演習問題1章解説"
date: 2020-07-24T00:27:17+09:00
draft: false
---
本記事では「現代数理統計学の基礎」における1章の演習問題を解説する。  
```
※本記事の解説内容は、厳密にレビューしたものではないため、誤りを含む可能性あり。
```

## 問1
$$
A{\Delta}B = (A{\backslash}B){\cup}(B{\backslash}A)  \\\\\\
           = (A{\cap}B^c){\cup}(B{\cap}A^c) \\\\\\
           = ((A{\cap}B^c){\cup}B){\cap}((A{\cap}B^c){\cup}A^c) \\\\\\
           = (A{\cup}B){\cap}(A^c{\cup}B^c) \\\\\\
           = (A{\cup}B){\cap}(A{\cap}B)^c \\\\\\
           =(A{\cup}B){\backslash}(A{\cap}B) \\\\\\
$$
***

## 問2
$$
P(A{\cup}B) = P(A)+ P(B)-P(A{\cap}B)を活用する。
$$
$$
P(A_1{\cup}A_2{\cup}A_3) = P(A_1{\cup}(A_2{\cup}A_3)) \\\\\\
        = P(A_1) + P(A_2{\cup}A_3) - P(A_1{\cap}(A_2{\cup}A_3)) \\\\\\
        = P(A_1) + P(A_2) + P(A_3)-P(A_2{\cap}A_3) - P(A_1{\cap}(A_2{\cup}A_3)) \\\\\\
        = P(A_1) + P(A_2) + P(A_3)-P(A_2{\cap}A_3) - P((A_1{\cap}A_2) {\cup}(A_1{\cap}A_3)) \\\\\\
        =P(A_1) + P(A_2) + P(A_3)-P(A_2{\cap}A_3) - P(A_1{\cap}A_2) - P(A_1{\cap}A_3) +  P((A_1{\cap}A_2) {\cap}(A_1{\cap}A_3))\\\\\\
        =P(A_1) + P(A_2) + P(A_3)-P(A_1{\cap}A_2) - P(A_2{\cap}A_3) - P(A_3{\cap}A_1) +  P(A_1{\cap}A_2 {\cap}A_3) \\\\\\
$$
***

## 問3
$$
P(A_1{\cap}{\cdots}{\cap}A_n) = P((A_1{\cap}{\cdots}{\cap}A_{n-1}){\cap}A_n) \\\\\\
        = P(A_n | A_1{\cap}{\cdots}{\cap}A_{n-1}) * P(A_1{\cap}{\cdots}{\cap}A_{n-1}) \\\\\\
        = P(A_n | A_1{\cap}{\cdots}{\cap}A_{n-1}) * P((A_1{\cap}{\cdots}{\cap}A_{n-2}){\cap}A_{n-1}) \\\\\\
        = P(A_n | A_1{\cap}{\cdots}{\cap}A_{n-1}) * P(A_{n-1}|A_1{\cap}{\cdots}{\cap}A_{n-2}) * P(A_1{\cap}{\cdots}{\cap}A_{n-2}) \\\\\\
        同様にして \\\\\\
        = P(A_n | A_1{\cap}{\cdots}{\cap}A_{n-1}) * {\cdots} * P(A_2|A_1) * P(A_1) \\\\\\
$$
***

## 問5
(1)
0を受信する確率は以下の2通りが考えられる。  
・「送信者が0を送信する」かつ「送信者が正しく送信する」  
・「送信者が1を送信する」かつ「送信者が誤って送信する」  
よって  
$$
0を受信する確率 = {\frac{1}{3}} * {\frac{1}{10}}+\frac{2}{3}*\frac{9}{10} = \frac{11}{30}
$$

(2)
0を受信する確率をP(0)、1が送信される確率をP(1)、受信したデータが誤っている確率をP(誤)とする。  
また、1を送信する確率と受信したデータが誤っている確率は独立であるため、  
$$
P(誤{\cap}1) = P(誤) * P(1)
$$
よって
$$
P(誤|0) = \frac{P(誤{\cap}P(1))}{P(0)} 
        = \frac{P(誤)*P(1)}{P(0)} 
        = \frac{ \frac{1}{10} * \frac{2}{3}}{\frac{11}{30}} 
        = \frac{2}{11}
$$

$$
同様にして
P(誤|1) = \frac{P(誤{\cap}P(0))}{P(1)} 
        = \frac{ \frac{1}{10} * \frac{1}{3}}{\frac{19}{30}} 
        = \frac{1}{19}
$$

***


## 問8
確率の劣加法性より
$$
P(\cup_{k=1}^{\infty}A_k) \leq \sum_{k=1}^{\infty}P(A_k) \\\\\\
$$
すなわち
$$
P(\cup_{k=1}^{\infty}A_k^c) \leq \sum_{k=1}^{\infty}P(A_k^c) \\\\\\
ド・モルガンの法則より、左辺を変形して \\\\\\
P((\cap_{k=1}^{\infty}A_k)^c) \leq \sum_{k=1}^{\infty}P(A_k^c) \\\\\\
1 - P(\cap_{k=1}^{\infty}A_k) \leq \sum_{k=1}^{\infty}P(A_k^c) \\\\\\
よって \\\\\\
P(\cap_{k=1}^{\infty}A_k) \geq 1 - \sum_{k=1}^{\infty}P(A_k^c) \\\\\\
$$