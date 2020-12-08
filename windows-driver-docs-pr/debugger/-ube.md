---
title: u）
description: U) 扩展重新启用用户空间断点。
keywords:
- u) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ube
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2b0bc8e0168837bbe714f24ea2cdbb3fe58237a4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838695"
---
# <a name="ube"></a>!ube


**！ U)** 扩展重新启用用户空间断点。

```dbgcmd
!ube BreakpointNumber 
```

## <a name="span-idddk__ube_dbgspanspan-idddk__ube_dbgspanparameters"></a><span id="ddk__ube_dbg"></span><span id="DDK__UBE_DBG"></span>参数


<span id="_______BreakpointNumber______"></span><span id="_______breakpointnumber______"></span><span id="_______BREAKPOINTNUMBER______"></span>*BreakpointNumber*   
指定要启用的断点号。 星号 (\*) 指示所有断点。

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

这用于重新启用 [**！ ubd**](-ubd.md)禁用的断点。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**!ubc**](-ubc.md)

[**!ubd**](-ubd.md)

[**!ubl**](-ubl.md)

[**!ubp**](-ubp.md)

[用户空间和系统空间](user-space-and-system-space.md)

 

 






