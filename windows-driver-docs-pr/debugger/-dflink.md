---
title: dflink
description: Dflink 扩展在正方向上按链接列表显示。
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
ms.openlocfilehash: 1cb4d2ef253daf4643774129551815dd2d17a558
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815542"
---
# <a name="dflink"></a>!dflink


**！ Dflink** extension 按向前方向显示链接列表。

```dbgcmd
!dflink Address [Count] [Bias]  
```

## <a name="span-idddk__dflink_dbgspanspan-idddk__dflink_dbgspanparameters"></a><span id="ddk__dflink_dbg"></span><span id="DDK__DFLINK_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定列表条目结构的地址 \_ 。 显示将从该节点开始。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span>*计数*   
指定要显示的列表条目的最大数量。 如果省略此值，则默认值为32。

<span id="_______Bias______"></span><span id="_______bias______"></span><span id="_______BIAS______"></span>*偏向*   
指定每个指针中要忽略的位掩码。 每个 **Flink** 地址都是 And，在将其跟在下一位置之前， (不会) *偏移* 。 默认值为零 (换言之，不要忽略任何位) 。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

**！ Dflink** EXTENSION 遍历列表条目结构的 **Flink** 字段 \_ ，并在每个地址最多显示四个 ULONGs。 若要继续，请使用 [**！ dblink**](-dblink.md)。

[**Dl (显示链接列表)**](dl--display-linked-list-.md)命令比 [**！ dblink**](-dblink.md)和 **！ dflink** 更通用。

 

 





