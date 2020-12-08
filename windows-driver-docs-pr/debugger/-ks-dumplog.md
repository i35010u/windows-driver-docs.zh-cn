---
title: ks. dumplog
description: Dumplog 扩展显示内部内核流调试日志。
keywords:
- dumplog Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.dumplog
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2a4423c74fc5cec4a82f4d60f14ac6c59282e2f6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787053"
---
# <a name="ksdumplog"></a>!ks.dumplog


**Dumplog** 扩展显示内部内核流调试日志。

```dbgcmd
!ks.dumplog [Entries] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Entries______"></span><span id="_______entries______"></span><span id="_______ENTRIES______"></span>*条目*   
可选。 指定要显示的日志条目数。 如果 *条目* 为零或省略，则显示整个日志。

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

可以通过按 [**CTRL + C**](ctrl-c--break-.md)停止日志显示。

此扩展要求目标计算机运行 Ks.sys 的已选中 (调试) 版本。

 

 





