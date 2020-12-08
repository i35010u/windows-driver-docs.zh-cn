---
title: kuser
description: Kuser 扩展显示 (KUSER_SHARED_DATA) 的 "共享用户模式" 页。
keywords:
- kuser Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- kuser
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0acbb9d42d28c6517e455207e18b4a0c11bc7951
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804051"
---
# <a name="kuser"></a>!kuser


**！ Kuser** 扩展显示共享用户模式页面 (kuser \_ 共享 \_ 数据) 。

```dbgcmd
!kuser 
```

## <span id="ddk__kuser_dbg"></span><span id="DDK__KUSER_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p></p>
Kdextx86.dll Ntsdexts.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Exts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

"KUSER \_ 共享 \_ 数据" 页提供了有关当前登录用户的资源和其他信息。

示例如下。 请注意，在此示例中，滴答计数以原始形式显示，并以更适合用户的形式显示在括号中。 用户友好的显示仅在 Windows XP 和更高版本中可用。

```dbgcmd
kd> !kuser
_KUSER_SHARED_DATA at 7ffe0000
TickCount:    fa00000 * 00482006 (0:20:30:56.093)
TimeZone Id: 2
ImageNumber Range: [14c .. 14c]
Crypto Exponent: 0
SystemRoot: 'F:\WINDOWS'
```

 

 





