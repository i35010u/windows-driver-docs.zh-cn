---
title: ubc
description: Ubc 扩展会清除用户空间断点。
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
ms.openlocfilehash: dbd00d9199f5c3d07ba824346c587a69df47692a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817573"
---
# <a name="ubc"></a>!ubc


**！ Ubc** 扩展会清除用户空间断点。

```dbgcmd
!ubc BreakpointNumber 
```

## <a name="span-idddk__ubc_dbgspanspan-idddk__ubc_dbgspanparameters"></a><span id="ddk__ubc_dbg"></span><span id="DDK__UBC_DBG"></span>参数


<span id="_______BreakpointNumber______"></span><span id="_______breakpointnumber______"></span><span id="_______BREAKPOINTNUMBER______"></span>*BreakpointNumber*   
指定要清除的断点号。 星号 (\*) 指示所有断点。

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

这将永久删除用 [**！ ubp**](-ubp.md)设置的断点。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**!ubd**](-ubd.md)

[**!ube**](-ube.md)

[**!ubl**](-ubl.md)

[**!ubp**](-ubp.md)

[用户空间和系统空间](user-space-and-system-space.md)

 

 






