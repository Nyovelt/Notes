---
description: ShanghaiTech University - Spring 2021
---

# EE 150: Signals and Systems

{% file src=".gitbook/assets/summary.pdf" caption="Summary from UCB" %}

## Basic concepts

### Signals and Systems

* **Signal**: a function of one or more independent variables \(e.g., time and spatial variables\); typically contains information about the behavior or nature of some physical phenomena
  * 信号是一系列独立变量
* **System**: responds to a particular signal input by producing another signal\(output\)
  * 系统是其一个信号进， 一个信号出

![A kind of signal](.gitbook/assets/image%20%281%29.png)

### Transformation

* Time reflection: x\(t\) ←→ x\(−t\), x\[n\] ←→ x\[−n\]
* Time scaling: x\(t\) ←→ x\(ct\)
* Time shift: x\(t\) ←→ x\(t − t0\), x\[n\] ←→ x\[n − n0\]
* Usually **do shift then scaling** to avoid complex mathematics

### Even and Odd functions

Every signal function is $$x(t) = Even(x) + Odd(t)$$ ,then

$$ x(-t) = Even(-t) + Odd(-t) = Even(t) - Odd(t) $$

$$ Even(t) = \frac12 ( x(t) + x(-t) ) $$

$$ Odd(t) = \frac12 ( x(t) - x(-t) )$$

### Periodic

* Preodic: $$ x(t) = x(t+mT)$$ or $$ x[t] = x[t+mT]$$ 
  * Fundamental period $$T$$:  Smallest positive $$T$$
  * 如果是合成的 signal, 其 Fundamental Period 是**最小公倍数**
* Aperiodic: Non-preodic

### Eular's Formula

$$ e^{j \omega0 t} = \cos ( \omega0 t ) + j \cdot \sin (\omega_0 t) $$

* Fundamental period $$T_0 = 2 \pi / \mid \omega _0 \mid$$ 
* $$A \cos (\omega0 t + \phi) = \frac A2 e^{j \phi} e^{j \omega_0 t} + \frac A2 e^{-j \phi} e^{-j \omega_0 t}$$
* 只要基础频率 $$ \omega_0$$ 一样， 指数和三角函数可以互相转化

### Sin

$$ x(t) = A \cos (\omega _0 t + \phi )$$

* unit: $$\omega_0$$
* radians: $$\phi$$
* phase: $$ \omega_0t+\phi$$

![Fundamantal Frequency&#xFF0C; &#x89D2;&#x9891;&#x7387;&#x8D8A;&#x5927;&#xFF0C; &#x632F;&#x8361;&#x8D8A;&#x5927;](.gitbook/assets/image%20%283%29.png)

### Discrete Time Unit Step and Unit Impulse Sequence

* $$ \delta[n]$$
  * 只有 $$n=0$$有正值

![](.gitbook/assets/image%20%285%29.png)

* $$ u[n]$$
  * 只有 $$ n \geq 0 $$有正值

![](.gitbook/assets/image%20%286%29.png)

$$ u[n] $$相当于 $$\delta[n]$$的积分

### Other concepts

* Energy and Power of Periodic Signals: 积分与积分后的处理
* 谐振: 同一个角频率的集合
* 
## Properties of System 

### Memory / Memoryless

Output only depends on input **at the same time**

### nvertibility and Inverse System

Distinct **input** leads to distinct **output**

### **Causality**

{% hint style="info" %}
**All memoryless are causal** 
{% endhint %}

Output only depends on input **at the same time** or **before**

### **Stability**

**Bounded input** gives **Bounded output**

### **T**ime-Invariance

A **time-shift** in the input causes a **same time-shift** in the output

$$ x[n] \to y[n] $$ then $$ x[n-n_0] \to y[n-n_0] $$

Example:

![](.gitbook/assets/image%20%2810%29.png)

### Linearity

Additivity and Scaling

If $$ x[n] \to y[n] $$ then $$ ax_1[n] + bx_2[n]  \to ay_1[n] + b y_2 [n] $$

{% hint style="info" %}
If linear, zero input gives zero output 

$$x[ n]=0 \to y[n] = 2x[n] = 0 $$
{% endhint %}

## Convolution

### Begin

We can construct any signal by discrete function  $$ y[n] = x[k]\delta[n-k] $$, so that $$y[n]$$can be valued only at $$k$$ and get $$x[k] $$. By accumulation, the signal can be **piled up**. This is convolution, defined by $$ x[n] =\Sigma _{k = - \infty} ^ {\infty} x[k]\delta[n-k] = x[n] * h[n] $$, which is called **convolution sum**.

Example:

![Origin Signal](.gitbook/assets/image%20%289%29.png)

![pile up](.gitbook/assets/image%20%288%29.png)

### Properties of Convolution

* Commutative: $$x(t)∗h(t) =h(t)∗x(t)$$
  * 交换律
* Bi-linear: $$(ax_1(t) +bx_2(t))∗h(t) =a(x_1∗h) +b(x_2∗h),x∗(ah_1+bh_2) =a(x∗h_1) +b(x∗h_2)$$
* Shift: $$x(t−τ)∗h(t) =x(t)∗h(t−τ)$$
* Identity: δ\(t\) is the identity signal,  $$ x∗δ=x=δ∗x $$
  * Identity is unique: $$i(t) =i(t)∗δ(t) =δ(t)$$
* Associative: $$x_1∗(x_2∗x_3) = (x_1∗x_2)∗x_3$$
* Smooth derivative: $$  y(n)' = x(n)'*h(n) = x(n)*h(n)' $$

### Properties of L.T.I. System

* Memoryless: $$x[n] \neq 0$$ when $$ n = 0 $$
* Invertibility: A system is invertible only if an inverse system exists.
* Causality: $$h[n] = 0 $$ when  $$ n < 0 $$
  * $$ y[n]=\sum_{k=0}^{\infty} h[k] \times[n-k] $$
  * $$ \begin{equation} y[n]=\sum_{k=-\infty}^{n} x[k] h[n-k] \end{equation} $$
* Stability: 
  *  $$ ( \sum_{k=-\infty}^{\infty}|h[k]|<\infty ) $$ 
* Convolving  $$δ(t)$$ with itself 
  * $$  ( \delta(t)  * \delta(t)) = \delta(t) $$

### Calculation

Sliding window: 

1. Reverse the simpler one $$x(t) $$
2. Record reversed $$x(t)$$ 's jumping points
3. Slide reversed $$x(t)$$, for each $$g(t)$$, is integral of multiplication

$$ g(t)=\int \frac{d}{d t} x * h(t) d t=\ldots $$

$$  \begin{equation}  g(t)=\frac{d}{d t} \int x * h(t) d t=\ldots  \end{equation}$$























