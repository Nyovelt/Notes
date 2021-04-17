---
description: ShanghaiTech University - Spring 2021
---

# EE 150: Signals and Systems

## Intro

### Basic concepts

#### Signals and Systems

* **Signal**: a function of one or more independent variables \(e.g., time and spatial variables\); typically contains information about the behavior or nature of some physical phenomena
  * 信号是一系列独立变量
* **System**: responds to a particular signal input by producing another signal\(output\)
  * 系统是其一个信号进， 一个信号出

![A kind of signal](.gitbook/assets/image%20%281%29.png)

#### Transformation

* Time reflection: x\(t\) ←→ x\(−t\), x\[n\] ←→ x\[−n\]
* Time scaling: x\(t\) ←→ x\(ct\)
* Time shift: x\(t\) ←→ x\(t − t0\), x\[n\] ←→ x\[n − n0\]
* Usually **do shift then scaling** to avoid complex mathematics

#### Even and Odd functions

Every signal function is $$x(t) = Even(x) + Odd(t)$$ ,then

$$ x(-t) = Even(-t) + Odd(-t) = Even(t) - Odd(t) $$

$$ Even(t) = \frac12 ( x(t) + x(-t) ) $$

$$ Odd(t) = \frac12 ( x(t) - x(-t) )$$

#### Periodic

* Preodic: $$ x(t) = x(t+mT)$$ or $$ x[t] = x[t+mT]$$ 
  * Fundamental period $$T$$:  Smallest positive $$T$$
* Aperiodic: Non-preodic

#### Sin



