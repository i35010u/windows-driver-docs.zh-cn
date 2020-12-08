---
title: ks. pciaudio
description: Pciaudio 扩展显示当前附加到 PortCls 的 FDOs 列表。
keywords:
- pciaudio Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.pciaudio
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ae1e42eee4b0e4f562f65367c656b8ce6bbc7151
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804063"
---
# <a name="kspciaudio"></a>!ks.pciaudio


**Pciaudio** 扩展显示当前附加到 PortCls 的 FDOs 列表。

```dbgcmd
!ks.pciaudio [Options] [Level]  
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
可选。 指定要显示的信息的类型。 *选项* 可以是以下位的任意组合。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
显示正在运行的流的列表。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)   
显示列出所有流。

<span id="Bit_3__0x4_"></span><span id="bit_3__0x4_"></span><span id="BIT_3__0X4_"></span>第 3 (0x4)   
输出显示的流。 只有在设置了此位时，*级别* 才有意义。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span>*级别*   
可选，并且仅当在 *选项* 中设置位3时才适用。 级别与 [**！ ks**](-ks-dump.md)相同。

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

下面是 **pciaudio** 的输出示例：

```dbgcmd
kd> !ks.pciaudio
1 Audio FDOs found:
 Functional Device 8299be18 [\Driver\smwdm]
```

 

 





