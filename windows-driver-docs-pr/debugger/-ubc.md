---
title: ubc
description: Ubc 扩展清除用户空间断点。
ms.assetid: 4BF2C589-A1C4-4714-B712-DD52D04704D1
keywords:
- ubc Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ubc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fa5cae2e4a05d2af80d6b88f7e4dca7841ea8bfd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545748"
---
# <a name="ubc"></a>!ubc


**！ Ubc**扩展清除用户空间断点。

```dbgcmd
!ubc BreakpointNumber 
```

## <a name="span-idddkubcdbgspanspan-idddkubcdbgspanparameters"></a><span id="ddk__ubc_dbg"></span><span id="DDK__UBC_DBG"></span>参数


<span id="_______BreakpointNumber______"></span><span id="_______breakpointnumber______"></span><span id="_______BREAKPOINTNUMBER______"></span> *BreakpointNumber*   
指定要清除的断点的数目。 一个星号 (\*) 指示所有断点。

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

这将永久删除与设置的断点[ **！ ubp**](-ubp.md)。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**!ubd**](-ubd.md)

[**!ube**](-ube.md)

[**!ubl**](-ubl.md)

[**!ubp**](-ubp.md)

[用户空间和系统空间](user-space-and-system-space.md)

 

 






