---
title: vtop
description: Vtop 扩展将虚拟地址转换为相应的物理地址，并显示其他页表和页目录信息。
ms.assetid: 41f4accc-3eb9-4406-a6cc-a05022166e14
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
ms.openlocfilehash: 343265d0d42a14ed1c0780ca66831e8112d60234
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533956"
---
# <a name="vtop"></a>！ vtop


**！ Vtop**扩展将虚拟地址转换为相应的物理地址，并显示其他页表和页目录信息。

语法

```dbgcmd
!vtop PFN VirtualAddress 
!vtop 0 VirtualAddress 
```

## <a name="span-idddkvtopdbgspanspan-idddkvtopdbgspanparameters"></a><span id="ddk__vtop_dbg"></span><span id="DDK__VTOP_DBG"></span>参数


<span id="_______DirBase______"></span><span id="_______dirbase______"></span><span id="_______DIRBASE______"></span> *DirBase*   
指定的目录基础的过程。 每个进程具有自己的虚拟地址空间。 使用[ **！ 过程**](-process.md)扩展来确定进程的目录基础。

<span id="_______PFN______"></span><span id="_______pfn______"></span> *PFN*   
指定的进程的目录基础页帧数 (PFN)。

<span id="_______0______"></span> **0**   
将导致 **！ vtop**以使用当前[进程上下文](changing-contexts.md#process-context)地址转换。

<span id="_______VirtualAddress______"></span><span id="_______virtualaddress______"></span><span id="_______VIRTUALADDRESS______"></span> *VirtualAddress*   
指定所需的页的虚拟地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关实现这些结果的其他方法，请参阅[转换到物理地址的虚拟地址](converting-virtual-addresses-to-physical-addresses.md)。 另请参阅[ **！ ptov**](-ptov.md)。 有关页表和页目录中的信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。

<a name="remarks"></a>备注
-------

若要使用此命令，首先使用[ **！ 过程**](-process.md)扩展来确定进程的目录基。 可以通过删除 （即，通过右移位数 12 位） 的三个尾随十六进制零找到此目录基础的页帧数 (PFN)。

下面是一个示例：

```dbgcmd
kd> !process 0 0
**** NT ACTIVE PROCESS DUMP ****
....
PROCESS ff779190  SessionId: 0  Cid: 04fc    Peb: 7ffdf000  ParentCid: 0394
 DirBase: 098fd000  ObjectTable: e1646b30  TableSize:   8.
    Image: MyApp.exe
```

由于目录基本 0x098FD000，其 PFN 是 0x098FD。

```dbgcmd
kd> !vtop 98fd 12f980
Pdi 0 Pti 12f
0012f980 09de9000 pfn(09de9)
```

请注意三个的尾随零都是可选的。 **！ Vtop**扩展显示页目录索引 (PDI)、 页表索引 (PTI)，最初必须输入的虚拟地址、 物理页的页帧数 (PFN) 开头的物理地址页表项 (PTE)。

如果你想要将虚拟地址 0x0012F980 转换为物理地址，只需具有执行最后三个十六进制数字 (0x980) 并将其添加到网页 (0x09DE9000) 的开头的物理地址。 这样，0x09DE9980 的物理地址。

如果你忘记了删除的三个零，并将完整目录传递到基 **！ vtop**而不是 PFN，结果通常是正确的。 这是因为当 **！ vtop**接收数字太大，无法 PFN，它右移位它 12 位，并改为数字的使用：

```dbgcmd
kd> !vtop 98fd 12f980
Pdi 0 Pti 12f
0012f980 09de9000 pfn(09de9)

kd> !vtop 98fd000 12f980
Pdi 0 Pti 12f
0012f980 09de9000 pfn(09de9)
```

但是，它是更好的做法始终使用 PFN，因为某些目录基础值不会以这种方式进行转换。

 

 





