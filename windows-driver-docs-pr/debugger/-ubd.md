---
title: ubd
description: Ubd 扩展可临时禁用用户空间断点。
ms.assetid: a639c5e0-111c-45c7-ac7d-6b7e70c1de4f
keywords:
- ubd Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ubd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 25306c912cd649d88880bc7255cec219c90b4678
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334160"
---
# <a name="ubd"></a>!ubd


**！ Ubd**扩展可临时禁用用户空间断点。

```dbgcmd
!ubd BreakpointNumber 
```

## <a name="span-idddkubddbgspanspan-idddkubddbgspanparameters"></a><span id="ddk__ubd_dbg"></span><span id="DDK__UBD_DBG"></span>参数


<span id="_______BreakpointNumber______"></span><span id="_______breakpointnumber______"></span><span id="_______BREAKPOINTNUMBER______"></span> *BreakpointNumber*   
指定要禁用的断点的数目。 一个星号 (\*) 指示所有断点。

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

已禁用的断点将被忽略。 使用[ **！ ube** ](-ube.md)若要重新启用断点。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**!ubc**](-ubc.md)

[**!ube**](-ube.md)

[**!ubl**](-ubl.md)

[**!ubp**](-ubp.md)

[用户空间和系统空间](user-space-and-system-space.md)

 

 






