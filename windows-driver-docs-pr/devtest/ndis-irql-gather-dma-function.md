---
title: Irql \_ 收集 \_ DMA \_ 函数规则（ndis）
description: Irql \_ 收集 \_ dma \_ 函数规则指定 NDIS 散播/聚集 dma 函数必须以正确的 Irql 级别进行调用。
ms.assetid: 2ac0d238-4ca0-4b07-9318-159cd9a64d35
ms.date: 05/21/2018
keywords:
- Irql_Gather_DMA_Function 规则（ndis）
topic_type:
- apiref
api_name:
- Irql_Gather_DMA_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b6e9bda77fffb5b8bd9f4354a45a6f297384185e
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917777"
---
# <a name="irql_gather_dma_function-rule-ndis"></a>Irql \_ 收集 \_ DMA \_ 函数规则（ndis）


Irql \_ 收集 \_ dma \_ 函数规则指定 NDIS 散播/聚集 dma 函数必须以正确的 Irql 级别进行调用。

此规则验证以下 NDIS 函数：

**NdisMAllocateNetBufferSGList** 
**NdisMAllocateSharedMemoryAsyncEx** 
**NdisMDeregisterScatterGatherDma** 
**NdisMFreeNetBufferSGList** 
**NdisMRegisterScatterGatherDma**

**驱动程序模型： NDIS**

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>Irql_Gather_DMA_Function</strong>规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码（使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**NdisMAllocateNetBufferSGList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatenetbuffersglist) 
[**NdisMAllocateSharedMemoryAsyncEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatesharedmemoryasyncex) 
[**NdisMDeregisterScatterGatherDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterscattergatherdma) 
[**NdisMFreeNetBufferSGList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreenetbuffersglist) 
[**NdisMRegisterScatterGatherDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterscattergatherdma)








