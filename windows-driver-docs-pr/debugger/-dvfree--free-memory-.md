---
title: .dvfree（释放内存）
description: Dvfree 命令释放目标进程所拥有的内存分配。
keywords:
- 。 dvfree (可用内存) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .dvfree (Free Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 96affea6e9fa733059d5dbeffdb0e4ddc392fa16
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792439"
---
# <a name="dvfree-free-memory"></a>.dvfree（释放内存）


**Dvfree** 命令释放目标进程所拥有的内存分配。

```dbgcmd
.dvfree [/d] BaseAddress Size 
```

## <a name="span-idddk_meta_free_memory_dbgspanspan-idddk_meta_free_memory_dbgspanparameters"></a><span id="ddk_meta_free_memory_dbg"></span><span id="DDK_META_FREE_MEMORY_DBG"></span>参数


<span id="________d______"></span><span id="________D______"></span>**/d**   
解除分配，但不实际释放包含分配的页面。 如果使用此选项，则调试器将调用 **VirtualFreeEx** ，并将 *DWFREETYPE* 参数等于 MEM \_ 解除。 如果未使用此选项，则使用值 MEM \_ RELEASE。 有关详细信息，请参阅 Microsoft Windows SDK。

<span id="_______BaseAddress______"></span><span id="_______baseaddress______"></span><span id="_______BASEADDRESS______"></span>*BaseAddress*   
指定分配开始的虚拟地址。

<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span>*大小*   
指定要释放的内存量（以字节为单位）。 已释放的实际内存将始终为大量内存页。

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

**Dvfree** 命令调用 **VirtualFreeEx** 以释放现有的内存分配。 除非指定了 **/d** 选项，否则将释放包含此内存的页面。

此命令可用于释放由 [**. dvalloc (分配内存)**](-dvalloc--allocate-memory-.md)的分配。 它还可用于释放目标进程所拥有的任何内存块，但释放未通过获取的内存 **。 dvalloc** 自然会给出目标进程的稳定性带来的风险。

 

 





