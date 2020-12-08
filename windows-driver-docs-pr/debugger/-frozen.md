---
title: frozen
description: 冻结扩展显示每个处理器的状态。
keywords:
- 处理器状态
- 已冻结 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- frozen
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 022330fcd803e0913b188b1c9b7a9aa82979489d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821065"
---
# <a name="frozen"></a>!frozen


**！冻结** 扩展显示每个处理器的状态。

```dbgcmd
!frozen
```

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

下面是此扩展的输出示例：

```dbgcmd
0: kd> !frozen
Processor states:
       0 : Current
       1 : Frozen
```

 

 





