---
title: NdisAllocateMemoryWithTagPriority 规则（ndis）
description: NdisAllocateMemoryWithTagPriority 规则指定驱动程序不得在不提供标记的情况下调用 NdisAllocateMemoryWithTagPriority。每个内存分配应使用唯一的池标记，以确保内核调试器和驱动程序验证器可以识别不同的已分配内存块。
ms.assetid: e27fe997-366d-4fe1-ad1e-3f145dc55f30
ms.date: 05/21/2018
keywords:
- NdisAllocateMemoryWithTagPriority 规则（ndis）
topic_type:
- apiref
api_name:
- NdisAllocateMemoryWithTagPriority
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a003815b183356cc23f7c73484e883377e6e0618
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839376"
---
# <a name="ndisallocatememorywithtagpriority-rule-ndis"></a>NdisAllocateMemoryWithTagPriority 规则（ndis）


**NdisAllocateMemoryWithTagPriority**规则指定驱动程序不得在不提供*标记*的情况下调用**NdisAllocateMemoryWithTagPriority** 。

每个内存分配应使用唯一的池标记，以确保内核调试器和驱动程序验证器可以识别不同的已分配内存块。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>NdisAllocateMemoryWithTagPriority</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码（使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用范围
----------

[**NdisAllocateMemoryWithTagPriority**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatememorywithtagpriority)
 

 





