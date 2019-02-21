---
title: pte2va
description: Pte2va 扩展到指定的页表项 (PTE) 显示对应的虚拟地址。
ms.assetid: 9a94ce3a-dbbc-4566-9ef5-3ec76c1505eb
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
ms.openlocfilehash: 0582e1cffaad68efee46529b86b3f8915f09f6cb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544341"
---
# <a name="pte2va"></a>!pte2va


**！ Pte2va**扩展到指定的页表项 (PTE) 显示对应的虚拟地址。

```dbgcmd
!pte2va Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定将 PTE。

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

页表和 Pte 有关的信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。 （这本书不可能在某些语言和国家/地区中可用。）

<a name="remarks"></a>备注
-------

若要检查的特定 PTE 内容，请使用[ **！ pte** ](-pte.md)扩展。

下面是输出的示例 **！ pte2va**扩展：

```dbgcmd
kd> !pte2va 9230
000800000248c000 
```

 

 





