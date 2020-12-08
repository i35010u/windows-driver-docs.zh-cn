---
title: pte2va
description: Pte2va 扩展显示与指定页表项相对应 (PTE) 的虚拟地址。
keywords:
- pte2va Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pte2va
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: eab939e624b74aab47eff9563dc704f91d0eb52c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792001"
---
# <a name="pte2va"></a>!pte2va


**！ Pte2va** extension 显示与指定页表项相对应 (PTE) 的虚拟地址。

```dbgcmd
!pte2va Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定 PTE。

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关页面表和 Pte 的信息，请参阅 *Microsoft Windows 内部机制*，方法是标记 Russinovich 和 David 所罗门群岛。 

<a name="remarks"></a>备注
-------

若要检查特定 PTE 的内容，请使用 [**！ PTE**](-pte.md) 扩展。

下面是 **！ pte2va** 扩展的输出示例：

```dbgcmd
kd> !pte2va 9230
000800000248c000 
```

 

 





