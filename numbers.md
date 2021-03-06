# Numbers

#### 整数

* Everything in a computer is a number, in fact only 0 and 1.
* Integers are interpreted by adhering to fixed-length
* Negative numbers are represented with Two’s complement
  * Overflows can be detected utilizing the carry bit
* 整数分为 unsigned 和 signed, 对应原码和补码
  * 关于补码的运算和溢出:
    * ![Nr50nu](https://oss.aaaab3n.moe/uPic/Nr50nu.jpg)
    * Overflow ERROR: When the result of addition exceeds the range of 
    * Overflow occurs if and only if two numbers with **the same sign** are added and the result has the opposite sign.
    * Generally, 负数的二进制值要大于非负数\(因为首位二进制为 1\)
    * `Unsigned` 对应 
    * A **neat trick** for flipping the sign of a two’s complement number: flip all thebits and add 1.
  * 2 problems \(in 6-bit binary\):
    * ![N9vNwe](https://oss.aaaab3n.moe/uPic/N9vNwe.jpg)
* The decoding and encoding system are human-defined, so that it can represent any number as wished. That is, no largest interger represent by n-bit numbers
*  because of `overflow`
* **n bit represents  numbers in binary**
* 2 进制适合计算机, 10进制适合数手指, 16进制表达更方便
* Consider `>>` operations, for signed int, &gt;&gt; 0 get signed bit; for neg get -1 \(-1 &gt;&gt; 1 = -1\)
* ref:
  * [About MSB and Overflow:](https://stackoverflow.com/questions/29330787/signed-overflow-why-carry-in-and-carry-out-of-msb-should-match)

#### IEEE 754 - 计算机数字标准表示

* Bias: 偏移, 即在结果加上偏移指, 或者 0b0 代表了偏移值本身. e.g. 0 -&gt; -127, 0xFF = -127 + 0xFF = -127 + 255 = 128 \(IEEE 754\)
* 第一位为符号位S。 接下来八位为指数位E，剩下23位为分数位F \(32 位\)
  * 
* 大小比较：
  * 首先按照指数排序， 再按照尾数排序
* 64位系统中: 1 位符号位， 11位指数位， 52位小数位 \(double\)
* 当指数位
* Overflow:
  * 在极大值的情况下会在指数位上溢出
  * 在极小值的情况下会在指数位下溢出
* 特殊情况：
  * 指数位全0： 极小数
  * 指数位全1, 小数位全0： Infinity 符号根据符号位确定
  * 全0: 0 , 符号位不确定
  * : 可正可负，指数位全1， **小数位不确定** =&gt; NaN
  * ![](https://snz04pap002files.storage.live.com/y4m6TNxePdpVx9OzxurZtXVgs0-3fOLclDH0k7i6GFR3uBJmyk8ExJerz1sM9rEUi2gDGXBNU2NHWYYn7cmpsI04cntU594NFCKadeg1W7veTAX8Nrp8zBbop67NuExwcynOXvvd7VlJ-B1zwI3YedANrzaQK6GW0eWPzGDp22_UNnaiwo4neyy6yF2lyUlivRI?width=1074&height=354&cropmode=none)
  * ![](https://snz04pap002files.storage.live.com/y4m8LUJ7roIO6DfM8Bg74PzkjMI4rDQkW8wQUEOG86Ic1f9Zp3McDQKf7S3H_CwDY-h4dAeEJmNOOTr0QSF8xyLlBBCpB2eq0aawyEuDJ9ELdyJRghZMKfiISI-ozXtr9kkbT1D0rbjuCvGLv5-4ywitiilZbjrblsxFmp3dGvRdm6q2TqhQnoEJZX26KKcVHBk?width=1468&height=400&cropmode=none)
* 浮点数不精确
* NaN 不可比较 \(仅仅在 NaN  x 时成立\)
* Smallest Gap: 
* 运算无交换律
* 最大整数: 0b0 11111110 全1， 因为指数位全1的话会变成 inf
* 计算方法: e.g. 53.125 =? 110101.001 =&gt;  =&gt; 127 + 5 = 132 = 10000100 =&gt; 0 10000100 10101001 000000..
* 加减法： [https://www.youtube.com/watch?v=wC950FKNl8Y](https://www.youtube.com/watch?v=wC950FKNl8Y)
* ref
  1. [IEEE 754 Simulator](https://www.h-schmidt.net/FloatConverter/IEEE754.html)

