# 基础概念

> \[!TODO] 约定\
> 本课程中使用的`Convex`代表$f^{''}(x)\geq 0$,`Concave`表示$f^{''}(x)\leq 0$

## 熵

### 熵的定义

> \[!SUCCESS] 前置知识:大数定理\
> 伯努利大数定理:$f\_A$是$n$次独立重复实验中事件$A$发生的次数,$p$是每次实验中$A$发生的概率,则对于任意正数$\epsilon$有:$$\underset{n\to\infty}{lim}P\{|\frac{f_A}{n}-p|<\epsilon\}=1$$\
> 即n趋于无穷大时,概率收敛于频率

现有$$X\in \{x_1,x_2,...x_n\} \overset{w.p.}{\sim}\{p_1,p_2...p_3\}$$有个长度为$M$的序列,由$X$组成,那么由大数定理,每个$x\_i$出现的次数为

$$
\begin{cases}
x_1\sim Mp_1\\
x_2\sim Mp_2\\
...\\
x_n\sim Mp_n
\end{cases}
$$

那么这个序列出现的概率为$$(p_1)^{Mp_1}(p_2)^{Mp_2}...(p_n)^{Mp_n}$$那么这样的序列有(类似于排列组合):$$\dfrac{1}{\prod_{i=1}^N(p_i)^{Mp_i}}$$\
最后取个对数就可以得到**熵**$$H(\mathbf{X})=\sum_{n=1}^{N}p_n\log(\frac{1}{p_n})=E[log\frac{1}{p_n}]$$考虑两种情况:

1. 什么时候熵最大
2. 什么时候熵最小

### 最大化熵

结论是:**均匀分布**的熵最大

> \[!SUCCESS] 前置知识:Jensen不等式及函数凹凸性\
> 二阶导大于0即为Convex函数,反之为Concave函数\
> Jensen不等式:若$f(x)$为区间$I$上的Concave函数,则对于任意的$x\_i\in I$和满足$\sum\_{i=1}^{n}\lambda\_i = 1$的$\lambda\_i>0 ,i=1,2...n$成立则有:$$\sum_{i=1}^{n}\lambda_i f(x_i)\leq f(\sum_{i=1}^{n}\lambda_i x_i)$$

> \[!NOTE] Proof\
> 即证$\sum\_{n=1}^{N}p\_n\log \frac{1}{p\_n}\leq \log N$当且仅当$p\_n=\frac{1}{N}$时取$=$\
> 由Jensen不等式,因为$log\_2(x)$为Concave函数,令$\lambda\_i=p\_i,x\_i=\frac{1}{x\_i},f(x)=log(x)$,则有$$\sum_{i=1}^{n}p_i log(\frac{1}{p_i})\leq log(\sum_{i=1}^{n}p_i\frac{1}{p_i})=logN$$,当且仅当$p\_i=\frac{1}{N}(i=1,2,...n)$时取等号,即均匀分布时取等号

Jensen不等式中常用的函数:$\log x$(Concave函数),$x\log x$(Convex函数)

### 最小化熵

先规定$0\log 0 = 0$\
因为$0\leq p\_i \leq 1$,那么$p\_i\log \frac{1}{p\_i}\geq 0$,那么$H(\mathbf{X})=\sum\_{n=1}^{N}p\_n\log(\frac{1}{p\_n})\geq 0$，当存在$1\leq i \leq n,s.t.p\_i=1 \quad and \quad p\_j=0,1\leq j \leq n,j \neq i$ 时取等

### 联合熵

二维的熵:$H(\mathbf{X},\mathbf{Y})=\sum\_{x,y}p(x,y)log\frac{1}{p(x,y)}=E\[log\frac{1}{p(x,y)}]$\
推广至高维:联合熵:$$H(\mathbf{X_1},...\mathbf{X_n})=\sum_{x_1...x_n}p(x_1...x_n)\log \frac{1}{p(x_1...x_n)}$$\
最大熵和最小熵的情形同一维

