---
title: .dvalloc（分配内存）
description: .Dvalloc 命令会使 Windows 以分配到目标进程的更多内存。
ms.assetid: 5bb0660e-0c88-4100-91ae-cd89834174f6
keywords:
- .dvalloc （分配内存） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .dvalloc (Allocate Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: de3632868528e71ccb078994bef77aee64d83709
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336868"
---
# <a name="dvalloc-allocate-memory"></a>.dvalloc（分配内存）


**.Dvalloc**命令将导致 Windows 以分配到目标进程的更多内存。

```dbgcmd
.dvalloc [Options] Size 
```

## <a name="span-idddkmetaallocatememorydbgspanspan-idddkmetaallocatememorydbgspanparameters"></a><span id="ddk_meta_allocate_memory_dbg"></span><span id="DDK_META_ALLOCATE_MEMORY_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
可以是任意数量的以下选项：

<span id="_b_BaseAddress"></span><span id="_b_baseaddress"></span><span id="_B_BASEADDRESS"></span>**/b** **** *BaseAddress*  
指定分配的开头的虚拟地址。

<span id="_r"></span><span id="_R"></span>**/r**  
保留虚拟地址空间中的内存，但不会实际分配的物理内存。 如果使用此选项，调试器将调用**VirtualAllocEx**与*flAllocationType*参数等于内存优化\_保留。 如果不使用此选项，内存优化的值\_提交 |内存优化\_使用保留。 请参阅 Microsoft Windows SDK 的详细信息。

<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span> *大小*   
指定要以字节为单位分配的内存量。 可用程序内存量将等于*大小*。 实际使用量可能会稍大一些，因为它始终是内存的整数数量的页。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>仅限用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**.Dvalloc**命令调用**VirtualAllocEx**分配新内存来存放目标进程。 已分配的内存允许读取、 写入和执行。

若要释放此内存，请使用[ **.dvfree （可用内存）**](-dvfree--free-memory-.md)。

 

 





