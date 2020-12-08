---
title: 释放时禁用堆合并
description: 释放时禁用堆合并
keywords:
- '在可用 (全局标志上禁用堆合并) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c2c99ca2ef234c6ea5c35f966c8031f9c6c30cb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826161"
---
# <a name="disable-heap-coalesce-on-free"></a>释放时禁用堆合并


## <span id="ddk_disable_heap_coalesce_on_free_dtools"></span><span id="DDK_DISABLE_HEAP_COALESCE_ON_FREE_DTOOLS"></span>


在释放时 **禁用堆合并** 会使相邻堆内存块在释放时保持分离。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>dhc</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x00200000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_HEAP_DISABLE_COALESCING</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>系统范围的注册表项、内核标志、映像文件注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

默认情况下，Windows 将 ( "合并" ) 新释放的相邻块合并为单个块。 组合块需要时间，但在找不到连续内存时，减少可能强制堆分配更多内存的碎片。

此标志用于维护与旧应用程序的兼容性。

 

 





