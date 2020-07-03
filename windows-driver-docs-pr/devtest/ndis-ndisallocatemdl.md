---
title: NdisAllocateMdl 规则（ndis）
description: NdisAllocateMdl 规则指定按替代顺序调用 NdisAllocateMdl 和 NdisFreeMdl。 最终目标是确保在 MiniportHaltEx 结束时释放所有 MDLs。
ms.assetid: 8146E72B-0B63-4224-9677-5E6FEFCEB745
ms.date: 05/21/2018
keywords:
- NdisAllocateMdl 规则（ndis）
topic_type:
- apiref
api_name:
- NdisAllocateMdl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 061d05c0edaed2f2a29fed223a81610feba921f3
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917619"
---
# <a name="ndisallocatemdl-rule-ndis"></a>NdisAllocateMdl 规则（ndis）


**NdisAllocateMdl**规则指定按替代顺序调用[**NdisAllocateMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatemdl)和[**NdisFreeMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreemdl) 。 最终目标是确保在[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)结束时释放所有 MDLs。

此规则使用三种不同的状态。 分配或释放 MDL 后，状态会更改。 如果在[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)退出时仍分配 MDL，规则将报告缺陷。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>NdisAllocateMdl</strong>规则。</p>
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

[**NdisAllocateMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatemdl) 
[ **NdisFreeMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreemdl)
 

 





