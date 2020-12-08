---
title: rm（寄存器掩码）
description: Rm 命令修改或显示注册显示掩码。 此掩码控制 r (寄存器) 命令显示寄存器的方式。
keywords:
- rm (注册掩码) Windows 调试
ms.date: 07/12/2018
topic_type:
- apiref
api_name:
- rm (Register Mask)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8c639a152cdfb84e57d31c35a0d2e4f528a88cc1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786947"
---
# <a name="rm-register-mask"></a>rm（寄存器掩码）


**Rm** 命令修改或显示注册显示掩码。 此掩码控制 [**r (寄存器)**](r--registers-.md) 命令显示寄存器的方式。

```dbgcmd
rm 
rm ? 
rm Mask 
```

## <a name="span-idddk_cmd_register_mask_dbgspanspan-idddk_cmd_register_mask_dbgspanparameters"></a><span id="ddk_cmd_register_mask_dbg"></span><span id="DDK_CMD_REGISTER_MASK_DBG"></span>参数


<span id="______________"></span> **?**   
显示可能的 *掩码* 位的列表。

<span id="_______Mask______"></span><span id="_______mask______"></span><span id="_______MASK______"></span>*掩码*   
指定调试器显示寄存器时要使用的掩码。 *掩码* 是指示寄存器显示内容的位的总和。 位的含义取决于处理器和模式。 有关详细信息，请查看请参阅以下 "备注" 部分中的表。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>



<a name="remarks"></a>备注
-------

命令名称中的 "m" 必须是小写字母。

如果使用不带参数的 **rm** ，将显示当前值以及有关其位的说明。

若要显示基本整数寄存器，必须将位 0 (0x1) 或第1位 (0x2) 。 默认情况下，为32位目标设置0x1，并为64位目标设置0x2。 不能同时设置这两个位--如果尝试设置两个位，0x2 将覆盖0x1。

您可以使用 [**r (寄存器)**](r--registers-.md) 命令以及 **M** 选项来替代默认掩码。

基于 x86 的处理器或基于 x64 的处理器支持以下 *掩码* 位。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">bit</th>
<th align="left">“值”</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p></p>
0 1</td>
<td align="left"><p></p>
0x1 0x2</td>
<td align="left"><p>显示基本整数寄存器。  (设置其中一个或两个位具有相同的效果。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0x4</p></td>
<td align="left"><p>显示浮点寄存器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0x8</p></td>
<td align="left"><p>显示段寄存器。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0x10</p></td>
<td align="left"><p>显示 MMX 寄存器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>5</p></td>
<td align="left"><p>0x20</p></td>
<td align="left"><p>显示调试寄存器。 在内核模式下，设置此位也会显示 CR4 注册。</p></td>
</tr>
<tr class="even">
<td align="left"><p>6</p></td>
<td align="left"><p>0x40</p></td>
<td align="left"><p>显示 SSE XMM 寄存器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>7</p></td>
<td align="left"><p>0x80</p></td>
<td align="left"><p>仅) 显示控制寄存器 (内核模式，例如 CR0、CR2、CR3 和 CR8。</p></td>
</tr>
<tr class="even">
<td align="left"><p>8</p></td>
<td align="left"><p>0x100</p></td>
<td align="left"><p> (内核模式仅) 显示描述符和任务状态寄存器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>9</p></td>
<td align="left"><p>0x200</p></td>
<td align="left"><p>显示浮点数中的 AVX YMM 寄存器。</p></td>
</tr>
<tr class="even">
<td align="left"><p>10</p></td>
<td align="left"><p>0x400</p></td>
<td align="left"><p>以十进制整数显示 AVX YMM 寄存器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>11</p></td>
<td align="left"><p>0x800</p></td>
<td align="left"><p>以十进制整数显示 AVX XMM 寄存器。</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>12</td>
<td align="left"><p></p>0x1000</td>
<td align="left"><p>以浮点格式显示 AVX-512 zmm0-zmm31 寄存器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>13</p></td>
<td align="left"><p>0x2000</p></td>
<td align="left"><p>以整数格式显示 AVX-512 zm00-zmm31 寄存器。</p></td>
</tr>
<tr class="even">
<td align="left"><p>14</p></td>
<td align="left"><p>0x4000</p></td>
<td align="left"><p>显示 512 k0-k7 寄存器 AVX。</p></td>
</tr>
</tbody>
</table>


## <a name="examples"></a>示例

启用整数状态和段寄存器。

```dbgcmd
0: kd> rm 0x00a
0: kd> rm
Register output mask is a:
       2 - Integer state (64-bit)
       8 - Segment registers
```


启用 0x1000 (显示浮点格式) 的 AVX-512 zmm0-zmm31 寄存器。

```dbgcmd
0: kd> rm 0x100a
0: kd> rm
Register output mask is 100a:
       2 - Integer state (64-bit)
       8 - Segment registers
    1000 - AVX-512 ZMM registers
```


启用掩码 0x2000 (以整数格式显示 512 zmm00-zmm31 寄存器) 。

```dbgcmd
0: kd> rm 0x200a
0: kd> rm
Register output mask is 200a:
       2 - Integer state (64-bit)
       8 - Segment registers
    2000 - AVX-512 ZMM Integer registers
```


启用所有 AVX-512 寄存器掩码：

```dbgcmd
0: kd> rm 0x700a
0: kd> rm
Register output mask is 700a:
       2 - Integer state (64-bit)
       8 - Segment registers
    1000 - AVX-512 ZMM registers
    2000 - AVX-512 ZMM Integer registers
    4000 - AVX-512 Opmask registers
```

如果尝试在不支持的硬件上设置寄存器掩码，则会忽略寄存器掩码的无效位。

```dbgcmd
kd> rm 0x100a
Ignored invalid bits 1000
kd> rm
Register output mask is a:
      2 - Integer state (64-bit)
       8 - Segment registers
```





