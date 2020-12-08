---
title: ks。图
description: Ks 扩展命令以界定闭合排序顺序显示内核模式图的文本说明。
keywords:
- ks Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.graph
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 94b35cdfc89080e90fb5127e6d634e4fa43de0d7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828273"
---
# <a name="ksgraph"></a>!ks.graph


**！ Ks** 扩展命令以界定闭合排序顺序显示内核模式图的文本说明。

```dbgcmd
!ks.graph Object [Level] [Flags] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span>*对象*   
指定指向对象的指针，该对象用作关系图的起始点。 必须是指向以下项之一的指针： file 对象、IRP、pin 或筛选器。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span>*级别*   
可选。 指定要在0-7 刻度上显示的详细信息的级别，并为较高的值显示更多的信息。 若要显示所有可用的详细信息，请提供值7。 **！ Ks** 的级别与 [**！ ks**](-ks-dump.md)的级别相同。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
可选。 指定要显示的信息的类型。 *标志* 可以是以下位的任意组合。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
显示图表中每个 pin 实例排队的 Irp 列表。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)   
显示图表中每个 pin 实例挂起的 Irp 列表。 只有 pin 知道的 Irp 正在等待。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>位 4 (0x10)   
针对可疑筛选器分析停止关系图。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>winxp\Ks.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ks.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核流调试](kernel-streaming-debugging.md)。

<a name="remarks"></a>备注
-------

此命令可能需要一些时间才能处理。

发出一个 **！ ks. graph** 命令，其中没有用于帮助的参数。

下面是一个使用筛选器对象地址的 **！ ks 图形** 显示示例：

```dbgcmd
kd> !graph 829493c4
Attempting a graph build on 829493c4...  Please be patient...

Graph With Starting Point 829493c4:

"avssamp" Filter 82949350, Child Factories 1
    Output Factory 0 [Video/General Capture]:
        Pin 8293f4f0 (File 82503498) Irps(q/p) = 2, 0
```

 

 





