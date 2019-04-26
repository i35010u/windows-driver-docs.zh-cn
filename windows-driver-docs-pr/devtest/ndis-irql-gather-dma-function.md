---
title: Irql\_收集\_DMA\_函数规则 (ndis)
description: Irql\_收集\_DMA\_函数规则指定的 NDIS 散播-聚集 DMA 函数的调用必须在正确的 IRQL 级别。
ms.assetid: 2ac0d238-4ca0-4b07-9318-159cd9a64d35
ms.date: 05/21/2018
keywords:
- Irql_Gather_DMA_Function 规则 (ndis)
topic_type:
- apiref
api_name:
- Irql_Gather_DMA_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8ecc8276199860007b3b8589b90b7f11aa508ef2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325101"
---
# <a name="irqlgatherdmafunction-rule-ndis"></a>Irql\_收集\_DMA\_函数规则 (ndis)


Irql\_收集\_DMA\_函数规则指定的 NDIS 散播-聚集 DMA 函数的调用必须在正确的 IRQL 级别。

此规则验证以下 NDIS 函数：

**NdisMAllocateNetBufferSGList**
**NdisMAllocateSharedMemoryAsyncEx**
**NdisMDeregisterScatterGatherDma**
**NdisMFreeNetBufferSGList**
**NdisMRegisterScatterGatherDma**

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>Irql_Gather_DMA_Function</strong>规则。</p>
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

[**NdisMAllocateNetBufferSGList**](https://msdn.microsoft.com/library/windows/hardware/ff562776)
[**NdisMAllocateSharedMemoryAsyncEx** ](https://msdn.microsoft.com/library/windows/hardware/ff562784) 
 [ **NdisMDeregisterScatterGatherDma**](https://msdn.microsoft.com/library/windows/hardware/ff563581)
[**NdisMFreeNetBufferSGList** ](https://msdn.microsoft.com/library/windows/hardware/ff563586) 
 [ **NdisMRegisterScatterGatherDma**](https://msdn.microsoft.com/library/windows/hardware/ff563659)








