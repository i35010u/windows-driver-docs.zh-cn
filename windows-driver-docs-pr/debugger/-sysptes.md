---
title: sysptes
description: Sysptes 扩展显示 (Pte) 的系统页表项的格式化视图。
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
ms.openlocfilehash: c045291ee5226dde3785a5e7cba4b2ef66790e07
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830317"
---
# <a name="sysptes"></a>!sysptes


**！ Sysptes** 扩展显示 (pte) 的系统页表项的格式化视图。

```dbgcmd
!sysptes [Flags]
```

## <a name="span-idddk__sysptes_dbgspanspan-idddk__sysptes_dbgspanparameters"></a><span id="ddk__sysptes_dbg"></span><span id="DDK__SYSPTES_DBG"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
指定要显示的详细信息的级别。 *标志* 可以是以下位的任意组合。 默认值为零：

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
显示免费 Pte 的相关信息。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)   
仅 (Windows 2000) 显示页面使用情况统计信息中未使用的页。

显示有关全局特殊池中可用 Pte 的信息。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)   
显示有关分配给映射锁定页的任何系统 Pte 的详细信息。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>第 3 (0x8)   
 (Windows 2000 和 Windows XP 仅) 显示非分页池扩展可用 PTE 信息。 如果设置了此位，则不显示其他列表。 如果设置了0x1 和0x8，则显示所有非分页池扩展可用 Pte。 如果仅设置了0x8，则只显示合计。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>位 4 (0x10)   
 (Windows Vista 及更高版本) 显示会话的特殊池可用 PTE 信息。

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关页面表和 Pte 的信息，请参阅 *Microsoft Windows 内部机制*，方法是标记 Russinovich 和 David 所罗门群岛。 

<a name="remarks"></a>备注
-------

若要检查特定的 PTE，请使用 [**！ PTE**](-pte.md) 扩展。

下面是 Windows 系统中的一个示例：

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

 

 





