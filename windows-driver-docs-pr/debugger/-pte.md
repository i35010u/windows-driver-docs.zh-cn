---
title: pte
description: Pte 扩展显示的页表项 (PTE) 和页目录项 (PDE) 指定的地址。
ms.assetid: e5603e58-8d9f-4693-bca2-a319080187cc
keywords:
- 页表项 (PTE)
- PTE （页表项）
- 页目录条目 (PDE)
- PDE （页目录条目）
- pte Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pte
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 53e09839a54bf11b2b625105b470aed19d004bce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541468"
---
# <a name="pte"></a>！ pte


**！ Pte**扩展显示的页表项 (PTE) 和页目录项 (PDE) 指定的地址。

语法

```dbgcmd
!pte VirtualAddress 
!pte PTE 
!pte LiteralAddress 1 
```

## <a name="span-idddkptedbgspanspan-idddkptedbgspanparameters"></a><span id="ddk__pte_dbg"></span><span id="DDK__PTE_DBG"></span>参数


<span id="_______VirtualAddress______"></span><span id="_______virtualaddress______"></span><span id="_______VIRTUALADDRESS______"></span> *VirtualAddress*   
指定的页表所需的虚拟地址。

<span id="_______PTE______"></span><span id="_______pte______"></span> *PTE*   
指定实际 PTE 的地址。

<span id="_______LiteralAddress_______1______"></span><span id="_______literaladdress_______1______"></span><span id="_______LITERALADDRESS_______1______"></span> *LiteralAddress* **** **1**   
指定实际 PTE 或 PDE 的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

页表、 页目录和的状态位说明有关的信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。 （这本书不可能在某些语言和国家/地区中可用。）

<a name="remarks"></a>备注
-------

如果提供一个参数，此参数为页表的存储位置的内存区域中的地址，调试器会将此视为*PTE*参数。 此参数被视为所需的 PTE 的实际地址，调试器将显示此 PTE 和相应 PDE。

如果提供一个参数，此参数不是此区域中的地址，调试器将此视为*VirtualAddress*参数。 显示 PTE 和 PDE 保存为此地址的映射。

如果提供了两个参数并按第二个参数是**1** （或任何其他小的数字），调试器将第一个参数视为*LiteralAddress*。 此地址解释 PTE 的实际地址，而且还为 PDE 的实际地址并且将显示相应的 （和可能是无效的） 数据。

（x86 或 x64 目标计算机仅）如果提供了两个参数并第二个参数是否大于第一个，则调试器将两个参数视为*StartAddress*并*EndAddress*。 然后，该命令中指定的内存范围显示每个页面 Pte。

所有系统 Pte 的列表，请[ **！ sysptes** ](-sysptes.md)扩展。

下面是一个示例从 x86 目标计算机：

```dbgcmd
kd> !pte 801544f4
801544F4  - PDE at C0300800        PTE at C0200550
          contains 0003B163      contains 00154121
        pfn 3b G-DA--KWV    pfn 154 G--A--KRV
```

此示例中的第一行重述正在调查的虚拟地址。 然后，它提供的虚拟地址 PDE 和 PTE，其中包含有关虚拟物理映射此地址的信息。

第二个行可提供 PDE 和 PTE 的实际内容。

第三行采用这些内容，并会分析，将它们分解成页帧数 (PFN) 和状态位。

请参阅[ **！ pfn** ](-pfn.md)扩展或[转换到物理地址的虚拟地址](converting-virtual-addresses-to-physical-addresses.md)部分，了解有关如何解释和使用 PFN 的信息。

在 x86 或 x64 目标计算机上，在下表显示 PDE 和 PTE 状态位。 **！ Pte**显示指示与大写字母或短划线，这些位并将添加其他信息。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">位</th>
<th align="left">显示时设置</th>
<th align="left">显示时清除</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x200</p></td>
<td align="left"><p>C</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>将复制中写入。</p></td>
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
<td align="left"><p>大型页。 这只是在 PDEs，永远不会在 Pte。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x40</p></td>
<td align="left"><p>D</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>脏页。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x20</p></td>
<td align="left"><p>A</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"><p>N</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>禁用缓存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8</p></td>
<td align="left"><p>T</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>写通式。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>U</p></td>
<td align="left"><p>K</p></td>
<td align="left"><p>（用户模式或内核模式） 的所有者。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>W</p></td>
<td align="left"><p>R</p></td>
<td align="left"><p>可写或只读的。 仅在多处理器计算机和任何计算机上运行 Windows Vista 或更高版本。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>V</p></td>
<td align="left"></td>
<td align="left"><p>有效。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>E</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>可执行文件的页。 不支持硬件执行/noexecute 位的平台，其中包括许多 x86 系统，E 始终显示出来。</p></td>
</tr>
</tbody>
</table>

 

在 Itanium 目标计算机上，是略有不同的 PPE PDE 和 PTE 状态位。 Itanium PPE 位如下所示：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">显示时设置</th>
<th align="left">显示时清除</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>V</p></td>
<td align="left"></td>
<td align="left"><p>有效。</p></td>
</tr>
<tr class="even">
<td align="left"><p>U</p></td>
<td align="left"><p>K</p></td>
<td align="left"><p>（用户模式或内核模式） 的所有者。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>脏页。</p></td>
</tr>
<tr class="even">
<td align="left"><p>A</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>访问。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>W</p></td>
<td align="left"><p>R</p></td>
<td align="left"><p>可写或只读的。 仅在多处理器计算机和任何计算机上运行 Windows Vista 或更高版本。</p></td>
</tr>
<tr class="even">
<td align="left"><p>E</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>执行。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>C</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>将复制中写入。</p></td>
</tr>
</tbody>
</table>

 

 

 





