---
title: 提前创建关键节事件
description: 提前创建关键节事件
keywords:
- '早期关键部分事件创建 (全局标志) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0892367b5d7c961e06b695d9c2828e6a5d3b7bfd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838649"
---
# <a name="early-critical-section-event-creation"></a>提前创建关键节事件


## <span id="ddk_early_critical_section_event_creation_dtools"></span><span id="DDK_EARLY_CRITICAL_SECTION_EVENT_CREATION_DTOOLS"></span>


在初始化关键节时，" **早期关键部分事件创建** " 标志会创建事件句柄，而不是等到需要该事件时。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>cse</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x10000000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_CRITSEC_EVENT_CREATION</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>系统范围的注册表项、内核标志、映像文件注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

当 Windows 无法创建事件时，它会在初始化期间生成异常，而进入并离开临界区的调用将失败。

由于此标志使用大量的非分页池内存，因此只能在具有足够内存的非常可靠系统上使用它。

 

 





