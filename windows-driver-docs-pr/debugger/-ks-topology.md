---
title: ks。拓扑
description: Ks 扩展显示最接近对象的筛选器内部拓扑的已排序关系图。
keywords:
- ks. 拓扑 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.topology
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b0df1cc68bd44ff60b6a83280bb9da7cdcd823da
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804053"
---
# <a name="kstopology"></a>!ks.topology


**！ Ks** 扩展显示最接近 *对象* 的筛选器内部拓扑的已排序关系图。

```dbgcmd
!ks.topology Object [Level] [Flags] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span>*对象*   
指定一个指针，该指针指向要用作关系图基础的对象。 可以是指向文件对象、IRP、pin、筛选器或其他 KS 对象的指针。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span>*级别*   
可选。 指定要在0-7 刻度上显示的详细信息的级别，并为较高的值显示更多的信息。 若要显示所有可用的详细信息，请提供值7。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
目前不可用。

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

若要获得帮助，请发出不带参数的 **！ ks** 命令。

请注意，此命令可能需要几分钟才能执行。

 

 





