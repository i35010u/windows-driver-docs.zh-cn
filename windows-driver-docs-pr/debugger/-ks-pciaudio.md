---
title: ks.pciaudio
description: Ks.pciaudio 扩展显示当前附加到 PortCls FDOs 的列表。
ms.assetid: 30d74f14-1cff-4b18-996a-8c91c20edebe
keywords:
- ks.pciaudio Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.pciaudio
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b73db84e86a5829cb22b763fd79cceb31f620887
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523375"
---
# <a name="kspciaudio"></a>!ks.pciaudio


**！ Ks.pciaudio**扩展显示当前附加到 PortCls FDOs 的列表。

```dbgcmd
!ks.pciaudio [Options] [Level]  
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
可选。 指定要显示的信息类型。 *选项*可以是以下位的任意组合。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
显示正在运行的流的列表。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
显示列表的所有流。

<span id="Bit_3__0x4_"></span><span id="bit_3__0x4_"></span><span id="BIT_3__0X4_"></span>位 3 (0x4)  
显示输出流。 *级别*具有仅在设置此位时的含义。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span> *级别*   
可选的且仅当在中设置位 3 适用*选项*。 级别都与用于相同[ **！ ks.dump**](-ks-dump.md)。

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

下面是输出的示例 **！ ks.pciaudio**:

```dbgcmd
kd> !ks.pciaudio
1 Audio FDOs found:
 Functional Device 8299be18 [\Driver\smwdm]
```

 

 





