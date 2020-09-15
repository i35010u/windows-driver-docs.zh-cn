---
title: 'Irql \_ 收集 \_ DMA \_ 函数规则 (ndis) '
description: Irql \_ 收集 \_ dma \_ 函数规则指定 NDIS 散播/聚集 dma 函数必须以正确的 Irql 级别进行调用。
ms.assetid: 2ac0d238-4ca0-4b07-9318-159cd9a64d35
ms.date: 05/21/2018
keywords:
- 'Irql_Gather_DMA_Function 规则 (ndis) '
topic_type:
- apiref
api_name:
- Irql_Gather_DMA_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 20d12af8522338486eefe3c15102194e9b714bda
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107106"
---
# <a name="irql_gather_dma_function-rule-ndis"></a>Irql \_ 收集 \_ DMA \_ 函数规则 (ndis) 


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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>Irql_Gather_DMA_Function</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**NdisMAllocateNetBufferSGList**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatenetbuffersglist) 
[**NdisMAllocateSharedMemoryAsyncEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatesharedmemoryasyncex) 
[**NdisMDeregisterScatterGatherDma**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterscattergatherdma) 
[**NdisMFreeNetBufferSGList**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreenetbuffersglist) 
[**NdisMRegisterScatterGatherDma**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterscattergatherdma)