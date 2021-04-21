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
* $$ \begin{equation} \mathrm{e}^{-\mathrm{j} \omega t}=\cos (\omega t)-\mathrm{j} \sin (\omega t) \end{equation} $$
* $$ \begin{equation} \cos (\omega t)=\frac{1}{2}\left(\mathrm{e}^{\mathrm{j} \omega t}+\mathrm{e}^{-\mathrm{j} \omega t}\right) \end{equation} $$
* $$ \begin{equation} \sin (\omega t)=\frac{1}{2 \mathrm{j}}\left(\mathrm{e}^{\mathrm{j} \omega t}-\mathrm{e}^{-\mathrm{j} \omega t}\right) \end{equation} $$

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

### 常见信号与周期判断

### 功率与能量

![](.gitbook/assets/image%20%2817%29.png)

### Other concepts

* Energy and Power of Periodic Signals: 积分与积分后的处理
* 谐振: 同一个角频率的集合
* 
## Properties of System 

### Memory / Memorylessx\`

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

### Properties of L.T.I System

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



## Eigen-function of L.T.I

### Eigen-functions

* A signal for which the system's output is just a constant \(possibly complex\) times the input.
* **Eigen Basis**: If an input signal can be decomposed to a weighted sum of eigenfunctions \(eigen basis\), then the output can be easily found.

So goal: Getting an **Eigen basis** of an L.T.I system.

### e^{st} as eigenfunction of L.T.I

1. Consider the input to be $$ x(t) = e^{st}$$, then the output is $$ y(t)=\int h(\tau) e^{s(t-\tau)} d \tau=e^{s t} \int h(\tau) e^{-s \tau} d \tau$$
2. $$ \begin{equation}  H(s)=\int h(\tau) e^{-s \tau} d \tau  \end{equation}$$ is just a constant, i.e. eigenvalue for function $$ e^{st}$$

### Orthonormal Basis

When $$ s$$ purely imaginary $$\begin{equation} j k \omega_{0} \end{equation}$$, $$ \begin{equation} e^{j k \omega_{0} t} \end{equation} $$ is orthonormal and standard among different .

* Definition of inner-product of perioidic functions: $$ \begin{equation}  <x_{1}(t), x_{2}(t)>=\frac{1}{T_{0}} \int_{T_{0}} x_{1}(t) x_{2}^{*}(t) d t  \end{equation}$$

## Fourier Analysis

### CT & DT

* CT: $$ e^{j\omega t } $$
  * $$ \begin{equation}  \mathrm{e}^{\mathrm{j} \omega \mathrm{t}} \longrightarrow \mathrm{H}(\mathrm{j} \omega) \mathrm{e}^{\mathrm{j} \omega \mathrm{t}}  \end{equation}$$
  * 纯虚数
* DT: $$ e^{j \omega n }$$
  * $$ \begin{equation}  \mathrm{e}^{j \omega n} \rightarrow H\left(\mathrm{e}^{j \omega}\right) \mathrm{e}^{j \omega n}  \end{equation}$$

### Periodic signals & Fourier Series Expansion

$$x(t)$$ may be expressed as a Fourier series:

$$ \begin{equation}  x(t)=\sum_{k=-\infty}^{\infty} a_{k} \cdot e^{j k \omega_{0} t}  \end{equation}$$, $$ \begin{equation}  x(t) \leftarrow{ }^{F . S .} \rightarrow a_{k}  \end{equation}$$

sum of sinusoids whose frequencies are multiple of ω0, the “fundamental frequency”.

Where $$a_k$$ can be obtained by

$$ \begin{equation}  a_{k}=\frac{1}{T_{0}} \int_{T_{0}} x(\tau) e^{-j k \omega_{0} \tau} d \tau  \end{equation}$$

* Case 0 is often special!
* $$a_0$$ controls a constant 

And, 



$$
\begin{aligned} x(t) &=\sum_{k=-\infty}^{\infty} a_{k} e^{j k \omega_{0} t} \\ &=\sum_{k=-\infty}^{\infty}\left(a_{k} \cos \left(k \omega_{0} t\right)+j a_{k} \sin \left(k \omega_{0} t\right)\right) \\ &=a_{0}+\sum_{k>0}\left(\left(a_{k}+a_{-k}\right) \cos \left(k \omega_{0} t\right)+j\left(a_{k}-a_{-k}\right) \sin \left(k \omega_{0} t\right)\right) \end{aligned}
$$

