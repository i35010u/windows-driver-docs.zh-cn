---
title: ks.graph
description: Ks.graph 扩展命令显示在拓扑结构上排序顺序中的内核模式关系图的文本说明。
ms.assetid: b9725499-9db3-422f-850b-97db4865b74d
keywords:
- ks.graph Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.graph
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 468efe03adea8c5d2309cb1fc778c4989304030e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336242"
---
# <a name="ksgraph"></a>!ks.graph


**！ Ks.graph**扩展命令按拓扑结构上排序顺序显示内核模式关系图的文本说明。

```dbgcmd
!ks.graph Object [Level] [Flags] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span> *Object*   
指定指向要作为起始点使用关系图的对象的指针。 必须是指向以下项之一： 文件对象、 IRP、 pin 或筛选器。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span> *级别*   
可选。 指定要显示在 0 到 7 的详细信息级别越来越多的信息显示为较高的值的小数位数。 若要显示所有可用的详细信息，请提供值为 7。 级别 **！ ks.graph**是与用于相同[ **！ ks.dump**](-ks-dump.md)。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
可选。 指定要显示的信息类型。 *标志*可以是以下位的任意组合。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
显示一系列 Irp 排队到关系图中每个 pin 实例。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
显示的处于挂起状态的 Irp 列表从关系图中每个 pin 实例。 显示 pin 知道它正在等待的 Irp。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>4 位 (0x10)  
分析已停止的可疑的筛选器图形。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[流式处理的内核调试](kernel-streaming-debugging.md)。

<a name="remarks"></a>备注
-------

此命令可能需要一些时间来处理。

问题 **！ ks.graph**命令不带任何参数的帮助。

下面是举例 **！ ks.graph**显示，请使用筛选器对象的地址：

```dbgcmd
kd> !graph 829493c4
Attempting a graph build on 829493c4...  Please be patient...

Graph With Starting Point 829493c4:

"avssamp" Filter 82949350, Child Factories 1
    Output Factory 0 [Video/General Capture]:
        Pin 8293f4f0 (File 82503498) Irps(q/p) = 2, 0
```

 

 





