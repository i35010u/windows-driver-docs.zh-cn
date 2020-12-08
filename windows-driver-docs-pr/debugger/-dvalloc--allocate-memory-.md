---
title: .dvalloc（分配内存）
description: Dvalloc 命令使 Windows 向目标进程分配额外的内存。
keywords:
- dvalloc () Windows 调试分配内存
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .dvalloc (Allocate Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 19c748262c3cffa9dcc9b6ea58d53daf8cb76370
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799895"
---
# <a name="dvalloc-allocate-memory"></a>.dvalloc（分配内存）


**Dvalloc** 命令使 Windows 向目标进程分配额外的内存。

```dbgcmd
.dvalloc [Options] Size 
```

## <a name="span-idddk_meta_allocate_memory_dbgspanspan-idddk_meta_allocate_memory_dbgspanparameters"></a><span id="ddk_meta_allocate_memory_dbg"></span><span id="DDK_META_ALLOCATE_MEMORY_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
可以是下列任意数量的选项：

<span id="_b_BaseAddress"></span><span id="_b_baseaddress"></span><span id="_B_BASEADDRESS"></span>**/b**  **** *BaseAddress*  
指定分配开始的虚拟地址。

<span id="_r"></span><span id="_R"></span>**/r**  
保留虚拟地址空间中的内存，但不会实际分配任何物理内存。 如果使用此选项，则调试器将调用 **VirtualAllocEx** ，并将 *FLALLOCATIONTYPE* 参数等于内存 \_ 预留。 如果未使用此选项，则值 "将 \_ 提交 |\_使用内存预留。 有关详细信息，请参阅 Microsoft Windows SDK。

<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span>*大小*   
指定要分配的内存量（以字节为单位）。 可用于该程序的内存量将等于 *大小*。 实际使用的内存量可能略大一些，因为它始终是整页。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**Dvalloc** 命令调用 **VirtualAllocEx** 为目标进程分配新内存。 分配的内存允许读取、写入和执行。

若要释放此内存，请使用 [**dvfree (可用内存)**](-dvfree--free-memory-.md)。

 

 





