---
title: dblink
description: Dblink 扩展显示链接的列表中向后方向。
ms.assetid: d57b07a6-217b-475e-adf5-7dc0f972c494
keywords:
- dblink Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dblink
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1461ca8b452874bde6841b7ba9a54e41f0fb2151
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520279"
---
# <a name="dblink"></a>！ dblink


**！ Dblink**扩展显示链接的列表中向后方向。

```dbgcmd
!dblink Address [Count] [Bias]  
```

## <a name="span-idddkdblinkdbgspanspan-idddkdblinkdbgspanparameters"></a><span id="ddk__dblink_dbg"></span><span id="DDK__DBLINK_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的地址列表\_条目结构。 与此节点将开始显示。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span> *Count*   
指定要显示的列表项的最大数目。 如果省略，默认值为 32。

<span id="_______Bias______"></span><span id="_______bias______"></span><span id="_______BIAS______"></span> *偏差*   
指定要在每个指针中忽略位数的掩码。 每个**闪烁**地址将它与 (不*偏差*) 之前遵循下一位置。 默认值为零 （即，不应忽略的任何位）。

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

**！ Dblink**扩展遍历**闪烁**字段列表的\_条目结构，并显示最多四个 ULONGs 在每个地址。 若要进入另一个方向，使用[ **！ dflink**](-dflink.md)。

[ **Dl （显示链接列表）** ](dl--display-linked-list-.md)命令是功能更多 **！ dblink**并[ **！ dflink**](-dflink.md)。

 

 





