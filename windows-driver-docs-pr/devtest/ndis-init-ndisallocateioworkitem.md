---
title: Init\_NdisAllocateIoWorkItem 规则 (ndis)
description: Init\_NdisAllocateIoWorkItem 规则指定是否 NdisAllocateIoWorkItem MiniportInitializeEx 期间至少一次调用，NdisFreeIoWorkItem 函数应-调用至少一次在 MPHaltEx，如果 MiniportInitializeEx会成功。
ms.assetid: B7889948-741C-4C54-B27F-3175ED4EA7BA
ms.date: 05/21/2018
keywords:
- Init_NdisAllocateIoWorkItem rule (ndis)
topic_type:
- apiref
api_name:
- Init_NdisAllocateIoWorkItem
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 261ec7f9d4f58abd4d729678e805f6a84932126e
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392369"
---
# <a name="initndisallocateioworkitem-rule-ndis"></a>Init\_NdisAllocateIoWorkItem 规则 (ndis)


**Init\_NdisAllocateIoWorkItem**规则指定，如果[ **NdisAllocateIoWorkItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocateioworkitem)至少一次期间调用[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)，则[ **NdisFreeIoWorkItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreeioworkitem)函数应：

-   - 如果在 MPHaltEx，至少一次调用[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)成功。
-   - 在中调用[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)，如果*MiniportInitializeEx*失败。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>Init_NdisAllocateIoWorkItem</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用对象
----------

[**NdisAllocateIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocateioworkitem)
[**NdisFreeIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreeioworkitem)
[**RemoveHeadList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-removeheadlist)
 

 





