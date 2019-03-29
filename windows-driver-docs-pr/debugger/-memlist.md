---
title: memlist
description: Memlist 扩展扫描从页帧数 (PFN) 数据库的物理内存列表以检查它们的一致性。
ms.assetid: 9d5307df-5e46-4d95-8c96-ab6da0f54cd0
keywords:
- PFN 数据库
- memlist Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- memlist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 90b8b877ec4f6e8cbb6b9be8015f7a49dd528862
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563504"
---
# <a name="memlist"></a>!memlist


**！ Memlist**扩展扫描从页帧数 (PFN) 数据库的物理内存列表以检查它们的一致性。

```dbgcmd
!memlist Flags
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
指定要验证哪些内存列表。 目前，已实现只有一个值：

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
导致要验证的清零的页列表。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

目前，此扩展仅会检查清零的页列表，以确保该列表中的所有页面均被清都零。 合适的语法是：

```dbgcmd
kd> !memlist 1
```

 

 





