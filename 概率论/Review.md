> 和所有的数学科目一样，概率论也是每章环环相扣的，这里边梳理边复习，对一些遗忘的内容重新认识。

#### 目录

- ###### [第一章：随机事件与概率](#随机事件与概率)
  
  - [第一节：随机事件及其运算](#随机事件及其运算)
  - [第二节：概率的定义及其确定方法](#概率的定义及其确定方法)
  - [第三节：概率的性质](#概率的性质)
  - [第四节：条件概率](#条件概率)
  - [第五节：独立性](#独立性)
  
- ###### [第二章：随机变量及其分布](#随机变量及其分布)
  
  - [第一节：随机变量及其分布](#随机变量及其分布)
  - [第二节：随机变量的数学期望](#随机变量的数学期望)
  - [第三节：随机变量的方差和标准差](#随机变量的方差和标准差)
  
- ###### [第三章](#第三章)

------

##### 随机事件与概率

###### 随机事件及其运算

样本空间 $\Omega$ 和样本点 $\omega$ , 样本空间至少含有两个样本点（有限和无限，离散和连续）
	对立事件的充要条件是 $A \cap B = \emptyset$ , 且 $A \cup B = \Omega$ 
	事件域 $f$ 为 $\Omega$ 的某些子集组成的集合类，需要满足的条件是:

1. $\Omega \in f$
2. 若 $A \in f$， 则 $\overline{A} \in f$
3. 若 $A_n \in f, n=1,2,···$， 则可列并 $\cup_{i=0}^ \infty A_n \in f$

又称 $\sigma$ 域或 $\sigma$ 代数

扩展：（前提是 $A_n \in f, n=1,2,3···$）

1. 由1可得 $\empty \in f$

2. 由3可得，取 $A_n= A_{n+1}=···=empty$，可得有限并$\cup_{i=0}^n A_i \in f$，

3. 由2可得，$\overline{A_1}, \overline{A_2}, ···，\overline{A_n} \in f$，$\cup_{i=0}^n \overline{A_i} \in f$   =>  $\overline{\cup_{i=0}^n \overline{A_i}} \in f$，即由德摩根公式可得有限交  $\cap_{i=0}^n A_i \in f$
4. 由2可得，$\overline{A_1}, \overline{A_2}, ···，\overline{A_n},··· \in f$， 由3可得，$\cup_{i=0}^\infty \overline{A_i} \in f$，再由2可得$\overline{\cup_{i=0}^\infty \overline{A_i}} \in f$，即由德摩根公式可得可列交  $\cap_{i=0}^\infty A_i \in f$
5. 由2可得，$\overline{A_2} \in f$，由第三扩展可得 $A_1\overline{A_2} \in f$，即 $A_1 - A_2 \in f$

###### 概率的定义及其确定方法

1. 非负性 若 $A \in f$, 则 P(A) ≥ 0

2. 正则性 $P(\Omega)$  = 1

3. 可列可加性 若 $A_1, A_2, ···$互不相容，则 $P(\cup_{i=1}^\infty A_i)$ = $\sum_{i=0}^\infty P(A_i)$

   重复组合：从n个不同的元素中每次取出一个，放回后再取下一个，如此连取r次组合总数为 $(\begin{matrix}n+r-1 \\ r\end{matrix})$

    $(\begin{matrix}n \\ r\end{matrix})$ =  $(\begin{matrix}n-1 \\ r-1\end{matrix})$+ $(\begin{matrix}n-1 \\ r\end{matrix})$

    $(\begin{matrix}n \\ 0\end{matrix})$+ $(\begin{matrix}n \\ 1\end{matrix})$+···+$(\begin{matrix}n \\ n\end{matrix})$ = $2^n$

    $(\begin{matrix}n \\ 1\end{matrix})$+ 2$(\begin{matrix}n \\ 2\end{matrix})$+···+n$(\begin{matrix}n \\ n\end{matrix})$ = n$2^{n-1}$

    $(\begin{matrix}a \\ 0\end{matrix})$$(\begin{matrix}b \\ n\end{matrix})$+$(\begin{matrix}a \\ 1\end{matrix})$$(\begin{matrix}b \\ n-1\end{matrix})$+···+ $(\begin{matrix}a \\ n\end{matrix})$$(\begin{matrix}b \\ 0\end{matrix})$ = $(\begin{matrix}a+b \\ n\end{matrix})$

    ${(\begin{matrix}n \\ 0\end{matrix})}^2$+ ${(\begin{matrix}n \\ 1\end{matrix})}^2$+···+${(\begin{matrix}n \\ n\end{matrix})}^2$ = $(\begin{matrix}2n \\ n\end{matrix})$

   前两个太简单就不证明了，第三个主要用了$r(\begin{matrix}n \\ r\end{matrix}) = n(\begin{matrix}n-1 \\ r-1\end{matrix})$

   ![image-20191229162737508](C:\Users\syz\AppData\Roaming\Typora\typora-user-images\image-20191229162737508.png)

   ![image-20191229162817302](C:\Users\syz\AppData\Roaming\Typora\typora-user-images\image-20191229162817302.png)
###### 概率的性质

有限可加性 与可列可加性类似 若 $A_1, A_2, ···, A_n$互不相容，则 $P(\cup_{i=1}^n A_i)$ = $\sum_{i=0}^n P(A_i)$

$P(A-B) = P(A) - P(AB)$

$P(A\cup B) = P(A)+P(B)-P(AB)$

概率为0的事件未必不可能  

求概率的时候切忌不能想当然！！！

###### 条件概率

乘法公式：
$$
P(AB) = P(B)P(A|B)
$$
全概率公式：设 $B_1,B_2,···,B_n$ 为样本空间 $\Omega$ 的一个分割，即互不相容且 $\cup_{i=1}^n B_i = \Omega$ ，如果 $P(B_i) > 0, i = 1,2,···,n$ ，则对任一事件A有
$$
P(A) = \sum_{i = 1}^n P(B_i)P(A|B_i)
$$
贝叶斯公式：设 $B_1,B_2,···,B_n$ 为样本空间 $\Omega$ 的一个分割，即互不相容且 $\cup_{i=1}^n B_i = \Omega$ ，如果 $P(A) > 0, P(B_i) > 0, i = 1,2,···,n$ ，则
$$
P(B_i|A) =\frac{P(B_i)P(A|B_i)}{\sum_{j = 1}^n P(B_j)P(A|B_j)} \space ,i = 1,2,···,n
$$

###### 独立性

若事件A与B独立，则A与 $\overline{B}$ 独立，$\overline{A}$ 与B独立，$\overline{A}$ 与 $\overline{B}$ 独立，证明从略，主要是证明 $P(A\overline{B}) = P(A)P(\overline{B})$: $P(A\overline{B})$ = P(A-B) = P(A)-P(AB)=P(A)-P(A)P(B)=P(A)P( $\overline{B}$ )

事件A,B独立是指这两个事件之间的概率满足一个等式：P(AB)=P(A)P(B)

事件A,B互不相容是指这两个事件之间的运算满足一个等式：AB=$\emptyset$

------

##### 随机变量及其分布

###### 随机变量及其分布

分布函数 $F(x) = P(X ≤ x)$:

1. 单调性
2. 有界性
3. 右连续性

离散随机变量的概率分布列：

1. 非负性 $p(x_i) ≥ 0, i = 1,2,···$
2. 正则性 $\sum_{i=0}^\infty p(x_i) = 1$

连续随机变量的概率密度函数：

$F(x)=\int_{-\infty}^x p(t)dt$        $p(x) = F'(x)$

1. 非负性 $p(x)≥0$
2. 正则性 $\int_{-\infty}^\infty p(x)dx=1 \space (含有p(x)的可积性)$

###### 随机变量的数学期望

离散随机变量 $E(x) = \sum_{i=0}^\infty x_ip(x_i)$

连续随机变量 $E(x)=\int_{-\infty}^\infty x p(x)dx$
$$
E[g(x)]=\begin{cases} \sum_{i}g(x_i)p(x_i)，在离散场合\\ \int_{-\infty}^\infty g(x) p(x)dx， 在连续场合\end{cases}
$$

###### 随机变量的方差和标准差



