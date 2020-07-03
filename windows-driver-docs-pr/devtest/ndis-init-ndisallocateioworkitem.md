---
title: Init \_ NdisAllocateIoWorkItem 规则（ndis）
description: Init \_ NdisAllocateIoWorkItem 规则指定在 MiniportInitializeEx 期间至少调用 NdisAllocateIoWorkItem 一次，如果 MPHaltEx 成功，则至少应在 MiniportInitializeEx 中调用 NdisFreeIoWorkItem 函数一次。
ms.assetid: B7889948-741C-4C54-B27F-3175ED4EA7BA
ms.date: 05/21/2018
keywords:
- Init_NdisAllocateIoWorkItem 规则（ndis）
topic_type:
- apiref
api_name:
- Init_NdisAllocateIoWorkItem
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a8e268e0e3b202dc16d3f0ac35c518fa27fbdb5a
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918059"
---
# <a name="init_ndisallocateioworkitem-rule-ndis"></a>Init \_ NdisAllocateIoWorkItem 规则（ndis）


**Init \_ NdisAllocateIoWorkItem**规则指定在[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)期间至少调用[**NdisAllocateIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateioworkitem)一次， [**NdisFreeIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreeioworkitem)函数应：

-   - 如果[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)成功，请在 MPHaltEx 中至少调用一次。
-   - 如果*MiniportInitializeEx*失败，则在[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)中调用。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>Init_NdisAllocateIoWorkItem</strong>规则。</p>
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

[**NdisAllocateIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateioworkitem) 
[**NdisFreeIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreeioworkitem) 
[**RemoveHeadList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-removeheadlist)
 

 





