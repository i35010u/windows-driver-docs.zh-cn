---
title: NdisAllocateNetBuffer 规则 (ndis)
description: NdisAllocateNetBuffer 规则指定备用的顺序调用 NdisAllocateNetBuffer 和 NdisFreeNetBuffer。 最终目标是确保所有实例的 NET\_MiniportHaltEx 结束时释放缓冲区。
ms.assetid: 218708DA-ADDF-4E59-900A-4F8B5CBF00B7
ms.date: 05/21/2018
keywords:
- NdisAllocateNetBuffer 规则 (ndis)
topic_type:
- apiref
api_name:
- NdisAllocateNetBuffer
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fc2231b09125a3f3be37a2a52f98cf357f7eea11
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575186"
---
# <a name="ndisallocatenetbuffer-rule-ndis"></a>NdisAllocateNetBuffer 规则 (ndis)


**NdisAllocateNetBuffer**规则指定[ **NdisAllocateNetBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff561607)并[ **NdisFreeNetBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff562582)备用顺序调用。 最终目标是确保所有实例的[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)时释放[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)结束。

此规则使用三个不同的状态。 在状态更改时[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)分配或释放时。 如果**NET\_缓冲区**仍分配时[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)退出，此规则报告缺陷。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>NdisAllocateNetBuffer</strong>规则。</p>
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

<a name="applies-to"></a>适用对象
----------

[**NdisAllocateNetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff561607)
[**NdisFreeNetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff562582)
 

 





