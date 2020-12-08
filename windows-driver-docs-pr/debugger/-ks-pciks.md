---
title: ks. pciks
description: Pciks 扩展列出附加到 PCI 总线的内核流式处理设备的功能设备。 此外，它还可以显示有关这些功能设备上的活动流的信息。
keywords:
- pciks Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.pciks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 36a23ac12587243905b80adc9f8682bfd6a8920f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804057"
---
# <a name="kspciks"></a>!ks.pciks


**Pciks** 扩展列出附加到 PCI 总线的内核流式处理设备的功能设备。 此外，它还可以显示有关这些功能设备上的活动流的信息。

```dbgcmd
!ks.pciks [Flags] [Level] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
可选。 指定要显示的信息的类型。 *标志* 可以是以下位的任意组合。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
列出所有当前正在运行的流。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)   
递归图形以查找非 PCI 设备。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)   
显示代理实例的列表。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>第 3 (0x8)   
显示当前排队的 Irp。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>位 4 (0x10)   
显示有关所有流的信息。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>第 5 (0x20)   
显示活动流格式。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span>*级别*   
可选，并且仅适用于标记导致显示数据的组合。 级别与 [**！ ks**](-ks-dump.md)相同。

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

此命令可能需要一段时间才能执行，尤其是在加载 ACPI 筛选器驱动程序时，或者如果启用了驱动程序验证程序并且驱动程序名称已分页。

下面是一个 **pciks** 显示示例：

```dbgcmd
kd> !pciks
1 Kernel Streaming FDOs found:
    Functional Device 82a17690 [\Driver\smwdm]
```

 

 





