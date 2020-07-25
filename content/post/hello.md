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


