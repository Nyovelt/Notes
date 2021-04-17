# RISC-V

#### Instructions

* ![](https://snz04pap002files.storage.live.com/y4mwCiM1SDGRlQ1V0upPdLAAdT0SGq8eQbvbgdNV7RogPurxVjCRvqXCPaoUTJretOunNk8Ty6PlCZR18DdfV_1mi7woJi0WkqK0XVqcwZdCstrBc0UowRJ9Xwo2IMF8vMph-gaUcEXm3B8k1w0VcSYN6AYnVXcLhAXLMBdWy_qzpdM6qs7xJdkxzNk9Tut7SLz?width=1816&height=534&cropmode=none)
* Techniques:
  * \*=-1: 取反加一
  * 寄存器置零： xor zero
* 函数调用
  * a0 - a7: arguments
  * a0, a1: return value
  * sp: 栈指针
  * when jal to functions, a0-a7, t0-t6, ra need to save, since they can be modified during callee
* `jr ra`: when some functions is called somewhere, in order to continue running programme, use jr ra to move to ra, and continue programme. 用于返回。 和 `jal`配合使用
* `jal`: jumo and link, 给 `ra`赋值， 这样函数就知道回到哪里了
* `j`: jal x0 offset 不记录返回值
* 伪指令
  * ![](https://snz04pap002files.storage.live.com/y4mfcArPm5wbrtiaGxz8iuy9UamZmb45wPwZh9IrUV0iD4f1xZx3jar9u_1Rj64Xh68hYgnQAwjeC31ONDkCGZtvfYJvGS2csyyMCCcdHkPd5LUTfFAvWLPIiOp_lfsDr9sS29iE7_7DH_PS9l37yCp5vpRNFh9dkHq3CFEP9shv1Be1Vo3zMK3Y13EUD05ak4N?width=1920&height=1440&cropmode=none)

#### Immediates

* An I-type instruction can only have 12 bits of immediate
  * Bits 31:12 get the same value as Bit 11
* RISC-V immediates are "sign extended"
  * 首位为符号位

#### Little Eddiem

* ![](https://snz04pap002files.storage.live.com/y4mT2S6RrFDKQJmTzbD0r-zFNd4ybshNaFhCiNnpCpgDarK_egSY5EirDubpuId2ljjU4s4rSfQ7thLe7LW5FI86KIudWsqymgp_6coO0D4jCGkYnc6cUPBF0DratTKLlZ8UJV2LWBZJgt_QXby0mOCcC65TDrXzgpe1kni14q0dYHvpVDyKzwcXTkF2nRSYnR9?width=2098&height=1184&cropmode=none)
  * 小端序： ![](https://upload.wikimedia.org/wikipedia/commons/thumb/e/ed/Little-Endian.svg/280px-Little-Endian.svg.png)
  * 自下而上的存储， 前面的在下面。 寄存器从下而上数。
  * 0x8f5 为负数\(itype 指令只有12位， 因此大于 0x7ff 的都是负数\)， 因此扩写成16位\(因为寄存器为32位\)的补码
    * 0xfffff8f5 \(两者取反 加一 值相同\)

#### Types

![](https://snz04pap002files.storage.live.com/y4m6bArYGFBiAHqyJvsp3OGJ_HLK-fgf4EJj5kOFUSGTWKBTkw0aQ6l-rkjdCHTfljQ430peJcBgMHS6i9BcNiWFyAlPFstoe5zNJV2jzYKJyNZH_IeyhxxUiAxyLuTEMgGdDiMYCPJ_Y63azFHjOv9oH_jPIlN9tcu5_b4x1PpZuBBMyXiEqjjdnmft_RCcrMr?width=1466&height=408&cropmode=none)

* `I type`只能处理12 bit 立即数
* * LI = LUI + ADDI
  * ![](https://snz04pap002files.storage.live.com/y4muP-145WsnADoJQkCOu408FSE_5yYyr0iryC-6wvNTJ7G3eZ8CthGBhm6IVdGRCuXZZrcKP4mepPgDQnpFnpEzAO8TvrEq6I4toAEjuMv0-tcjy2X7wF_fNKCqq-7togjeBqhZaOn8w6RS8mI_KZqXwKue9dV95mv__AWzFy4vyAt2oSKcT6FttPN-o-gGmhW?width=1770&height=990&cropmode=none)
  * ![](https://snz04pap002files.storage.live.com/y4mUTd2NJ5QIKRlWd0NtMbOYNirRqFBlLUndMQPTIi9_fqaDFlbgM7WiIeSKITRzqE1ecF22d0wQFSDZxhijaq8nfzNr6MRWbQQ_EVMwXt81b1SpQ_glRN6pfgCAdMo0ZQ9nM9_J5urBw7-dHTI7v-3gGKoj591FHQT_EEVcUBZ8H65UMy9wlxqNs3Et6XY-_En?width=1770&height=1328&cropmode=none)
  * **DEADBEEF**: 如图所示，出现了问题。当且仅当32bit的后12bit为负数时，进行addi操作会扩展成补码。例如 `0xEFF`会扩展成`0xFFFFFEFF`。对于前20bit来说， 加上 `0xFFFFF000`无疑等于对第12位取反。
  * 解决方法是， 当后三位大于 `0x7FF`的时候，对第12位+1， 或者是对`x10`+1。 因为第12位是对于16进制的剩余类，在这个剩余类中，`0+F=F, F+1=0`, 取反加1为自身。

#### REF

1. [Risc-V instructions Set](https://1drv.ms/b/s!Au3reWMu7K2ChOZfWdNGg9fNARrDAA?e=QDam4p)

