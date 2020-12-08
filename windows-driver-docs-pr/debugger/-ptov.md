---
title: ptov
description: Ptov 扩展显示给定进程的整个物理到虚拟映射。
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
ms.openlocfilehash: 52aeccf365ac674b9459294077540538151896a0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837589"
---
# <a name="ptov"></a>!ptov


**！ Ptov** 扩展显示给定进程的整个物理到虚拟图。

```dbgcmd
!ptov DirBase
```

## <a name="span-idddk__ptov_dbgspanspan-idddk__ptov_dbgspanparameters"></a><span id="ddk__ptov_dbg"></span><span id="DDK__PTOV_DBG"></span>参数


<span id="_______DirBase______"></span><span id="_______dirbase______"></span><span id="_______DIRBASE______"></span>*DirBase*   
指定进程的目录库。 若要确定目录基础，请使用 [**！ process**](-process.md) 命令，并查看 DirBase 显示的值。

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

 

<a name="remarks"></a>备注
-------

示例如下。 首先，使用 [**. process**](-process--set-process-context-.md) 和 [**！进程**](-process.md) 来确定当前进程的目录基：

```dbgcmd
1: kd> .process
Implicit process is now 852b4040
1: kd> !process 852b4040 1
PROCESS 852b4040  SessionId: none  Cid: 0004    Peb: 00000000  ParentCid: 0000
    DirBase: 00185000  ObjectTable: 83203000  HandleCount: 663.
    Image: System
    ...
```

在这种情况下，目录基为0x00185000。 将此地址传递给 **！ ptov**：

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

左栏中的数字是具有此进程映射的每个内存页的物理地址。 右侧列中的数字是它们所映射到的虚拟地址。

总显示时间非常长。

下面是一个64位示例。

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

目录基是在虚拟地址转换中使用的第一个表的物理地址。 此表具有不同的名称，具体取决于目标操作系统的位数以及对于目标操作系统是否启用了物理地址扩展 (PAE) 。

对于64位 Windows，目录基是页映射级别 4 (PML4) 表的物理地址。 对于启用了 PAE 的32位 Windows，目录库是 (PDP) 表的页面目录指针的物理地址。 对于禁用了 PAE 的32位 Windows，目录 bas 是页面目录 (PD) 表的物理地址。

相关主题，请参阅 [**！ vtop**](-vtop.md) 和 [将虚拟地址转换为物理地址](converting-virtual-addresses-to-physical-addresses.md)。 有关虚拟地址转换的信息，请参阅 *Microsoft Windows 内部机制*，方法是标记 Russinovich 和 David 所罗门群岛。

 

 





