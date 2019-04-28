---
title: filetime
description: Filetime 扩展将人读时间转换为 64 位 FILETIME 结构。
ms.assetid: 26ee9219-ad37-4b0e-b204-5ed6d93355b0
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
ms.openlocfilehash: d3bb5075a06875a4f18b04dd415fb25b5ea9bb4e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336730"
---
# <a name="filetime"></a>!filetime


**！ Filetime**扩展将人读时间转换为 64 位 FILETIME 结构。

```dbgcmd
!filetime Time
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Time______"></span><span id="_______time______"></span><span id="_______TIME______"></span> *时间*   
指定 64 位 FILETIME 结构。

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

下面是输出的来自此扩展插件示例：

```dbgcmd
kd> !filetime 1c4730984712348
 7/26/2004 04:10:18.712 (Pacific Standard Time)
```

 

 





