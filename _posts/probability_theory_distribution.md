title: 常用分布及其性质
tags:
- 概率分布
- 期望
- 方差
- MathJax
categories:
- 课程学习
- 数理统计
comments: true
mathjax: true
description: 在学习数理统计的过程中，经常忘记各分布的期望与方差，百度后只找到图片或文档。现用MathJax的形式记录下这些公式，看得舒服。
---

## **常见分布的期望和方差：** ##

<style>
table th:nth-of-type(1) {
    width: 20%;
}
table th:nth-of-type(2) {
    width: 40%;
}
table th:nth-of-type(3) {
    width: 20%;
}
table th:nth-of-type(4) {
    width: 20%;
}
</style>

| 分布类型 | 概率密度函数 | 期望 | 方差 |
| :------: | :----------------------: | :------: | :------: |
| 0-1分布 B(1,p) |  | $p$ | $pq$ |
| 二项分布 B(n,p) | $ {p_i}=P\left\{X=i\right\}={C^{i}_{n}}{p^i}{q^{n-1}}  (q=1-p),(i=1,2,\ldots,n) $ | $np$ | $npq$ |
| 泊松分布 P($\lambda$) | $ p_{i}=P\left\{X=i\right\}=\frac{\lambda^{i}}{i!}e^{-\lambda } $ | $\lambda$ | $\lambda$ |
| 均匀分布 U(a,b) | $ f(x)=\frac{1}{b-a} $ | $\frac{1}{b-a}$ | $\frac{(b-a)^{2}}{12}$ |
| 正态分布 N($\mu$,$\sigma^{2}$) | $ f(x)=\frac{1}{\sqrt{2\pi}\sigma}e^{\frac{(x-\mu)^{2}}{2\sigma^{2}}} $ | $\mu$ | $\sigma^{2}$ |
| 指数分布 E($\lambda$) | $f(x)=\begin{cases}\lambda e^{-\lambda x},x> 0\\ 0,x\leq 0\end{cases}$ | $\frac{1}{\lambda}$ | $\frac{1}{\lambda^{2}}$ |
| 卡方分布 $\chi ^{2}(n)$ | $X_{1},X_{2}...X_{n}$相互独立,且都服从标准正态分布N(0,1)<br>$\chi _{2}=X_{1}^{2}+X_{2}^{2}+\cdots+X_{n}^{2}$ | $n$ | $2n$ |
| $t$分布 $t$(n) | $X\sim N(0,1)$&nbsp;$Y\sim x^{2}(n)$&nbsp;$t=\frac{X}{\sqrt{Y/n}}$ | 0 | $\frac{n}{n-2}(n\geq 2)$ |
| F分布 F($n_{1}$,$n_{2}$) | $X\sim \chi ^{2}(n_{1})$&nbsp;$X\sim \chi ^{2}(n_{2})$&nbsp;$F=\frac{X/n_{1}}{Y/n_{2}}$ | $\frac{n_2}{n_{2}-2}$ | $\frac{2n_{2}^{2}(n_{1}+n_{2}-2)}{n_{1}(n_{2}-2)^{2}(n_{2}-4)}$ |


## **参考链接：** ##



1、[简书：在Markdown中输入数学公式(MathJax)](https://www.jianshu.com/p/a0aa94ef8ab2)
2、[数学公式使用参考](https://www.cnblogs.com/q735613050/p/7253073.html)
3、[在线LaTeX公式编辑器](http://www.codecogs.com/latex/eqneditor.php)