---
title: ks.findlive
description: Ks.findlive 扩展搜索要尝试查找具有指定类型的活动对象的内部 Ks.sys 调试日志。
ms.assetid: 71372144-3f39-460b-859c-ac4cba0c766d
keywords:
- ks.findlive Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.findlive
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c9470725ce1c6ba25c18f20241457857ba9bf6ed
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336248"
---
# <a name="ksfindlive"></a>!ks.findlive


**！ Ks.findlive**扩展搜索要尝试查找具有指定类型的活动对象的内部 Ks.sys 调试日志。

```dbgcmd
!ks.findlive Type [Entries] [Level] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Type______"></span><span id="_______type______"></span><span id="_______TYPE______"></span> *Type*   
指定要搜索的对象的类型。 作为一个文本值中输入以下值之一：**队列**，**请求者**， **Pin**，**筛选器**，或**Irp**。

<span id="Entries"></span><span id="entries"></span><span id="ENTRIES"></span>条目  
如果此参数为零或省略，则搜索整个日志。

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

**！ Ks.findlive**命令可能找不到所有可能的都指定活动对象。

此扩展需要目标计算机是运行 Ks.sys 选中 （调试） 版本。

 

 





