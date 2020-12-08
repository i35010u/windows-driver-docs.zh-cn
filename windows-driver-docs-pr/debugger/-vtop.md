---
title: vtop
description: Vtop 扩展将虚拟地址转换为相应的物理地址，并显示其他页面表和页面目录信息。
keywords:
- vtop Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- vtop
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6b2bc7d19a10432205560cdb4e3d7965f19ae926
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839175"
---
# <a name="vtop"></a>!vtop


**！ Vtop** extension 将虚拟地址转换为相应的物理地址，并显示其他页面表和页面目录信息。

语法

```dbgcmd
!vtop PFN VirtualAddress 
!vtop 0 VirtualAddress 
```

## <a name="span-idddk__vtop_dbgspanspan-idddk__vtop_dbgspanparameters"></a><span id="ddk__vtop_dbg"></span><span id="DDK__VTOP_DBG"></span>参数


<span id="_______DirBase______"></span><span id="_______dirbase______"></span><span id="_______DIRBASE______"></span>*DirBase*   
指定进程的目录库。 每个进程都有其自己的虚拟地址空间。 使用 [**！进程**](-process.md) 扩展来确定进程的目录库。

<span id="_______PFN______"></span><span id="_______pfn______"></span>*PFN*   
指定进程 (的目录基) 的页面帧号。

<span id="_______0______"></span>**0**   
导致 **！ vtop** 使用当前 [进程上下文](changing-contexts.md#process-context) 进行地址转换。

<span id="_______VirtualAddress______"></span><span id="_______virtualaddress______"></span><span id="_______VIRTUALADDRESS______"></span>*VirtualAddress*   
指定需要其页面的虚拟地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关实现这些结果的其他方法，请参阅 [将虚拟地址转换为物理地址](converting-virtual-addresses-to-physical-addresses.md)。 另请参阅 [**！ ptov**](-ptov.md)。 有关页表和页目录的信息，请参阅 Russinovich 和 David 所罗门群岛的 *Microsoft Windows 内部机制*。

<a name="remarks"></a>备注
-------

若要使用此命令，请先使用 [**！进程**](-process.md) 扩展来确定进程的目录库。 可以通过删除三个尾随十六进制零来查找此目录基础 (PFN) 的页面帧号， (用鼠标右键将这三个尾随十六进制零右移) 。

以下是示例：

```dbgcmd
kd> !process 0 0
**** NT ACTIVE PROCESS DUMP ****
....
PROCESS ff779190  SessionId: 0  Cid: 04fc    Peb: 7ffdf000  ParentCid: 0394
 DirBase: 098fd000  ObjectTable: e1646b30  TableSize:   8.
    Image: MyApp.exe
```

由于目录基为0x098FD000，因此其 PFN 为0x098FD。

```dbgcmd
kd> !vtop 98fd 12f980
Pdi 0 Pti 12f
0012f980 09de9000 pfn(09de9)
```

请注意，尾随三个零是可选的。 **！ Vtop** extension 显示了页目录索引 (PDI) 、页表索引 (PTI) 、最初所输入的虚拟地址、物理页开头的物理地址，以及页表项 (PTE) 的页帧号 (PFN) 。

如果要将虚拟地址0x0012F980 转换为物理地址，只需使用最后三个十六进制数字 (0x980) ，并将其添加到 (0x09DE9000) 页面开头的物理地址。 这会提供0x09DE9980 的物理地址。

如果忘记删除三个零，并将完整目录基数传递到 **！ vtop** 而不是 PFN，则结果通常是正确的。 这是因为当 **！ vtop** 接收到的数字太大而无法成为 PFN 时，它会将它右移十二位，并改为使用该数字：

```dbgcmd
kd> !vtop 98fd 12f980
Pdi 0 Pti 12f
0012f980 09de9000 pfn(09de9)

kd> !vtop 98fd000 12f980
Pdi 0 Pti 12f
0012f980 09de9000 pfn(09de9)
```

但是，最好始终使用 PFN，因为某些目录基值不会以这种方式进行转换。

 

 





