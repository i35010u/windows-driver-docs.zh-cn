---
title: ptov
description: Ptov 扩展显示为给定进程的整个物理到虚拟映射。
ms.assetid: 82352d12-4e81-4746-9333-b2cc98eb7a9d
keywords:
- ptov Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ptov
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 586f99d53184a7a0110ee06855beed897f1db97a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334328"
---
# <a name="ptov"></a>!ptov


**！ Ptov**扩展显示给定进程的整个物理到虚拟代码图。

```dbgcmd
!ptov DirBase
```

## <a name="span-idddkptovdbgspanspan-idddkptovdbgspanparameters"></a><span id="ddk__ptov_dbg"></span><span id="DDK__PTOV_DBG"></span>参数


<span id="_______DirBase______"></span><span id="_______dirbase______"></span><span id="_______DIRBASE______"></span> *DirBase*   
指定的目录基础的过程。 若要确定目录基，使用[ **！ 过程**](-process.md)命令，并查看为 DirBase 显示的值。

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

 

<a name="remarks"></a>备注
-------

下面是一个示例。 首先，使用[ **.process** ](-process--set-process-context-.md)并[ **！ 过程**](-process.md)来确定当前进程的目录基：

```dbgcmd
1: kd> .process
Implicit process is now 852b4040
1: kd> !process 852b4040 1
PROCESS 852b4040  SessionId: none  Cid: 0004    Peb: 00000000  ParentCid: 0000
    DirBase: 00185000  ObjectTable: 83203000  HandleCount: 663.
    Image: System
    ...
```

在这种情况下，目录基数是 0x00185000。 传递到此地址 **！ ptov**:

```dbgcmd
1: kd> !ptov 185000
X86PtoV: pagedir 185000, PAE enabled.
15e11000 10000
549e6000 20000
...
60a000 210000
40b000 211000
...
54ad3000 25f000
548d3000 260000
...
d71000 77510000
...
```

左侧列中的数字是每个具有此过程的映射的内存页的物理地址。 右侧列中的数字是映射到的虚拟地址。

总显示为非常长。

下面是一个 64 位的示例。

```dbgcmd
3: kd> .process
Implicit process is now fffffa80`0361eb30
3: kd> !process fffffa80`0361eb30 1
PROCESS fffffa800361eb30
    SessionId: none  Cid: 0004    Peb: 00000000  ParentCid: 0000
    DirBase: 00187000  ObjectTable: fffff8a000002870  HandleCount: 919.
    Image: System
    ...
3: kd> !ptov 187000
Amd64PtoV: pagedir 187000
00000001`034fb000 1d0000
a757c000 1d1000
00000001`0103d000 1d2000
c041e000 1d3000
...
2ed6f000 fffff680`00001000
00000001`13939000 fffff680`00003000
ceefb000 fffff680`00008000
...
```

Directory base 是第一个表中的虚拟地址转换使用的物理地址。 此表具有不同的名称，具体取决于目标操作系统和物理地址扩展 (PAE) 是否已启用的目标操作系统的位数。

对于 64 位 Windows 目录基数是 4 页映射级别 (PML4) 表的物理地址。 对于启用了 PAE 32 位 Windows，directory base 是页目录指针 (PDP) 表的物理地址。 对于使用 PAE 禁用的 32 位 Windows，directory bas 是页目录 (PD) 表的物理地址。

相关主题，请参阅[ **！ vtop** ](-vtop.md)并[转换到物理地址的虚拟地址](converting-virtual-addresses-to-physical-addresses.md)。 有关虚拟地址转换的信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。 （这些资源可能不可用在某些语言和国家/地区中。）

 

 





