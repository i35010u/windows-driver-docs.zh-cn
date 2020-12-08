---
title: memlist
description: Memlist 扩展会扫描页面帧编号 (PFN) 数据库中的物理内存列表，以便检查它们的一致性。
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
ms.openlocfilehash: e47e2f4ae7ce5737a9030207ac8cccbcd6dc6555
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795733"
---
# <a name="memlist"></a>!memlist


**！ Memlist** extension) 数据库中扫描页面帧号 (PFN 的物理内存列表，以检查它们是否一致。

```dbgcmd
!memlist Flags
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
指定要验证的内存列表。 目前仅实现了一个值：

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
导致验证 "零页" 列表。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

目前，此扩展将仅检查 "归零页" 列表以确保该列表中的所有页面都归零。 正确的语法为：

```dbgcmd
kd> !memlist 1
```

 

 





