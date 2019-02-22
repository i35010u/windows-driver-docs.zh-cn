---
title: NdisAllocateMemoryWithTagPriority 规则 (ndis)
description: NdisAllocateMemoryWithTagPriority 规则指定一个驱动程序必须提供 Tag.Every 内存分配应使用唯一池标记以确保该内核调试器和驱动程序验证程序可以识别没有调用 NdisAllocateMemoryWithTagPriority非重复分配的内存块。
ms.assetid: e27fe997-366d-4fe1-ad1e-3f145dc55f30
ms.date: 05/21/2018
keywords:
- NdisAllocateMemoryWithTagPriority 规则 (ndis)
topic_type:
- apiref
api_name:
- NdisAllocateMemoryWithTagPriority
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 76fa75da6afb5074bfe646bd298b1564a6a00e65
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545957"
---
# <a name="ndisallocatememorywithtagpriority-rule-ndis"></a>NdisAllocateMemoryWithTagPriority 规则 (ndis)


**NdisAllocateMemoryWithTagPriority**规则指定一个驱动程序必须调用**NdisAllocateMemoryWithTagPriority**而无需提供*标记*。

每个内存分配应使用唯一池标记来确保内核调试程序和驱动程序验证程序可以标识不同分配的内存块。

|              |      |
|--------------|------|
| 驱动程序模型 | NDIS |

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在编译时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>NdisAllocateMemoryWithTagPriority</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**NdisAllocateMemoryWithTagPriority**](https://msdn.microsoft.com/library/windows/hardware/ff561606)
 

 





