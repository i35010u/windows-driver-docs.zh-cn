---
title: ks.allstreams
description: Ks.allstreams 扩展需要遍历整个设备树并查找系统中的流式处理设备每个内核。
ms.assetid: 3a9f4ad4-a3aa-46dc-887d-c83296bc8f84
keywords:
- ks.allstreams Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.allstreams
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f91666c28cdbe5560c7a2583027e5cfbe101b00a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336332"
---
# <a name="ksallstreams"></a>!ks.allstreams


**！ Ks.allstreams**扩展需要遍历整个设备树并查找系统中的流式处理设备每个内核。

```dbgcmd
!ks.allstreams [Flags] [Level] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
可选。 指定要显示的信息类型。 *标志*可以是以下位的任意组合。 默认值为 0x1:

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
将导致显示以包括流。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
将导致显示以包括代理实例。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>位 3 (0x8)  
将导致显示以包括排队的 Irp。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>4 位 (0x10)  
将导致显示以包括所有流的无格式的显示。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>5 位 (0x20)  
将导致显示以包括所有流格式的无格式的显示。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span> *级别*   
可选。 指定要显示在 0 到 7 的详细信息级别越来越多的信息显示为较高的值的小数位数。 若要显示所有可用的详细信息，请提供值为 7。

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

此命令可能需要一些时间执行 （一分钟的时间并不少见）。

下面是举例 **！ ks.allstreams**显示：

```dbgcmd
kd> !allstreams 
6 Kernel Streaming FDOs found:
    Functional Device 82a17690 [\Driver\smwdm]
    Functional Device 8296eb08 [\Driver\wdmaud]
    Functional Device 82490388 [\Driver\sysaudio]
    Functional Device 82970cb8 [\Driver\MSPQM]
    Functional Device 824661b8 [\Driver\MSPCLOCK]
    Functional Device 8241c020 [\Driver\avssamp]
```

 

 





