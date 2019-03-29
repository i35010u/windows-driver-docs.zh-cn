---
title: rm（寄存器掩码）
description: Rm 命令修改或显示注册显示掩码。 此掩码控制寄存器 r （寄存器） 命令的显示方式。
ms.assetid: b3203bf3-b614-490b-8cbd-6abb291a801a
keywords:
- rm （注册掩码） Windows 调试
ms.date: 07/12/2018
topic_type:
- apiref
api_name:
- rm (Register Mask)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 76526208eb8ed0ccf8457bbd6f8768e708cbb6a9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567051"
---
# <a name="rm-register-mask"></a>rm（寄存器掩码）


**Rm**命令修改或显示注册显示掩码。 此掩码控制如何显示寄存器[ **r （寄存器）** ](r--registers-.md)命令。

```dbgcmd
rm 
rm ? 
rm Mask 
```

## <a name="span-idddkcmdregistermaskdbgspanspan-idddkcmdregistermaskdbgspanparameters"></a><span id="ddk_cmd_register_mask_dbg"></span><span id="DDK_CMD_REGISTER_MASK_DBG"></span>参数


<span id="______________"></span> **?**   
显示可能的列表*掩码*位。

<span id="_______Mask______"></span><span id="_______mask______"></span><span id="_______MASK______"></span> *掩码*   
指定要使用时，调试器显示寄存器的掩码。 *掩码*是位，指示有关注册显示的内容的总和。 位的含义取决于处理器和模式。 有关详细信息;请参阅以下备注部分中的表。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>



<a name="remarks"></a>备注
-------

"M"中的命令名称必须是小写字母。

如果您使用**rm**不带任何参数的当前值会显示，以及有关其位的解释。

若要将基本整数显示注册时，必须设置位 0 (0x1) 或第 1 (0x2) 位。 默认情况下，为 32 位目标设置 0x1 和 0x2 设置为 64 位目标。 不能设置这两个位在同一时间--如果您尝试设置两个位 0x2 重写 0x1。

可以使用来覆盖默认的掩码[ **r （寄存器）** ](r--registers-.md)命令一起**M**选项。

以下*掩码*支持基于 x86 的处理器或基于 x64 的处理器的位。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">位</th>
<th align="left">ReplTest1</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p></p>
0 1</td>
<td align="left"><p></p>
0x1 0x2</td>
<td align="left"><p>显示基本整数寄存器。 （一个或两个这些位将设置有相同的效果。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0x4</p></td>
<td align="left"><p>显示浮点寄存器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0x8</p></td>
<td align="left"><p>显示段寄存器信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0x10</p></td>
<td align="left"><p>显示 MMX 寄存器信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>5</p></td>
<td align="left"><p>0x20</p></td>
<td align="left"><p>显示调试寄存器信息。 在内核模式下设置此位还显示 CR4 注册。</p></td>
</tr>
<tr class="even">
<td align="left"><p>6</p></td>
<td align="left"><p>0x40</p></td>
<td align="left"><p>显示 SSE XMM 寄存器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>7</p></td>
<td align="left"><p>0x80</p></td>
<td align="left"><p>（仅适用于内核模式）显示控制寄存器，例如 CR0、 CR2、 CR3 和 CR8。</p></td>
</tr>
<tr class="even">
<td align="left"><p>8</p></td>
<td align="left"><p>0x100</p></td>
<td align="left"><p>（仅适用于内核模式）显示描述符和任务状态寄存器信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>9</p></td>
<td align="left"><p>0x200</p></td>
<td align="left"><p>AVX YMM 寄存器中浮动点的显示。</p></td>
</tr>
<tr class="even">
<td align="left"><p>10</p></td>
<td align="left"><p>0x400</p></td>
<td align="left"><p>显示 AVX YMM 寄存器中十进制整数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>11</p></td>
<td align="left"><p>0x800</p></td>
<td align="left"><p>显示 AVX XMM 注册十进制整数。</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>12</td>
<td align="left"><p></p>0x1000</td>
<td align="left"><p>显示浮动点格式 AVX-512 zmm0 zmm31 注册。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>13</p></td>
<td align="left"><p>0x2000</p></td>
<td align="left"><p>显示 AVX-512 zm00 zmm31 注册整数格式。</p></td>
</tr>
<tr class="even">
<td align="left"><p>14</p></td>
<td align="left"><p>0x4000</p></td>
<td align="left"><p>显示 AVX-512 k0 k7 寄存器信息。</p></td>
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


启用的 0x1000 （浮动点格式显示 AVX-512 zmm0 zmm31 寄存器）。

```dbgcmd
0: kd> rm 0x100a
0: kd> rm
Register output mask is 100a:
       2 - Integer state (64-bit)
       8 - Segment registers
    1000 - AVX-512 ZMM registers
```


启用掩码 0x2000 （AVX-512 zmm00 zmm31 注册整数格式显示）。

```dbgcmd
0: kd> rm 0x200a
0: kd> rm
Register output mask is 200a:
       2 - Integer state (64-bit)
       8 - Segment registers
    2000 - AVX-512 ZMM Integer registers
```


启用所有 AVX-512 注册掩码：

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

如果你尝试并不支持的硬件上设置注册掩码，将忽略无效的注册掩码位。

```dbgcmd
kd> rm 0x100a
Ignored invalid bits 1000
kd> rm
Register output mask is a:
      2 - Integer state (64-bit)
       8 - Segment registers
```