### 条件熵

给定$X$条件下$Y$的熵为

$$$
\begin{equation}
\begin{aligned}
H(Y|X) &=\sum_{x}p(x)H(Y|X=x) \\
&=\sum_{x}p(x)\sum_{y}p(y|x)\log(\frac{1}{p(y|x)})\\
&=\sum_{x,y}p(x,y)\log(\frac{1}{p(y|x)})\\
&=E[\log \frac{1}{p(y|x)}]
\end{aligned}
\end{equation}$$
当$X$和$Y$相互独立时$H(Y|X)=H(Y)$
**链式法则**:$$H(X,Y)=H(X)+H(Y|X)=H(Y)+H(X|Y)$$
> [!NOTE] Proof
> 右式=$\sum_{x}p(x)\log(\frac{1}{p(x)})+\sum_{x,y}p(x,y)\log(\frac{1}{p(y|x)})$,可以看出这是一个一维求和和二维求和相加,对于前面那一项中的$p(x)$,将其写成边缘分布的形式$p(x)=\sum_{y}p(x,y)$,代进去有$$\begin{equation}
> \begin{aligned}
> &\sum_{x}\sum_{y}p(x,y)\log(\frac{1}{p(x)})+\sum_{x,y}p(x,y)\log(\frac{1}{p(y|x)})\\
> &=\sum_{x}\sum_{y}p(x,y)\log(\frac{1}{p(x)})+\sum_{x,y}p(x,y)\log(\frac{p(x)}{p(x,y)})\\
> &=\sum_{x,y}p(x,y)\log (\frac{1}{p(x,y)})\\
> &=H(X,Y)
> \end{aligned}
> \end{equation}$$

一般形式:$$H(X_1,X_2...,X_n)=H(X_1)+H(X_2|X_1)+H(X_3|X_2,X_1)+...+H(X_n|X_{n-1},X_{n-2}...X_1)$$
> [!NOTE] Proof
> 利用条件概率:$$
> P(x_1,x_2...x_n)=P(x_1)P(x_2|x_1)...P(x_n|x_{n-1}...x_1)$$
> $$\log \frac{1}{P(x_1,x_2...x_n)} = \log \frac{1}{P(x_1)}+\log \frac{1}{P(x_2|1)}+...+\log \frac{1}{P(x_n|x_{n-1}...x_1)}$$
> $$E[\log \frac{1}{P(x_1,x_2...x_n)}] = E[\log \frac{1}{P(x_1)}]+E[\log \frac{1}{P(x_2|1)}]+...+E[\log \frac{1}{P(x_n|x_{n-1}...x_1)}]$$
> 即$$H(X_1,X_2...,X_n)=H(X_1)+H(X_2|X_1)+H(X_3|X_2,X_1)+...+H(X_n|X_{n-1},X_{n-2}...X_1)$$

**重要不等式**:$$H(Y)\geq H(Y|X)$$
> [!NOTE] Proof1
> $$\begin{equation}
> \begin{aligned}
> H(Y|X)&=\sum_{x}p(x)\sum_{y}p(y|x)\log(\frac{1}{p(y|x)})\\
> &=\sum_{x}\sum_{y}p(x)[p(y|x)\log(\frac{1}{p(y|x)})]
> \end{aligned}
> \end{equation}
> $$
> 此时考虑函数$x\log(\frac{1}{x})$为凹函数,由Jensen不等式:
> $$
> \begin{equation}
> \begin{aligned}
> H(Y|X)&\leq \sum_{y}[\sum_{x}p(x)p(y|x)]\log(\frac{1}{\sum_{x}p(y|x)p(x)})\\
> &=\sum_{y}p(y)\log(\frac{1}{p(y)})\\
> &=H(Y)
> \end{aligned}
> \end{equation}
> $$

