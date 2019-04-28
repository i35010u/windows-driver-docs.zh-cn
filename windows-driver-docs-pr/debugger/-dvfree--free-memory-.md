---
title: .dvfree（释放内存）
description: .Dvfree 命令释放所拥有的目标进程的内存分配。
ms.assetid: 46845a5c-6ec4-4ae4-b89d-886df367dc5e
keywords:
- .dvfree （可用内存） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .dvfree (Free Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e65add81d64a3818c45061001879a5692f30f72a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334552"
---
# <a name="dvfree-free-memory"></a>.dvfree（释放内存）


**.Dvfree**命令释放所拥有的目标进程的内存分配。

```dbgcmd
.dvfree [/d] BaseAddress Size 
```

## <a name="span-idddkmetafreememorydbgspanspan-idddkmetafreememorydbgspanparameters"></a><span id="ddk_meta_free_memory_dbg"></span><span id="DDK_META_FREE_MEMORY_DBG"></span>参数


<span id="________d______"></span><span id="________D______"></span> **/d**   
解除分配，但不会实际释放包含分配的页。 如果使用此选项，调试器将调用**VirtualFreeEx**与*dwFreeType*参数等于内存优化\_回收时。 如果不使用此选项，内存优化的值\_使用版本。 请参阅 Microsoft Windows SDK 的详细信息。

<span id="_______BaseAddress______"></span><span id="_______baseaddress______"></span><span id="_______BASEADDRESS______"></span> *BaseAddress*   
指定分配的开头的虚拟地址。

<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span> *大小*   
指定要释放，以字节为单位的内存量。 实际释放的内存将始终为整数数量的内存页。

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

**.Dvfree**命令调用**VirtualFreeEx**来释放现有内存分配。 除非 **/d**指定选项，其中包含此内存这些页释放。

此命令可用于释放所做的分配[ **.dvalloc （分配内存）**](-dvalloc--allocate-memory-.md)。 此外可用于释放的内存归目标进程中，但不是获取通过释放内存的任何块 **.dvalloc**将自然会带来的风险，目标进程的稳定性。

 

 





