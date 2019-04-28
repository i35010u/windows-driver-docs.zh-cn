---
title: ks.topology
description: Ks.topology 扩展显示的对象最接近的筛选器内部拓扑的已排序关系图。
ms.assetid: 04ef6920-c022-4136-a42a-800679fe7ff4
keywords:
- ks.topology Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.topology
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: aea4718827c4d81d26e5a88d4c874cd469012faa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336206"
---
# <a name="kstopology"></a>!ks.topology


**！ Ks.topology**扩展显示最接近的筛选器的内部拓扑的已排序关系图*对象*。

```dbgcmd
!ks.topology Object [Level] [Flags] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span> *Object*   
指定指向要用作基础关系图的对象的指针。 可以是指向文件对象、 IRP、 pin、 筛选器或其他 KS 对象的指针。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span> *级别*   
可选。 指定要显示在 0 到 7 的详细信息级别越来越多的信息显示为较高的值的小数位数。 若要显示所有可用的详细信息，请提供值为 7。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
当前不可用。

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

有关帮助，发出 **！ ks.topology**命令不带任何参数。

请注意，此命令可能需要一些时间来执行。

 

 