> [!NOTE] Proof2
>  $$\begin{equation}
> \begin{aligned}
> H(Y)-H(Y|X)&=E[\log(\frac{1}{p(y)})]-E[\log(\frac{1}{p(y|x)})]\\
> &=E[\log(\frac{p(x,y)}{p(x)p(y)})]
> \end{aligned}
> \end{equation}
> $$
> 若要证明上式大于0,那么就证明$E[\log(\frac{p(x)p(y)}{p(x,y)})]\leq 0$,又由换底公式得:$E[\log(\frac{p(x)p(y)}{p(x,y)})]=E[\ln(\frac{p(x)p(y)}{p(x,y)})]\leq 0$
> 由常用不等式$\ln x\leq x-1$,$E[\ln(\frac{p(x)p(y)}{p(x,y)})]\leq E[\frac{p(x)p(y)}{p(x,y)}-1]$,对于$E[\frac{p(x)p(y)}{p(x,y)}]$有
> $$\begin{equation}
> \begin{aligned}
>E[\frac{p(x)p(y)}{p(x,y)}] &= \sum_{x,y}p(x,y)\frac{p(x)p(y)}{p(x,y)}\\
>&=\sum_{x,y}p(x)p(y)\\
>&=(\sum_x p(x))(\sum_y p(y))=1
> \end{aligned}
> \end{equation}
> $$
> 所以$E[\frac{p(x)p(y)}{p(x,y)}-1]=0$,$E[\log(\frac{p(x)p(y)}{p(x,y)})]=E[\ln(\frac{p(x)p(y)}{p(x,y)})]\leq 0$成立,所以$E[\log(\frac{p(x,y)}{p(x)p(y)})]\geq 0$,则$H(Y)\geq H(Y|X)$

## 几个熵之间的关系
![[Pasted image 20250227215859.png]]

## Renyi 熵
$$R(q)=\dfrac{\log(\sum_{n=1}^{N}p_n^q)}{1-q}$$
有几点性质:
1. $q=0,R(q)=\log N$
2. $q=1,R(q)$等价于香农熵
3. $R(q)$对于$q$单调递减
> [!SUCCESS] 前置知识:Cauchy不等式的离散形式
> 对于任意实数序列{$a_i$},{$b_i$},有:
> $$(\sum_{i=1}^na_i^2)(\sum_{i=1}^nb_i^2)\geq (\sum_{i=1}^na_ib_i)^2$$

> [!NOTE] Proof1
>对于性质1,显然
>性质2:$$\begin{equation}
>\begin{aligned}
>&\underset{q\to 1}{\lim}\dfrac{\log(\sum_{n=1}^{N}p_n^q)}{1-q}\\
>&\overset{L'Hospital}{=}\underset{q\to 1}{\lim}-\dfrac{\sum_{n=1}^Np_n^q\ln p_n}{\sum_{n=1}^Np_n^q\ln 2}\\
>&=-\sum_{n=1}^Np_n\log_2 p_n=H(p)
>\end{aligned}
>\end{equation}$$
>性质3:不妨先记$f(q)=\log(\sum_{n=1}^{N}p_n^q)$,$R(q)=\dfrac{\log(f(q))}{1-q}$,对$R(q)$求导以观察其单调性:$R'(q)=\dfrac{\frac{f'(q)}{f(q)\ln 2}(1-q)+\log f(q)}{(1-q)^2}$,求导后和0的关系不是那么显然,所以不妨记$g(q)=\log f(q)$,那么分子就可以化成$g'(q)(1-q)+g(q)$,我们继续对$g(q)$进行研究,$g'(q)=\dfrac{f'(q)}{f(q)\ln 2},g''(q)=\dfrac{f''(q)f(q)-[f'(q)]^2}{(f(q))^2ln2}$,不难求出$f'(q)=\sum_{n=1}^Np_n^q\ln p_n,f''(q)=\sum_{n=1}^Np_n^q(\ln p_n)^2$,由Cauchy不等式,令$a_i=p_i^{q_i/2}\ln p_i,b_i=p_i^{q_i/2}$则有:$$(\sum_{n=1}^Np_i\ln p_i)(\sum_{n=1}^Np_i)\geq (\sum_{n=1}^Np_i(\ln p_i)^2)^2$$
>所以$g''(q)\geq 0$,所以$g(q)$是convex的,所以$g'(q)$单调递增
>接下来分情况讨论
>1.$q<1$时:
>取任意$t\in [q,1]$,有$g'(t)\geq g'(q)$,利用积分不等式:
>$$\begin{equation}
>\begin{aligned}
>g(q)=\int_1^{q}g'(t)dt \leq \int_1^{q}g'(q) dt = g'(q)(q-1)
>\end{aligned}
>\end{equation}$$
>所以$g(q)\leq g'(q)(q-1)$所以$(1-q)g'(q)+g(q)\leq (1-q)g'(q)+(q-1)g'(q)=0$
>2.$q>1$时:
>取任意$t\in [1,q]$,有$g'(t)\leq g'(q)$,利用积分不等式:
>$$g(q)=\int_1^{q}g'(t)dt \leq \int_1^{q}g'(q) dt = g'(q)(q-1)$$
>代入得$(1-q)g'(q)+g(q)\leq (1-q)g'(q)+g'(q)(q-1)=0$
>因为$(1-q)^2$恒正,所以$R'(q)\leq 0$所以$R(q)$对$q$单调递减


