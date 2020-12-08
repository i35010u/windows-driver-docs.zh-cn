---
title: filetime
description: Filetime 扩展将64位 FILETIME 结构转换为可读的时间。
keywords:
- FILETIME
- filetime Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- filetime
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3b116824db939730857fdc8933333102bd604dca
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821695"
---
# <a name="filetime"></a>!filetime


**！ Filetime** 扩展将64位 filetime 结构转换为可读的时间。

```dbgcmd
!filetime Time
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Time______"></span><span id="_______time______"></span><span id="_______TIME______"></span>*时间*   
指定64位 FILETIME 结构。

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

下面是此扩展的输出示例：

```dbgcmd
kd> !filetime 1c4730984712348
 7/26/2004 04:10:18.712 (Pacific Standard Time)
```

 

 





