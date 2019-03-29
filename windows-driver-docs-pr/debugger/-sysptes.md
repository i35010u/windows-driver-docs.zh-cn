---
title: sysptes
description: Sysptes 扩展显示系统页表项 (Pte) 格式化的的视图。
ms.assetid: cfb40732-6658-43aa-8b83-0ad4b55194ba
keywords:
- sysptes Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- sysptes
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 75066ef7201fb1112eeb1f26145ca310e4166c98
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569501"
---
# <a name="sysptes"></a>!sysptes


**！ Sysptes**扩展显示的系统页表项 (Pte) 格式化的视图。

```dbgcmd
!sysptes [Flags]
```

## <a name="span-idddksysptesdbgspanspan-idddksysptesdbgspanparameters"></a><span id="ddk__sysptes_dbg"></span><span id="DDK__SYSPTES_DBG"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
指定要显示详细信息的级别。 *标志*可以是以下位的任意组合。 默认值为零：

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
显示免费 Pte 有关的信息。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
(仅适用于 Windows 2000)在页使用情况统计信息中显示未使用的页。

显示有关免费 Pte 全局特殊池中的信息。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
显示详细的信息的任何系统 Pte 分配到映射的锁定页。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>位 3 (0x8)  
（Windows 2000 和 Windows XP 仅）显示非分页缓冲的池扩展免费 PTE 信息。 如果设置此位，则将不会显示其他列表。 如果 0x1 和 0x8 免费 Pte 显示设置此选项，所有非分页缓冲池扩展。 如果仅设置 0x8，将显示仅总数。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>4 位 (0x10)  
(Windows Vista 及更高版本)显示会话的特殊池免费 PTE 信息。

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

页表和 Pte 有关的信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。 

<a name="remarks"></a>备注
-------

若要检查特定 PTE，使用[ **！ pte** ](-pte.md)扩展。

下面是 Windows 系统中的示例：

```dbgcmd
kd> !sysptes 1

System PTE Information
  Total System Ptes 571224
     SysPtes list of size 1 has 361 free
     SysPtes list of size 2 has 91 free
     SysPtes list of size 4 has 48 free
     SysPtes list of size 8 has 36 free
     SysPtes list of size 9 has 29 free
     SysPtes list of size 23 has 29 free
 
    starting PTE: fffffe0059388000
    ending PTE:   fffffe00597e3ab8

      free ptes: fffffe0059388000   number free: 551557.
      free ptes: fffffe00597be558   number free: 104.
      free ptes: fffffe00597d2828   number free: 676.

  free blocks: 3   total free: 552337    largest free block: 551557
```

 

 





