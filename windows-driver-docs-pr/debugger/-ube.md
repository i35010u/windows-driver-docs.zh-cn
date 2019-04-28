---
title: ube
description: Ube 扩展将重新启用用户空间断点。
ms.assetid: caa13c30-e03a-44fd-9221-66e44eec88af
keywords:
- ube Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ube
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1eb9555fb292fadc4aa65987aa70bf4a08f2b625
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334154"
---
# <a name="ube"></a>!ube


**！ Ube**扩展将重新启用用户空间断点。

```dbgcmd
!ube BreakpointNumber 
```

## <a name="span-idddkubedbgspanspan-idddkubedbgspanparameters"></a><span id="ddk__ube_dbg"></span><span id="DDK__UBE_DBG"></span>参数


<span id="_______BreakpointNumber______"></span><span id="_______breakpointnumber______"></span><span id="_______BREAKPOINTNUMBER______"></span> *BreakpointNumber*   
指定要启用的断点的数目。 一个星号 (\*) 指示所有断点。

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

这用来重新启用已被禁用的断点[ **！ ubd**](-ubd.md)。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**!ubc**](-ubc.md)

[**!ubd**](-ubd.md)

[**!ubl**](-ubl.md)

[**!ubp**](-ubp.md)

[用户空间和系统空间](user-space-and-system-space.md)

 

 






