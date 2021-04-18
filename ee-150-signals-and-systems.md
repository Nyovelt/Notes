---
description: ShanghaiTech University - Spring 2021
---

# EE 150: Signals and Systems

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

![](.gitbook/assets/image%20%287%29.png)

### Linearity

Additivity and Scaling

If $$ x[n] \to y[n] $$ then $$ ax_1[n] + bx_2[n]  \to ay_1[n] + b y_2 [n] $$





\*\*\*\*