#### Odd / Even

![&#x5947;&#x5076;&#x7279;&#x6027;](.gitbook/assets/image%20%2811%29.png)



#### Approximation

![](.gitbook/assets/image%20%2812%29.png)

#### Linearity



$$
z(t)=\alpha x(t)+\beta y(t) \underset{\longleftrightarrow}{\longleftarrow S}{\longrightarrow} \alpha a_{k}+\beta b_{k}
$$

#### Time-shift



$$
x\left(t-t_{0}\right) \stackrel{F S}{\longleftrightarrow} e^{-j k \omega_{0} t_{0}} a_{k}
$$

#### Time-reverse



$$
x(-t) \stackrel{F S}{\longleftarrow} a_{-k}
$$

#### Time-scaling



$$
x(\alpha t)=\sum_{k=-\infty}^{\infty} a_{k} e^{j k\left(\alpha \omega_{0}\right) t}
$$

#### Multiplication



$$
x(t) y(t) \underset{\longleftrightarrow}{\longleftrightarrow S}, h_{k}=\sum_{l=-\infty}^{\infty} a_{l} b_{k-1}
$$

which is **Convolution**

#### conjugation & conjugate symmetry

![](.gitbook/assets/image%20%2816%29.png)

#### 7



$$
\frac{d x(t)}{d t} \longleftrightarrow F S, j k \omega_{0} a_{k}
$$



$$
\int_{-\infty}^{t} x(\tau) d \tau \underset{\longleftrightarrow}{\text { FS }}, \frac{a_{k}}{j k \omega_{0}}
$$

#### Parseval's identity



$$
\frac{1}{T} \int_{T}|x(t)|^{2} d t=\sum_{k=-\infty}^{\infty}\left|a_{k}\right|^{2}
$$

Proof:



$$
\begin{aligned} \frac{1}{T} \int_{T}|x(t)|^{2} d t &=\frac{1}{T} \int_{T} \sum_{k_{1}, k_{2}} a_{k_{1}} a_{k_{2}}^{*} e^{j\left(k_{1}-k_{2}\right) \omega_{0} t} d t \\ &=\sum_{k_{1}, k_{2}} a_{k_{1}} a_{k_{2}}^{*} \delta\left[k_{1}-k_{2}\right] \\ &=\sum_{k}\left|a_{k}\right|^{2} \end{aligned}
$$



## Continuous-Time Fourier Transform \(CTFT\)

### 变换与逆变换

Fourier series: $$\begin{equation}  x(t)=\sum_{k=-\infty}^{\infty} a_{k} \mathrm{e}^{j k \omega_{0} t}  \end{equation}$$

Inverse fourier transform: $$ x(t)=\frac{1}{2 \pi} \int_{\infty}^{\infty} X(j \omega) \mathrm{e}^{j \omega t} \mathrm{~d} \omega $$

### Fourier Transform Pair

Fourier Transform: $$ \begin{equation}  \mathcal{F}: X(j \omega)=\int_{-\infty}^{\infty} x(t) e^{-j \omega t} d t  \end{equation}$$

* For periodic signals, $$ \begin{equation}  X(j \omega)=2 \pi \sum_{-\infty}^{\infty} a_{k} \delta\left(\omega-k \omega_{0}\right)  \end{equation}$$, i.e. the Fourier Series
* $$ \begin{equation}  X(j \omega)  \end{equation}$$is called the "Spectrum" of $$ x(t)$$

Inverse F.T.  $$ \begin{equation}  \mathcal{F}^{-1}: x(t)=\frac{1}{2 \pi} \int_{-\infty}^{\infty} X(j \omega) e^{j \omega t} d \omega  \end{equation}$$

### Dual Porperty

$$ \begin{equation}  \mathcal{F}(\mathcal{F}(x(t)))=2 \pi \cdot x(-t)  \end{equation}$$

Means that when we put the $$ \begin{equation}  X(j \omega)  \end{equation}$$ in **time** domain, it will produce $$ 2\pi $$times $$ x(-t) $$ waveform in **freq** domain

### Properties

![](.gitbook/assets/image%20%2815%29.png)

![](.gitbook/assets/image%20%2813%29.png)

### Normal CT Fourier Pairs

![](.gitbook/assets/image%20%2814%29.png)

## 



## REF

* [https://www.josehu.com/assets/file/signals-systems.pdf](https://www.josehu.com/assets/file/signals-systems.pdf)

















