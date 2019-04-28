---
title: dflink
description: Dflink 扩展显示链接的列表中向前定位。
ms.assetid: b75a01f6-557c-4602-83fa-629e16ba8c5d
keywords:
- dflink Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dflink
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 74ebe7ae760ea6e1d35bddd08a80c5321dd2ebfa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334588"
---
# <a name="dflink"></a>!dflink


**！ Dflink**扩展插件都会显示在正向链接的列表。

```dbgcmd
!dflink Address [Count] [Bias]  
```

## <a name="span-idddkdflinkdbgspanspan-idddkdflinkdbgspanparameters"></a><span id="ddk__dflink_dbg"></span><span id="DDK__DFLINK_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的地址列表\_条目结构。 与此节点将开始显示。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span> *Count*   
指定要显示的列表项的最大数目。 如果省略，默认值为 32。

<span id="_______Bias______"></span><span id="_______bias______"></span><span id="_______BIAS______"></span> *偏差*   
指定要在每个指针中忽略位数的掩码。 每个**Flink**地址将它与 (不*偏差*) 之前遵循下一位置。 默认值为零 （即，不应忽略的任何位）。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**！ Dflink**扩展遍历**Flink**字段列表的\_条目结构，并显示最多四个 ULONGs 在每个地址。 若要进入另一个方向，使用[ **！ dblink**](-dblink.md)。

[ **Dl （显示链接列表）** ](dl--display-linked-list-.md)命令是功能更多[ **！ dblink** ](-dblink.md)并 **！ dflink**。

 

 





