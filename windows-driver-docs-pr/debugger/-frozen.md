---
title: 冻结
description: 冻结的扩展显示每个处理器的状态。
ms.assetid: aa2761b7-e7e1-435e-98d3-bfaac64925bf
keywords:
- 处理器状态
- 冻结 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- frozen
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 40987edacdd353979b69b7f56cb3d57784573d3a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336653"
---
# <a name="frozen"></a>!frozen


**！ 冻结**扩展显示每个处理器的状态。

```dbgcmd
!frozen
```

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

下面是输出的来自此扩展插件示例：

```dbgcmd
0: kd> !frozen
Processor states:
       0 : Current
       1 : Frozen
```

 

 





