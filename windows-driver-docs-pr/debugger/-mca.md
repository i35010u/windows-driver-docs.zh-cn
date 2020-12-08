---
title: mca
description: 在 x86 目标计算机上，mca 扩展显示 (MCA) 寄存器的计算机检查体系结构。
keywords:
- '计算机检查体系结构 (MCA) '
- 'MCA (计算机检查体系结构) '
- mca Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- mca
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 476c8b22e629eebbd3a28af0d1c54171201639be
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825275"
---
# <a name="mca"></a>!mca

！ Mca 扩展显示 (MCA) 寄存器的计算机检查体系结构。 

```dbgcmd
!mca
```


## <a name="span-idddk__mca_dbgspanspan-idddk__mca_dbgspanparameters"></a><span id="ddk__mca_dbg"></span><span id="DDK__MCA_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
仅 (Itanium 目标) 指定 MCA 错误记录的地址。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
仅 (Itanium 目标) 指定输出级别。 *标志* 可以是以下位的任意组合。 默认值为0xFF，这将显示日志中显示的所有部分。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
显示处理器部分。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)   
显示平台特定的部分。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)   
显示内存部分。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>第 3 (0x8)   
显示 PCI 组件部分。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>位 4 (0x10)   
显示 PCI 总线部分。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>第 5 (0x20)   
显示 Dataaccessservice 日志部分。

<span id="Bit_6__0x40_"></span><span id="bit_6__0x40_"></span><span id="BIT_6__0X40_"></span>第 6 (0x40)   
显示 "平台主机控制器" 部分。

<span id="Bit_7__0x80_"></span><span id="bit_7__0x80_"></span><span id="BIT_7__0X80_"></span>第7位 (0x80)   
显示以包含平台总线部分。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

此扩展命令只能与基于 x86 的目标计算机一起使用。

<a name="remarks"></a>备注
-------

在 x86 目标上， **！ mca** 显示活动处理器支持的计算机检查寄存器。 它还显示基本 CPU 信息 (与显示的) [**！ cpuinfo**](-cpuinfo.md) ）相同。 下面是此扩展的输出示例：

```dbgcmd
0: kd> !mca
MCE: Enabled, Cycle Address: 0x00000001699f7a00, Type: 0x0000000000000000

MCA: Enabled, Banks 5, Control Reg: Supported, Machine Check: None.
Bank  Error  Control Register     Status Register
  0. None   0x000000000000007f   0x0000000000000000

  1. None   0x00000000ffffffff   0x0000000000000000

  2. None   0x00000000000fffff   0x0000000000000000

  3. None   0x0000000000000007   0x0000000000000000

  4. None   0x0000000000003fff   0x0000000000000000

No register state available.

CP F/M/S Manufacturer   MHz Update Signature Features
 0 15,5,0 SomeBrandName 1394 0000000000000000 a0017fff
```

请注意，此扩展需要专用 HAL 符号。 如果没有这些符号，扩展将显示消息 "找不到 HalpFeatureBits" 和基本 CPU 信息。 例如：

```dbgcmd
kd> !mca
HalpFeatureBits not found
CP F/M/S Manufacturer  MHz Update Signature Features
 0 6,5,1 GenuineIntel  334 0000004000000000 00001fff
```

 

 