## 互信息
$I(X;Y)$表示$X$中包含$Y$的熵(不确定度)(交换$X,Y$也成立)
$$\begin{equation}
\begin{aligned}
I(X;Y)&=H(Y)-H(Y|X) \geq 0\\
&=H(X)-H(X|Y) \geq 0
\end{aligned}
\end{equation}$$
特殊情况:
- $X,Y$统计独立,则$I(X,Y)=0(H(Y|X)=H(Y))$
- $X=Y$,$I(X,Y)=H(X)=H(Y)$
同时$I(X,Y)$也可以表征信道容量
$I(X;Y)=E[\log\frac{P(X,Y)}{P(X)P(Y)}]$,记$i(X;Y)=\log\frac{P(X,Y)}{P(X)P(Y)}$表示信息密度,$I(X;Y)=E[i(X;Y)]$
$i(X;Y)$的方差表示信号的色散:$$D=\sum_{x}P(x)Var[i(x;y)|P(y|x)]$$表征传输的差异性
### 条件互信息
$$I(X;Y|Z)=H(X|Z)-H(X|Y,Z)$$
![pic][https://wiki.swarma.org/images/7/7a/VennInfo3Var.svg.png]
### 互信息的链式法则
$$I(X_1,X_2...X_n;Y)=I(X_1;Y)+I(X_2;Y|X_1)+......I(X_n;Y|X_{n-1}...X_1)$$
> [!NOTE] Proof1
> $$\begin{equation}
> \begin{aligned}
> I(X_1,X_2...X_n;Y) = H(X_1&,X_2...X_n)-H(X_1....X_n|Y)\\
> 其中H(X_1...X_n)=H(X_1)&+H(X_2|X_1)+...H(X_k|X_{k-1}...X_1)+...H(X_n|X_{n-1}...X_1)\\
> H(X_1...X_n|Y)=H(X_1|Y)&+H(X_2|X_1,Y)+...H(X_k|X_{k-1}...X_1,Y)+...H(X_n|X_{n-1}...X_1,Y)\\
> 逐项相减得:
> H(X_1...X_n)-&H(X_1...X_n|Y) = I(X_1;Y)+I(X_2;Y|X_1)+...I(X_k;Y|X_{k-1}...X_1)+...+I(X_n;Y|X_n...X_1)
> \end{aligned}
> \end{equation}$$

## K-L距离
用于描述两个概率分布$p(x)$和$q(x)$之间的差异
定义:$p(x)$和$q(x)$之间的K-L距离为$$D(p||q)=\sum_xp(x)\log\frac{p(x)}{q(x)}$$
有以下几点性质
- $D(p||q)\geq 0$
- $D(p||q)\neq D(q||p)$
> [!NOTE] Proof1
> 对第一条性质进行证明:
> - 法1:首先$f(x)=\log x$是concave的,由Jensen不等式:$$\sum_xp(x)\log\frac{q(x)}{p(x)}\leq \log (\sum_xp(x)\frac{q(x)}{p(x)})=0$$所以$D(p||q)\geq 0$
> - 法2:利用不等式$ln x\leq x-1$有$$\sum_xp(x)\log\frac{q(x)}{p(x)}\leq \sum_x(q(x)-p(x))=0$$所以$D(p||q)\geq 0$

### 条件K-L距离
$$\begin{equation}\begin{aligned}D(p(y|x)||q(x|y)|p(x))&=\sum_xp(x)D(p(y|x)||q(y||x))\\&=\sum_xp(x)\sum_yp(y|x)\log\frac{p(y|x)}{q(y|x)}\end{aligned}\end{equation}$$
有以下几点性质:
- $D(p(y|x)||q(x|y)|p(x))=D(p(y|x)p(x)||q(y|x)p(x))$
- $D(p(x,y)||q(x,y))=D(p(y|x)||q(x|y)|p(x))+\underset{先验概率分布的KL距离}{D(p(x||q(x)))}$
- $D(p(x,y)||q(x,y))\geq D(p(x)||q(x))$
- $D(p(x_1...x_n)||q(x_1...x_n))=\sum_{i=1}^nD(p(x_i|x_1...x_{i-1})||q(x_i||x_1...x_{i-1})|p(x_1...x_{i-1}))$
- 若$$\begin{equation}
\begin{cases}
p(y)\sim p(y|x)p(x)\\
q(y)\sim q(y|x)q(x)
\end{cases}
\end{equation}$$
则$D(p(y)||q(y))\leq D(p(y|x)||q(y|x)|p(x))$
> [!NOTE] Proof1
> - 性质1:$$\begin{equation}\begin{aligned}
> D(p(y|x)||q(x|y)|p(x))&=\sum_xp(x)\sum_yp(y|x)\log\frac{p(y|x)}{p(x|y)}\\
> &=\sum_{x,y}p(y|x)p(x)\log\frac{p(y|x)p(x)}{p(x|y)p(x)}\\
> &=D(p(y|x)p(x)||q(y|x)p(x))
> \end{aligned}
> \end{equation}$$
> - 性质2:$$\begin{equation}\begin{aligned}
> 右式&=\sum_{x,y}p(y|x)p(x)\log\frac{p(y|x)p(x)}{p(x|y)p(x)}+\sum_{x,y}p(x,y)\log\frac{p(x)}{q(x)}\\
> &=\sum_{x,y}p(x,y)\log\frac{p(y|x)p(x)}{q(y|x)q(x)}\\
> &=\sum_{x,y}p(x,y)\log\frac{p(x,y)}{q(x,y)}=D(p(x,y)||q(x,y))
> \end{aligned}
> \end{equation}$$
> - 性质3:$$\begin{equation}\begin{aligned}
> D(p(y|x)||q(x|y)|p(x)),结合性质2即可推出
> \end{aligned}
> \end{equation}$$
> - 性质4:$$\begin{equation}\begin{aligned}
> TBA
> \end{aligned}
> \end{equation}$$
> - 性质5:$$\begin{equation}\begin{aligned}
> 由性质2可得:\\
> D(p(x,y)||q(x,y))&=D(p(y|x)||q(y|x)|p(x))+\underset{=0}{\underline{D(p(x)||p(x))}}\\
> &=\underset{\geq 0}{\underline{D(p(x,y)||q(x,y)|q(y))}}+D(p(x)||q(y))\\
> D(p(y|x)|&|q(y|x)|p(x))  \geq D(p(y)||q(y))
> \end{aligned}
> \end{equation}$$
$$$
