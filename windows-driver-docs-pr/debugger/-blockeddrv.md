---
title: blockeddrv
description: Blockeddrv 扩展显示目标计算机上被阻止的驱动程序的列表。
keywords:
- 阻止的驱动程序
- blockeddrv Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- blockeddrv
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0e33586696c68d55858712fed3f8fd1303e1f545
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799977"
---
# <a name="blockeddrv"></a>!blockeddrv


**！ Blockeddrv** extension 显示目标计算机上被阻止的驱动程序的列表。

```dbgcmd
    !blockeddrv
```

## <span id="ddk__blockeddrv_dbg"></span><span id="DDK__BLOCKEDDRV_DBG"></span>


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

 

<a name="remarks"></a>备注
-------

以下是示例：

```dbgcmd
kd> !blockeddrv
Driver:      Status    GUID
afd.sys      0:        {00000008-0206-0001-0000-000030C964E1}
agp440.sys   0:        {0000005C-175A-E12D-5000-010020885580}
atapi.sys    0:        {0000005C-B04A-E12E-5600-000020885580}
audstub.sys  0:        {0000005C-B04A-E12E-5600-000020885580}
Beep.SYS     0:        {0000005C-B04A-E12E-5600-000020885580}
Cdfs.SYS     0:        {00000008-0206-0001-0000-000008F036E1}
.....
```

 

 





