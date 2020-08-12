---
title: pte
description: Pte 扩展显示指定地址 (PDE) 的页表条目 (PTE) 和页面目录条目。
ms.assetid: e5603e58-8d9f-4693-bca2-a319080187cc
keywords:
- '页表项 (PTE) '
- 'PTE (页表条目) '
- '页面目录条目 (PDE) '
- 'PDE (页目录条目) '
- pte Windows 调试
ms.date: 05/13/2020
topic_type:
- apiref
api_name:
- pte
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ca587b3e750bd0a926eb5e58508de87465ae1601
ms.sourcegitcommit: bb3b62a57ba3aea4a0adeefd2d81993367b7b334
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88148275"
---
# <a name="pte"></a>!pte

**！ Pte** extension 为指定地址显示页表条目 (pte) 和页面目录条目 (PDE) 。

语法

```dbgcmd
!pte VirtualAddress 
!pte PTE 
!pte LiteralAddress 1 
```

## <a name="span-idddk__pte_dbgspanspan-idddk__pte_dbgspanparameters"></a><span id="ddk__pte_dbg"></span><span id="DDK__PTE_DBG"></span>参数


<span id="_______VirtualAddress______"></span><span id="_______virtualaddress______"></span><span id="_______VIRTUALADDRESS______"></span>*VirtualAddress*   
指定需要其页面表的虚拟地址。

<span id="_______PTE______"></span><span id="_______pte______"></span>*PTE*   
指定实际 PTE 的地址。

<span id="_______LiteralAddress_______1______"></span><span id="_______literaladdress_______1______"></span><span id="_______LITERALADDRESS_______1______"></span>*LiteralAddress*  **** **1**   
指定实际 PTE 或 PDE 的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关页表、页目录和状态位说明的信息，请参阅*Microsoft Windows 内部机制*，其标记为 Russinovich 和 David 所罗门群岛。 

<a name="remarks"></a>备注
-------

如果提供了一个参数，并且此参数是存储页表的内存区域中的地址，则调试器会将其视为*PTE*参数。 此参数被视为所需 PTE 的实际地址，调试器将显示此 PTE 和相应的 PDE。

如果提供了一个参数，并且此参数不是该区域中的地址，则调试器会将其视为*VirtualAddress*参数。 将显示保存此地址的映射的 PTE 和 PDE。

如果提供了两个参数，第二个参数为**1** (或任何其他小数值) ，则调试器会将第一个参数视为*LiteralAddress*。 此地址被解释为 PTE 的实际地址和 PDE 的实际地址，并将显示相应的 (和可能无效的) 数据。

 (x86 或 x64 目标计算机仅) 如果提供了两个参数，第二个参数大于第一个参数，则调试器会将这两个参数视为*StartAddress*和*EndAddress*。 然后，该命令显示指定内存范围内每个页面的 Pte。

有关所有系统 Pte 的列表，请使用[**！ sysptes**](-sysptes.md)扩展。

下面是来自 x86 目标计算机的示例：

```dbgcmd
kd> !pte 801544f4
801544F4  - PDE at C0300800        PTE at C0200550
          contains 0003B163      contains 00154121
        pfn 3b G-DA--KWV    pfn 154 G--A--KRV
```

此示例的第一行重述正在调查的虚拟地址。 然后，它提供 PDE 的虚拟地址和 PTE，其中包含有关此地址的虚拟物理映射的信息。

第二行提供 PDE 和 PTE 的实际内容。

第三行使用这些内容并对其进行分析，将它们分割到页面框架编号 (PFN) 和状态位。

有关如何解释和使用 PFN 的信息，请参阅[**！ pfn**](-pfn.md) extension 或将[虚拟地址转换为物理地址](converting-virtual-addresses-to-physical-addresses.md)部分。

在 x86 或 x64 目标计算机上，下表显示了 PDE 和 PTE 的状态位。 **！ Pte**显示表明这些位带有大写字母或短划线，并添加其他信息。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">bit</th>
<th align="left">设置时显示</th>
<th align="left">清除时显示</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x200</p></td>
<td align="left"><p>C</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>写入时复制。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x100</p></td>
<td align="left"><p>G</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>全局。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x80</p></td>
<td align="left"><p>L</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>大页面。 这仅出现在 PDEs 中，不在 Pte 中。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x40</p></td>
<td align="left"><p>D</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>脏.</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x20</p></td>
<td align="left"><p>A</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>存取.</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"><p>N</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>缓存已禁用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8</p></td>
<td align="left"><p>T</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>写。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>U</p></td>
<td align="left"><p>K</p></td>
<td align="left"><p>所有者 (用户模式或内核模式) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>W</p></td>
<td align="left"><p>R</p></td>
<td align="left"><p>可写或只读。 仅在多处理器计算机和运行 Windows Vista 或更高版本的计算机上。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>V</p></td>
<td align="left"></td>
<td align="left"><p>适用.</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>E</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>可执行文件页。 对于不支持硬件执行/noexecute 位的平台（包括许多 x86 系统），将始终显示 E。</p></td>
</tr>
</tbody>
</table>
