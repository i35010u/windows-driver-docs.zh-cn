---
title: ubp
description: Ubp 扩展用户空间中设置断点。
ms.assetid: 1aaa6bec-59d3-4e37-a1c6-af3554da809f
keywords:
- ubp Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ubp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9703b641e383cc2cf036817379b9b9e7373a6b48
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334156"
---
# <a name="ubp"></a>!ubp


**！ Ubp**扩展用户空间中设置断点。

```dbgcmd
!ubp Address 
```

## <a name="span-idddkubpdbgspanspan-idddkubpdbgspanparameters"></a><span id="ddk__ubp_dbg"></span><span id="DDK__UBP_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
设置断点的位置的用户空间中指定位置的十六进制虚拟地址。

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

**！ Ubp**扩展用户空间中设置断点。 在实际的物理页上，而不仅仅是虚拟的页上设置断点。

设置物理断点将同时修改每个页上，结果不可预知的虚拟副本。 一个可能的结果是损坏的系统状态，可能是后跟的 bug 检查或其他系统发生崩溃。 因此，这些断点应谨慎，如果根本。

此扩展不能用于已交换内存不足的页上设置断点。 如果页面交换内存不足后设置断点，断点将不再存在。

不能页表或页目录中设置断点。

分配每个断点*断点号*。 若要了解分配的断点号，请使用[ **！ ubl**](-ubl.md)。 在创建时启用断点。 单步执行断点，您必须首先禁用它通过使用[ **！ ubd**](-ubd.md)。 若要清除断点，请使用[ **！ ubc**](-ubc.md)。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**!ubc**](-ubc.md)

[**!ubd**](-ubd.md)

[**!ube**](-ube.md)

[**!ubl**](-ubl.md)

[用户空间和系统空间](user-space-and-system-space.md)

 

 






