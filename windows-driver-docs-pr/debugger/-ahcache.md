---
title: ahcache
description: Ahcache 扩展会显示应用程序兼容性缓存。
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
ms.openlocfilehash: 8f7725394e1408bb50707b373021eef658f9d489
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800147"
---
# <a name="ahcache"></a>!ahcache


**！ Ahcache** 扩展显示应用程序兼容性缓存。

```dbgcmd
!ahcache [Flags] 
```

## <a name="span-idddk__ahcache_dbgspanspan-idddk__ahcache_dbgspanparameters"></a><span id="ddk__ahcache_dbg"></span><span id="DDK__AHCACHE_DBG"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
指定要包含在显示中的信息。 这可以是以下位的任意组合 (默认值为零) ：

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
显示 RTL \_ 泛型 \_ 表列表，而不是 LRU 列表。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>位 4 (0x10)   
详细显示：包括所有条目详细信息，而不仅仅是名称。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

 

 





