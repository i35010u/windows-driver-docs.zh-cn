---
title: ks.dumplog
description: Ks.dumplog 扩展显示内部内核调试日志流式处理。
ms.assetid: 09829517-c01c-4cbd-bd0f-2ad0c1554f39
keywords:
- ks.dumplog Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.dumplog
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 48f08ad3b6950749f3300eb384680f94423a2780
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336305"
---
# <a name="ksdumplog"></a>!ks.dumplog


**！ Ks.dumplog**扩展显示内部内核调试日志流式处理。

```dbgcmd
!ks.dumplog [Entries] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Entries______"></span><span id="_______entries______"></span><span id="_______ENTRIES______"></span> *条目*   
可选。 指定要显示的日志项的数量。 如果*条目*为零或省略，将显示整个日志。

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

可以通过按停止显示日志[ **CTRL + C**](ctrl-c--break-.md)。

此扩展需要目标计算机是运行 Ks.sys 选中 （调试） 版本。

 

 





