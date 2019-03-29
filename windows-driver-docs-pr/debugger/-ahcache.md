---
title: ahcache
description: Ahcache 扩展显示应用程序兼容性缓存。
ms.assetid: 65a7c320-3ea3-4657-b271-ec3d9c2bd5de
keywords:
- ahcache Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- ahcache
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0bf1fed47df382824dded69c2aa6869f1d79cc16
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564744"
---
# <a name="ahcache"></a>!ahcache


**！ Ahcache**扩展显示应用程序兼容性缓存。

```dbgcmd
!ahcache [Flags] 
```

## <a name="span-idddkahcachedbgspanspan-idddkahcachedbgspanparameters"></a><span id="ddk__ahcache_dbg"></span><span id="DDK__AHCACHE_DBG"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
指定要包括在显示的信息。 这可以是以下位 （默认值为零） 的任意组合：

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
显示 RTL\_泛型\_而不是 LRU 列表的表列表。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>4 位 (0x10)  
详细显示： 包含所有项详细信息，而不仅仅是名称。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

 

 





