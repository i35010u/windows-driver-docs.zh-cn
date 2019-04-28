---
title: ks.pciks
description: Ks.pciks 扩展列出了用于流式处理附加到 PCI 总线的设备的内核功能设备。 （可选） 它可以在这些功能的设备上显示有关活动流的信息。
ms.assetid: 525eb1eb-4b96-46da-90ae-d3c5f8d7511a
keywords:
- ks.pciks Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.pciks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5c202a4c9985225e8c43ec5dfd36a566bb15e129
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336231"
---
# <a name="kspciks"></a>!ks.pciks


**！ Ks.pciks**扩展列出了用于流式处理附加到 PCI 总线的设备的内核功能设备。 （可选） 它可以在这些功能的设备上显示有关活动流的信息。

```dbgcmd
!ks.pciks [Flags] [Level] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
可选。 指定要显示的信息类型。 *标志*可以是以下位的任意组合。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
列出所有当前正在运行流。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
递归关系图来查找非 PCI 设备。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
显示代理实例的列表。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>位 3 (0x8)  
显示当前正在排队 Irp。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>4 位 (0x10)  
显示有关所有流的信息。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>5 位 (0x20)  
显示活动流格式。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span> *级别*   
可选的并仅适用于导致显示的数据的标志组合。 级别都与用于相同[ **！ ks.dump**](-ks-dump.md)。

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

此命令可能需要执行时间，尤其是当加载 ACPI 筛选器驱动程序，或如果已启用驱动程序验证程序和驱动程序名称调出。

下面是举例 **！ ks.pciks**显示：

```dbgcmd
kd> !pciks
1 Kernel Streaming FDOs found:
    Functional Device 82a17690 [\Driver\smwdm]
```

 

 





